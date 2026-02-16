# Distributed Rate Limiter

## Problem Statement

Design a distributed rate limiting system that can enforce API quotas across multiple application servers and data centers.

**Scale Requirements:**
- 100,000 API clients
- 1 million requests per second across all clients
- Rate limits: Per-user, per-API-key, per-IP, per-endpoint
- Multi-region deployment (5 regions globally)
- Sub-millisecond latency overhead

**Business Constraints:**
- Accurate rate limiting (no significant over-limiting or under-limiting)
- Support multiple rate limit windows (1 second, 1 minute, 1 hour, 1 day)
- Support burst allowances
- Graceful degradation if rate limiter fails
- Real-time quota visibility for users

**Failure Expectations:**
- System should fail open (allow requests) if rate limiter unavailable
- No data loss of quota information
- Consistent enforcement across regions

**Edge Cases:**
- Clock skew across distributed systems
- Network partitions between regions
- Burst traffic patterns
- Quota resets at window boundaries
- Concurrent requests from same user

## Functional Requirements

- Enforce rate limits per user/API key
- Support multiple time windows (sliding and fixed)
- Track quota consumption in real-time
- Provide quota remaining information in API responses
- Support burst allowances
- Allow dynamic rate limit updates
- Provide admin API for quota management
- Support rate limit exemptions (whitelisting)
- Log rate limit violations

## Non-Functional Requirements

- **Availability:** 99.99%
- **Latency:** < 1ms P99 overhead for rate limit check
- **Throughput:** 1M RPS
- **Consistency:** Strong consistency within region, eventual across regions
- **Durability:** Quota state persisted, recoverable after failures
- **Accuracy:** < 1% error rate in quota enforcement
- **Scalability:** Linear scaling with number of API keys

## Core Engineering Challenges

1. **Distributed Counter Consistency**
   - Multiple servers incrementing same counter simultaneously
   - Race conditions in read-increment-write operations
   - Atomic operations across distributed systems

2. **Clock Synchronization**
   - Different servers have different system times
   - Window boundary calculations inconsistent
   - Sliding window implementation complexity

3. **High Throughput with Low Latency**
   - 1M RPS requires sub-millisecond operations
   - Network round-trips add latency
   - Database locks cause contention

4. **Sliding Window Implementation**
   - Fixed windows allow burst at boundaries
   - Sliding windows require historical data
   - Memory efficiency for millions of keys

5. **Multi-Region Coordination**
   - Global rate limits across regions
   - Network latency between regions (100-300ms)
   - Partition tolerance vs consistency trade-off

6. **Burst Handling**
   - Allow temporary exceeding of rate limit
   - Token bucket vs leaky bucket algorithms
   - Refill rate calculations

## High-Level Design (HLD)

### System Architecture Overview

The distributed rate limiter uses a **regional-first architecture** with the following key components:

1. **Regional Redis Clusters** - Low-latency rate limit counters per region
2. **API Gateway Layer** - Rate limit enforcement before request processing
3. **Configuration Service** - Centralized rate limit policy management
4. **Sync Service** - Cross-region quota synchronization for global limits
5. **Monitoring Service** - Real-time quota tracking and alerting

### Architecture Diagram

```
                            API Clients (100K)
                                   │
                                   ▼
                          Global Load Balancer
                                   │
        ┌──────────────────────────┼──────────────────────────┐
        ▼                          ▼                          ▼
    Region 1                   Region 2                   Region 3
        │                          │                          │
        ▼                          ▼                          ▼
  Regional LB                Regional LB                Regional LB
        │                          │                          │
        ▼                          ▼                          ▼
  API Servers                API Servers                API Servers
  (Stateless)                (Stateless)                (Stateless)
        │                          │                          │
        └──────────────────────────┼──────────────────────────┘
                                   │
                    ┌──────────────┼──────────────┐
                    ▼              ▼              ▼
              Redis Cluster   Redis Cluster   Redis Cluster
              (Region 1)      (Region 2)      (Region 3)
                    │              │              │
                    └──────────────┼──────────────┘
                                   │
                                   ▼
                          Cross-Region Sync
                          (Async Replication)
                                   │
                                   ▼
                            PostgreSQL
                        (Rate Limit Config)
```

### Component Responsibilities

**1. Global Load Balancer:**
- Route requests to nearest region (latency-based)
- Health check regional endpoints
- Failover to backup regions
- DDoS protection

**2. API Gateway:**
- Extract rate limit identifiers (user_id, API key, IP)
- Enforce rate limits before request processing
- Add rate limit headers to responses
- Log rate limit violations

**3. Regional Redis Clusters:**
- Store rate limit counters (per user/key/IP)
- Atomic increment operations
- TTL-based automatic cleanup
- Sub-millisecond latency

**4. Configuration Service:**
- Manage rate limit policies
- Support dynamic updates
- Cache configurations locally
- Validate policy changes

**5. Cross-Region Sync Service:**
- Aggregate quota usage across regions
- Synchronize global rate limits
- Handle network partitions
- Eventual consistency guarantees

**6. PostgreSQL:**
- Durable storage for rate limit configurations
- Audit trail for policy changes
- Historical quota usage data
- Analytics and reporting

### Data Flow

```
1. Request Arrival
   Client → Global LB → Regional LB → API Gateway

2. Rate Limit Check (Regional)
   API Gateway → Extract Identifier (user_id/API key)
   → Check Local Cache (rate limit config)
   → Redis (EVAL Lua script for atomic check)
   → Response: ALLOW or DENY

3. Rate Limit Check (Global)
   API Gateway → Redis (local region counter)
   → Sync Service (aggregate across regions)
   → Redis (update global counter)
   → Response: ALLOW or DENY

4. Request Processing (if allowed)
   API Gateway → Backend Service
   → Response with headers:
      X-RateLimit-Limit: 1000
      X-RateLimit-Remaining: 742
      X-RateLimit-Reset: 1642348800

5. Cross-Region Sync (Async)
   Sync Service → Poll regional Redis (every 100ms)
   → Aggregate counts
   → Update global counters
   → Propagate to all regions
```

### Scalability Strategy

**Horizontal Scaling:**
- API Gateways: Auto-scale based on request rate
- Redis: Cluster mode with 3-12 shards per region
- Sync Service: One active instance per region (leader election)
- PostgreSQL: Read replicas for configuration queries

**Vertical Scaling:**
- Redis: r6g.xlarge (32 GB RAM) for millions of keys
- API Gateway: c6g.large (2 vCPU) for CPU-intensive operations
- Sync Service: c6g.xlarge (4 vCPU) for aggregation

**Partitioning:**
- Redis: Shard by identifier hash (user_id, API key)
- PostgreSQL: Partition quota_usage table by date
- Regional isolation: Each region independent

**Caching:**
- Rate limit configs: 1-minute TTL in API gateway memory
- User quotas: No caching (always check Redis)
- Global aggregates: 100ms TTL in sync service

### Failure Handling

**Redis Failure:**
- Fail open: Allow requests (graceful degradation)
- Log failures for audit
- Automatic failover to replica (< 30s RTO)
- Alert operations team

**Sync Service Failure:**
- Regional limits continue working
- Global limits may be inaccurate temporarily
- Automatic leader re-election
- Catch-up sync when recovered

**Network Partition:**
- Regional limits enforced independently
- Global limits may allow over-quota temporarily
- Reconciliation after partition heals
- Alert on quota violations

**PostgreSQL Failure:**
- Use cached rate limit configurations
- New policy updates blocked
- Failover to read replica
- No impact on rate limiting (Redis is source of truth)

## Low-Level Design (LLD)

### Class Diagram

```
┌─────────────────────────┐
│   RateLimiterMiddleware │
├─────────────────────────┤
│ + call(request)         │
│ - check_rate_limit()    │
│ - add_headers()         │
└─────────────────────────┘
            │
            │ uses
            ▼
┌─────────────────────────┐
│   RateLimitChecker      │
├─────────────────────────┤
│ - redis: Redis          │
│ - config: Config        │
├─────────────────────────┤
│ + check(identifier)     │
│ + get_remaining()       │
│ - get_window_key()      │
└─────────────────────────┘
            │
            │ uses
            ▼
┌─────────────────────────┐
│  SlidingWindowLimiter   │
├─────────────────────────┤
│ - redis: Redis          │
│ - window_size: Integer  │
├─────────────────────────┤
│ + allow?(identifier)    │
│ - cleanup_old_entries() │
└─────────────────────────┘

┌─────────────────────────┐
│   TokenBucketLimiter    │
├─────────────────────────┤
│ - redis: Redis          │
│ - capacity: Integer     │
│ - refill_rate: Float    │
├─────────────────────────┤
│ + allow?(identifier)    │
│ - refill_tokens()       │
└─────────────────────────┘

┌─────────────────────────┐
│   FixedWindowLimiter    │
├─────────────────────────┤
│ - redis: Redis          │
│ - window_size: Integer  │
├─────────────────────────┤
│ + allow?(identifier)    │
│ - get_current_window()  │
└─────────────────────────┘

┌─────────────────────────┐
│  CrossRegionSyncService │
├─────────────────────────┤
│ - redis_clusters: Array │
│ - sync_interval: Integer│
├─────────────────────────┤
│ + sync_quotas()         │
│ - aggregate_counts()    │
│ - propagate_to_regions()│
└─────────────────────────┘

┌─────────────────────────┐
│   RateLimitConfig       │
├─────────────────────────┤
│ + load_from_db()        │
│ + cache_locally()       │
│ + validate()            │
└─────────────────────────┘
```

### Database Schema Details

**Rate Limit Policies Table:**
```sql
CREATE TABLE rate_limit_policies (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    name VARCHAR(255) NOT NULL,
    identifier_type VARCHAR(50) NOT NULL, -- user_id, api_key, ip_address
    limit_value INTEGER NOT NULL,
    window_size INTEGER NOT NULL,        -- in seconds
    window_type VARCHAR(50) NOT NULL,    -- sliding, fixed, token_bucket
    burst_allowance INTEGER DEFAULT 0,
    scope VARCHAR(50) NOT NULL,          -- regional, global
    enabled BOOLEAN DEFAULT true,
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),

    CONSTRAINT positive_limit CHECK (limit_value > 0),
    CONSTRAINT positive_window CHECK (window_size > 0)
);

CREATE INDEX idx_policies_identifier_type ON rate_limit_policies(identifier_type);
CREATE INDEX idx_policies_enabled ON rate_limit_policies(enabled) WHERE enabled = true;
```

**Quota Usage Table (Analytics):**
```sql
CREATE TABLE quota_usage (
    id BIGSERIAL PRIMARY KEY,
    identifier VARCHAR(255) NOT NULL,
    identifier_type VARCHAR(50) NOT NULL,
    policy_id UUID REFERENCES rate_limit_policies(id),
    requests_count INTEGER NOT NULL,
    window_start TIMESTAMP NOT NULL,
    window_end TIMESTAMP NOT NULL,
    region VARCHAR(50) NOT NULL,
    created_at TIMESTAMP DEFAULT NOW()
) PARTITION BY RANGE (window_start);

-- Monthly partitions
CREATE TABLE quota_usage_2024_01 PARTITION OF quota_usage
    FOR VALUES FROM ('2024-01-01') TO ('2024-02-01');

CREATE INDEX idx_quota_usage_identifier ON quota_usage(identifier, window_start DESC);
CREATE INDEX idx_quota_usage_policy ON quota_usage(policy_id, window_start DESC);
```

### API Endpoints

**Rate Limit Check API (Internal):**

```ruby
# Check if request is allowed
POST /internal/rate_limit/check
{
  "identifier": "user:123",
  "identifier_type": "user_id",
  "endpoint": "/api/v1/users"
}

Response: 200 OK
{
  "allowed": true,
  "limit": 1000,
  "remaining": 742,
  "reset_at": "2024-01-16T12:00:00Z",
  "retry_after": null
}

Response: 429 Too Many Requests
{
  "allowed": false,
  "limit": 1000,
  "remaining": 0,
  "reset_at": "2024-01-16T12:00:00Z",
  "retry_after": 45
}
```

**Admin API:**

```ruby
# Create rate limit policy
POST /admin/rate_limits
{
  "name": "API Key Limit",
  "identifier_type": "api_key",
  "limit_value": 10000,
  "window_size": 3600,
  "window_type": "sliding",
  "scope": "global"
}

# Update policy
PATCH /admin/rate_limits/:id
{
  "limit_value": 15000
}

# Get quota usage
GET /admin/rate_limits/:id/usage?start_date=2024-01-01&end_date=2024-01-31
```

### Algorithms

**1. Sliding Window Algorithm (Lua Script):**

```ruby
SLIDING_WINDOW_SCRIPT = <<~LUA
  local key = KEYS[1]
  local now = tonumber(ARGV[1])
  local window = tonumber(ARGV[2])
  local limit = tonumber(ARGV[3])

  -- Remove entries outside window
  local window_start = now - window
  redis.call('ZREMRANGEBYSCORE', key, '-inf', window_start)

  -- Count requests in current window
  local count = redis.call('ZCARD', key)

  if count < limit then
    -- Add current request
    redis.call('ZADD', key, now, now .. ':' .. math.random())
    redis.call('EXPIRE', key, window + 1)
    return {1, limit - count - 1}  -- [allowed, remaining]
  else
    return {0, 0}  -- [denied, remaining]
  end
LUA

def check_sliding_window(identifier, limit:, window:)
  key = "ratelimit:sliding:#{identifier}"
  now = Time.current.to_f

  allowed, remaining = redis.eval(
    SLIDING_WINDOW_SCRIPT,
    keys: [key],
    argv: [now, window, limit]
  )

  {
    allowed: allowed == 1,
    remaining: remaining,
    reset_at: Time.at(now + window)
  }
end
```

**2. Token Bucket Algorithm:**

```ruby
TOKEN_BUCKET_SCRIPT = <<~LUA
  local key = KEYS[1]
  local capacity = tonumber(ARGV[1])
  local refill_rate = tonumber(ARGV[2])
  local now = tonumber(ARGV[3])
  local requested = tonumber(ARGV[4])

  -- Get current state
  local state = redis.call('HMGET', key, 'tokens', 'last_refill')
  local tokens = tonumber(state[1]) or capacity
  local last_refill = tonumber(state[2]) or now

  -- Calculate tokens to add
  local time_passed = now - last_refill
  local tokens_to_add = time_passed * refill_rate
  tokens = math.min(capacity, tokens + tokens_to_add)

  -- Check if request can be allowed
  if tokens >= requested then
    tokens = tokens - requested
    redis.call('HMSET', key, 'tokens', tokens, 'last_refill', now)
    redis.call('EXPIRE', key, 3600)
    return {1, math.floor(tokens)}  -- [allowed, remaining]
  else
    redis.call('HMSET', key, 'tokens', tokens, 'last_refill', now)
    redis.call('EXPIRE', key, 3600)
    return {0, math.floor(tokens)}  -- [denied, remaining]
  end
LUA

def check_token_bucket(identifier, capacity:, refill_rate:, requested: 1)
  key = "ratelimit:token_bucket:#{identifier}"
  now = Time.current.to_f

  allowed, remaining = redis.eval(
    TOKEN_BUCKET_SCRIPT,
    keys: [key],
    argv: [capacity, refill_rate, now, requested]
  )

  {
    allowed: allowed == 1,
    remaining: remaining,
    reset_at: Time.at(now + (capacity - remaining) / refill_rate)
  }
end
```

**3. Fixed Window Algorithm:**

```ruby
def check_fixed_window(identifier, limit:, window:)
  # Calculate current window bucket
  now = Time.current.to_i
  window_start = (now / window) * window

  key = "ratelimit:fixed:#{identifier}:#{window_start}"

  # Atomic increment
  count = redis.incr(key)

  # Set expiry on first request
  redis.expire(key, window * 2) if count == 1

  {
    allowed: count <= limit,
    remaining: [limit - count, 0].max,
    reset_at: Time.at(window_start + window)
  }
end
```

**4. Cross-Region Sync Algorithm:**

```ruby
class CrossRegionSyncService
  SYNC_INTERVAL = 0.1  # 100ms

  def sync_global_quotas
    loop do
      global_policies = RateLimitPolicy.where(scope: 'global')

      global_policies.each do |policy|
        # Aggregate counts from all regions
        total_count = aggregate_regional_counts(policy)

        # Check if global limit exceeded
        if total_count > policy.limit_value
          # Propagate block to all regions
          propagate_block(policy)
        else
          # Update global counter
          update_global_counter(policy, total_count)
        end
      end

      sleep SYNC_INTERVAL
    end
  end

  private

  def aggregate_regional_counts(policy)
    regions = ['us-east', 'eu-west', 'ap-south']

    counts = regions.map do |region|
      redis = redis_for_region(region)
      pattern = "ratelimit:*:#{policy.identifier_type}:*"

      keys = redis.scan_each(match: pattern).to_a
      keys.sum { |key| redis.get(key).to_i }
    end

    counts.sum
  end

  def propagate_block(policy)
    regions.each do |region|
      redis = redis_for_region(region)
      redis.setex(
        "ratelimit:global_block:#{policy.id}",
        60,
        '1'
      )
    end
  end
end
```

**5. Adaptive Rate Limiting:**

```ruby
def adaptive_rate_limit(identifier, base_limit:)
  # Adjust limit based on system load
  current_load = get_system_load

  adjusted_limit = case current_load
  when 0..50
    base_limit * 1.5  # Low load, allow more
  when 51..80
    base_limit        # Normal load
  when 81..95
    base_limit * 0.7  # High load, reduce
  else
    base_limit * 0.5  # Critical load, reduce significantly
  end

  check_sliding_window(identifier, limit: adjusted_limit.to_i, window: 60)
end

def get_system_load
  # CPU, memory, queue depth, etc.
  cpu_usage = SystemMetrics.cpu_usage
  memory_usage = SystemMetrics.memory_usage
  queue_depth = SystemMetrics.queue_depth

  [cpu_usage, memory_usage, queue_depth].max
end
```

### Sequence Diagrams

**Rate Limit Check Flow:**

```
Client    API Gateway   Redis   Sync Service   Other Regions
 │             │          │            │              │
 │─Request────>│          │            │              │
 │             │          │            │              │
 │             │─Extract Identifier    │              │
 │             │─Get Policy (cache)    │              │
 │             │          │            │              │
 │             │─EVAL Lua Script──────>│              │
 │             │<─Result (allowed=true, remaining=742)│
 │             │          │            │              │
 │             │─Add Headers           │              │
 │             │  X-RateLimit-Limit: 1000             │
 │             │  X-RateLimit-Remaining: 742          │
 │             │          │            │              │
 │<─200 OK─────│          │            │              │
 │             │          │            │              │
 │             │          │            │─Aggregate────>│
 │             │          │            │<─Counts──────│
 │             │          │            │              │
 │             │          │<─Update Global Counter────│
```

**Rate Limit Exceeded Flow:**

```
Client    API Gateway   Redis
 │             │          │
 │─Request────>│          │
 │             │          │
 │             │─EVAL Lua Script──────>│
 │             │<─Result (allowed=false, remaining=0)
 │             │          │
 │             │─Log Violation
 │             │─Add Headers
 │             │  X-RateLimit-Limit: 1000
 │             │  X-RateLimit-Remaining: 0
 │             │  X-RateLimit-Reset: 1642348800
 │             │  Retry-After: 45
 │             │          │
 │<─429 Too Many Requests─│
```

### Performance Optimizations

**1. Local Caching:**
```ruby
# Cache rate limit policies in memory
class RateLimitConfigCache
  TTL = 60  # 1 minute

  def get_policy(identifier_type)
    cache_key = "policy:#{identifier_type}"

    Rails.cache.fetch(cache_key, expires_in: TTL) do
      RateLimitPolicy.find_by(identifier_type: identifier_type)
    end
  end
end
```

**2. Redis Pipelining:**
```ruby
# Check multiple rate limits in one round-trip
def check_multiple_limits(identifier, policies)
  redis.pipelined do
    policies.each do |policy|
      check_sliding_window(identifier, limit: policy.limit_value, window: policy.window_size)
    end
  end
end
```

**3. Bloom Filters for Whitelisting:**
```ruby
# Fast whitelist check
def whitelisted?(identifier)
  # Bloom filter: O(1) lookup, small memory footprint
  bloom_filter.include?(identifier)
end
```

**4. Connection Pooling:**
```ruby
REDIS_POOL = ConnectionPool.new(size: 100, timeout: 1) do
  Redis.new(url: ENV['REDIS_URL'])
end

def with_redis(&block)
  REDIS_POOL.with(&block)
end
```

**5. Batch Aggregation:**
```ruby
# Aggregate regional counts in batches
def aggregate_in_batches(identifiers, batch_size: 1000)
  identifiers.each_slice(batch_size) do |batch|
    counts = redis.pipelined do
      batch.each { |id| redis.get("ratelimit:#{id}") }
    end

    process_counts(batch.zip(counts))
  end
end
```

## Step-by-Step Request Flow

### Rate Limit Check (Happy Path)

1. **Request arrives at API server**
   - Extract identifier (user_id, api_key, IP)
   - Determine applicable rate limits
   - Check local cache for rate limit config (1-minute TTL)

2. **Check Redis for current quota**
   ```
   Key: ratelimit:{user_id}:{window}:{bucket}
   Example: ratelimit:user:123:minute:2024-01-15T10:05
   ```

3. **Sliding Window Algorithm (Lua Script)**
   ```lua
   -- Remove old entries outside window
   -- Count entries in current window
   -- If count < limit, add new entry
   -- Return: allowed (true/false), remaining, reset_time
   ```

4. **Response to client**
   - Headers:
     - `X-RateLimit-Limit: 1000`
     - `X-RateLimit-Remaining: 847`
     - `X-RateLimit-Reset: 1642243560`
   - If exceeded: `429 Too Many Requests`

5. **Async: Update metrics**
   - Increment violation counter if limit exceeded
   - Log to analytics system
   - Alert if sustained violations

### Failure Scenarios

**Scenario 1: Redis unavailable**
- Fallback: Allow request (fail open)
- Log warning
- Use local in-memory counter (best effort)
- Alert ops team

**Scenario 2: Clock skew**
- Use Redis server time (TIME command)
- Normalize all timestamps to UTC
- Periodic NTP sync on all servers

**Scenario 3: Network partition**
- Regional rate limits enforced independently
- Global limits may be temporarily inaccurate
- Reconciliation after partition heals

## Data Model Design

### Redis Data Structures

**Sliding Window (Sorted Set):**
```
Key: ratelimit:user:{user_id}:window:{window_size}
Type: SORTED SET
Score: timestamp (milliseconds)
Member: request_id (UUID)
TTL: 2 * window_size

Example:
ZADD ratelimit:user:123:window:60 1642243500123 "req_uuid_1"
ZADD ratelimit:user:123:window:60 1642243501456 "req_uuid_2"
```

**Token Bucket (Hash):**
```
Key: ratelimit:bucket:{user_id}
Type: HASH
Fields:
  - tokens: current token count
  - last_refill: last refill timestamp
TTL: 1 hour

Example:
HSET ratelimit:bucket:123 tokens 50 last_refill 1642243500
```

**Fixed Window (String):**
```
Key: ratelimit:fixed:{user_id}:{bucket_timestamp}
Type: STRING (counter)
Value: request count
TTL: window_size

Example:
INCR ratelimit:fixed:123:1642243500
EXPIRE ratelimit:fixed:123:1642243500 60
```

### PostgreSQL Schema

```sql
-- Rate limit configurations
CREATE TABLE rate_limit_configs (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    entity_type VARCHAR(50) NOT NULL,  -- 'user', 'api_key', 'ip'
    entity_id VARCHAR(255) NOT NULL,
    endpoint_pattern VARCHAR(255),     -- '/api/v1/*' or NULL for all
    limit_value INTEGER NOT NULL,
    window_seconds INTEGER NOT NULL,   -- 1, 60, 3600, 86400
    burst_allowance INTEGER DEFAULT 0,
    algorithm VARCHAR(50) NOT NULL,    -- 'sliding_window', 'token_bucket', 'fixed_window'
    enabled BOOLEAN DEFAULT true,
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),

    UNIQUE(entity_type, entity_id, endpoint_pattern, window_seconds)
);

CREATE INDEX idx_rate_limit_entity ON rate_limit_configs(entity_type, entity_id);
CREATE INDEX idx_rate_limit_enabled ON rate_limit_configs(enabled) WHERE enabled = true;

-- Rate limit violations log
CREATE TABLE rate_limit_violations (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    entity_type VARCHAR(50) NOT NULL,
    entity_id VARCHAR(255) NOT NULL,
    endpoint VARCHAR(255) NOT NULL,
    limit_value INTEGER NOT NULL,
    actual_count INTEGER NOT NULL,
    window_seconds INTEGER NOT NULL,
    violated_at TIMESTAMP DEFAULT NOW(),
    region VARCHAR(50) NOT NULL
);

-- Partition by violated_at (daily partitions)
CREATE INDEX idx_violations_entity ON rate_limit_violations(entity_type, entity_id, violated_at);
CREATE INDEX idx_violations_time ON rate_limit_violations(violated_at);
```

## Concurrency & Consistency Strategy

### Sliding Window with Lua Script

**Why Lua?**
- Atomic execution (no race conditions)
- Runs on Redis server (no network round-trips)
- Can perform complex logic

**Implementation:**

```ruby
class SlidingWindowRateLimiter
  def initialize(redis, user_id, limit, window_seconds)
    @redis = redis
    @user_id = user_id
    @limit = limit
    @window_seconds = window_seconds
    @key = "ratelimit:user:#{user_id}:window:#{window_seconds}"
  end

  def allow_request?
    now_ms = (Time.now.to_f * 1000).to_i
    window_start_ms = now_ms - (@window_seconds * 1000)

    lua_script = <<~LUA
      local key = KEYS[1]
      local now_ms = tonumber(ARGV[1])
      local window_start_ms = tonumber(ARGV[2])
      local limit = tonumber(ARGV[3])
      local window_seconds = tonumber(ARGV[4])
      local request_id = ARGV[5]

      -- Remove entries outside current window
      redis.call('ZREMRANGEBYSCORE', key, '-inf', window_start_ms)

      -- Count current requests in window
      local current_count = redis.call('ZCARD', key)

      if current_count < limit then
        -- Allow request
        redis.call('ZADD', key, now_ms, request_id)
        redis.call('EXPIRE', key, window_seconds * 2)

        local remaining = limit - current_count - 1
        return {1, remaining, now_ms + (window_seconds * 1000)}
      else
        -- Deny request
        local oldest_entry = redis.call('ZRANGE', key, 0, 0, 'WITHSCORES')
        local reset_time = tonumber(oldest_entry[2]) + (window_seconds * 1000)
        return {0, 0, reset_time}
      end
    LUA

    request_id = SecureRandom.uuid
    result = @redis.eval(
      lua_script,
      keys: [@key],
      argv: [now_ms, window_start_ms, @limit, @window_seconds, request_id]
    )

    allowed, remaining, reset_time = result

    {
      allowed: allowed == 1,
      remaining: remaining,
      reset_at: Time.at(reset_time / 1000.0)
    }
  rescue Redis::BaseError => e
    # Fail open: allow request if Redis unavailable
    Rails.logger.error("Rate limiter Redis error: #{e.message}")
    { allowed: true, remaining: -1, reset_at: nil, degraded: true }
  end
end
```

### Token Bucket Algorithm

**Better for burst handling:**

```ruby
class TokenBucketRateLimiter
  def initialize(redis, user_id, capacity, refill_rate)
    @redis = redis
    @user_id = user_id
    @capacity = capacity  # Max tokens
    @refill_rate = refill_rate  # Tokens per second
    @key = "ratelimit:bucket:#{user_id}"
  end

  def allow_request?(tokens_required = 1)
    lua_script = <<~LUA
      local key = KEYS[1]
      local capacity = tonumber(ARGV[1])
      local refill_rate = tonumber(ARGV[2])
      local tokens_required = tonumber(ARGV[3])
      local now = tonumber(ARGV[4])

      -- Get current state
      local bucket = redis.call('HMGET', key, 'tokens', 'last_refill')
      local tokens = tonumber(bucket[1])
      local last_refill = tonumber(bucket[2])

      -- Initialize if doesn't exist
      if not tokens then
        tokens = capacity
        last_refill = now
      end

      -- Calculate tokens to add based on time elapsed
      local time_elapsed = now - last_refill
      local tokens_to_add = time_elapsed * refill_rate
      tokens = math.min(capacity, tokens + tokens_to_add)

      -- Check if enough tokens
      if tokens >= tokens_required then
        -- Consume tokens
        tokens = tokens - tokens_required
        redis.call('HMSET', key, 'tokens', tokens, 'last_refill', now)
        redis.call('EXPIRE', key, 3600)
        return {1, math.floor(tokens)}
      else
        -- Not enough tokens
        redis.call('HMSET', key, 'tokens', tokens, 'last_refill', now)
        redis.call('EXPIRE', key, 3600)
        return {0, math.floor(tokens)}
      end
    LUA

    now = Time.now.to_f
    result = @redis.eval(
      lua_script,
      keys: [@key],
      argv: [@capacity, @refill_rate, tokens_required, now]
    )

    allowed, remaining = result
    {
      allowed: allowed == 1,
      remaining: remaining
    }
  end
end
```

## Ruby Implementation Examples

### Rate Limiter Middleware

```ruby
class RateLimiterMiddleware
  def initialize(app)
    @app = app
    @redis = Redis.new(url: ENV['REDIS_URL'])
  end

  def call(env)
    request = Rack::Request.new(env)

    # Extract identifier
    identifier = extract_identifier(request)
    endpoint = request.path

    # Get rate limit config
    config = RateLimitConfig.find_for(identifier, endpoint)
    return @app.call(env) unless config

    # Check rate limit
    limiter = create_limiter(config, identifier)
    result = limiter.allow_request?

    # Add headers
    headers = {
      'X-RateLimit-Limit' => config.limit_value.to_s,
      'X-RateLimit-Remaining' => result[:remaining].to_s,
      'X-RateLimit-Reset' => result[:reset_at]&.to_i.to_s
    }

    if result[:allowed]
      # Allow request
      status, response_headers, body = @app.call(env)
      [status, response_headers.merge(headers), body]
    else
      # Deny request
      log_violation(identifier, endpoint, config)
      [
        429,
        headers.merge('Content-Type' => 'application/json'),
        [{ error: 'Rate limit exceeded', retry_after: result[:reset_at] }.to_json]
      ]
    end
  end

  private

  def extract_identifier(request)
    # Priority: API key > User ID > IP address
    request.env['HTTP_X_API_KEY'] ||
      request.env['rack.session']&.[]('user_id') ||
      request.ip
  end

  def create_limiter(config, identifier)
    case config.algorithm
    when 'sliding_window'
      SlidingWindowRateLimiter.new(
        @redis,
        identifier,
        config.limit_value,
        config.window_seconds
      )
    when 'token_bucket'
      TokenBucketRateLimiter.new(
        @redis,
        identifier,
        config.limit_value,
        config.limit_value.to_f / config.window_seconds
      )
    when 'fixed_window'
      FixedWindowRateLimiter.new(
        @redis,
        identifier,
        config.limit_value,
        config.window_seconds
      )
    end
  end

  def log_violation(identifier, endpoint, config)
    RateLimitViolation.create!(
      entity_type: identifier.start_with?('user:') ? 'user' : 'api_key',
      entity_id: identifier,
      endpoint: endpoint,
      limit_value: config.limit_value,
      window_seconds: config.window_seconds,
      region: ENV['AWS_REGION']
    )
  rescue => e
    Rails.logger.error("Failed to log rate limit violation: #{e.message}")
  end
end
```

### Fixed Window Implementation (Simpler, Less Accurate)

```ruby
class FixedWindowRateLimiter
  def initialize(redis, user_id, limit, window_seconds)
    @redis = redis
    @user_id = user_id
    @limit = limit
    @window_seconds = window_seconds
  end

  def allow_request?
    # Calculate current window bucket
    now = Time.now.to_i
    bucket = (now / @window_seconds) * @window_seconds
    key = "ratelimit:fixed:#{@user_id}:#{bucket}"

    # Atomic increment and check
    count = @redis.incr(key)

    # Set expiry on first request in window
    @redis.expire(key, @window_seconds * 2) if count == 1

    if count <= @limit
      {
        allowed: true,
        remaining: @limit - count,
        reset_at: Time.at(bucket + @window_seconds)
      }
    else
      {
        allowed: false,
        remaining: 0,
        reset_at: Time.at(bucket + @window_seconds)
      }
    end
  end
end
```

### Multi-Tier Rate Limiting

```ruby
class MultiTierRateLimiter
  def initialize(redis, user_id)
    @redis = redis
    @user_id = user_id
  end

  def allow_request?
    # Check multiple tiers (all must pass)
    tiers = [
      { limit: 10, window: 1 },      # 10 req/second
      { limit: 100, window: 60 },    # 100 req/minute
      { limit: 1000, window: 3600 }  # 1000 req/hour
    ]

    results = tiers.map do |tier|
      limiter = SlidingWindowRateLimiter.new(
        @redis,
        @user_id,
        tier[:limit],
        tier[:window]
      )
      limiter.allow_request?
    end

    # All tiers must allow
    if results.all? { |r| r[:allowed] }
      # Return most restrictive remaining count
      min_remaining = results.min_by { |r| r[:remaining] }
      min_remaining
    else
      # Return first violated tier
      results.find { |r| !r[:allowed] }
    end
  end
end
```

## Scaling Strategy

### Horizontal Scaling

**Redis Cluster:**
- Shard by user_id (consistent hashing)
- 10 shards, each with 1 primary + 2 replicas
- Each shard handles ~10K users
- Total capacity: 100K users

**API Servers:**
- Stateless, auto-scale based on CPU
- Minimum: 20 instances per region
- Maximum: 200 instances per region

### Vertical Scaling

**Redis:**
- Instance type: r6g.xlarge (32 GB RAM)
- Reason: In-memory storage for millions of sorted sets

### Caching Strategy

**Rate Limit Configs:**
- Cache in application memory (1-minute TTL)
- Reduces PostgreSQL load
- Invalidate on config update

```ruby
class RateLimitConfig
  def self.find_for(identifier, endpoint)
    cache_key = "rate_limit_config:#{identifier}:#{endpoint}"

    Rails.cache.fetch(cache_key, expires_in: 1.minute) do
      where(entity_id: identifier)
        .where('endpoint_pattern IS NULL OR ? LIKE endpoint_pattern', endpoint)
        .where(enabled: true)
        .order('endpoint_pattern DESC NULLS LAST')
        .first
    end
  end
end
```

## High Availability Strategy

### Multi-Region Deployment

**Regional Independence:**
- Each region has own Redis cluster
- Rate limits enforced locally
- Async replication for global limits

**Global Rate Limits:**
```ruby
class GlobalRateLimiter
  def initialize(redis_clusters, user_id, global_limit, window)
    @redis_clusters = redis_clusters  # Hash of region => redis_client
    @user_id = user_id
    @global_limit = global_limit
    @window = window
  end

  def allow_request?(current_region)
    # Check local region first (fast)
    local_limiter = SlidingWindowRateLimiter.new(
      @redis_clusters[current_region],
      @user_id,
      @global_limit,
      @window
    )

    local_result = local_limiter.allow_request?
    return local_result unless local_result[:allowed]

    # Async: Aggregate counts from all regions
    GlobalRateLimitSyncJob.perform_later(@user_id, current_region)

    local_result
  end
end

class GlobalRateLimitSyncJob < ApplicationJob
  def perform(user_id, current_region)
    # Aggregate counts from all regions
    total_count = REDIS_CLUSTERS.sum do |region, redis|
      key = "ratelimit:user:#{user_id}:window:60"
      redis.zcard(key)
    end

    # If global limit exceeded, mark user
    if total_count > GLOBAL_LIMIT
      REDIS_CLUSTERS.each do |region, redis|
        redis.setex("ratelimit:global_exceeded:#{user_id}", 60, "1")
      end
    end
  end
end
```

### Circuit Breaker

```ruby
class RateLimiterWithCircuitBreaker
  def initialize(limiter)
    @limiter = limiter
    @circuit_breaker = CircuitBreaker.new(
      failure_threshold: 5,
      timeout: 30
    )
  end

  def allow_request?
    @circuit_breaker.call do
      @limiter.allow_request?
    end
  rescue CircuitBreakerOpen
    # Fail open: allow request
    { allowed: true, remaining: -1, degraded: true }
  end
end
```

## Failsafe & Rollback Strategy

### Reconciliation Job

```ruby
class RateLimitReconciliationJob
  # Runs every 5 minutes
  def perform
    # Clean up expired keys (Redis didn't auto-expire)
    cleanup_expired_keys

    # Verify counts match across replicas
    verify_replica_consistency

    # Alert on anomalies
    detect_anomalies
  end

  private

  def cleanup_expired_keys
    cursor = "0"
    loop do
      cursor, keys = redis.scan(cursor, match: "ratelimit:*", count: 1000)

      keys.each do |key|
        ttl = redis.ttl(key)
        redis.del(key) if ttl == -1  # No expiry set
      end

      break if cursor == "0"
    end
  end

  def verify_replica_consistency
    # Sample random keys and compare across replicas
    sample_keys = redis.randomkey(100)

    sample_keys.each do |key|
      primary_count = redis_primary.zcard(key)
      replica_count = redis_replica.zcard(key)

      if (primary_count - replica_count).abs > 5
        Rails.logger.warn(
          "Replica inconsistency: #{key} " \
          "primary=#{primary_count} replica=#{replica_count}"
        )
      end
    end
  end
end
```

## Zero Downtime Deployment

### Rolling Update Strategy

```ruby
# Deploy script
# 1. Update rate limit configs in database
# 2. Wait for cache TTL to expire (1 minute)
# 3. Deploy new code with rolling update
# 4. Monitor error rates

# Feature flag for new algorithm
class RateLimiterFactory
  def self.create(config, identifier)
    if FeatureFlag.enabled?(:new_rate_limit_algorithm)
      NewSlidingWindowRateLimiter.new(...)
    else
      SlidingWindowRateLimiter.new(...)
    end
  end
end
```

## Observability & Monitoring

### Key Metrics

```ruby
class RateLimiterMetrics
  def self.record_check(identifier, allowed, latency_ms)
    StatsD.increment('rate_limiter.check',
      tags: ["allowed:#{allowed}"])

    StatsD.histogram('rate_limiter.latency', latency_ms)

    StatsD.gauge('rate_limiter.remaining',
      get_remaining(identifier),
      tags: ["identifier:#{identifier}"])
  end

  def self.record_violation(identifier, endpoint)
    StatsD.increment('rate_limiter.violation',
      tags: ["identifier:#{identifier}", "endpoint:#{endpoint}"])
  end
end
```

### Alerting

```yaml
alerts:
  - name: HighRateLimitViolations
    condition: rate_limiter.violation > 1000/min
    duration: 5m
    severity: warning

  - name: RateLimiterHighLatency
    condition: p99(rate_limiter.latency) > 10ms
    duration: 2m
    severity: critical

  - name: RateLimiterRedisDown
    condition: rate_limiter.degraded > 0
    duration: 1m
    severity: critical
```

## Testing Strategy

### Unit Tests

```ruby
RSpec.describe SlidingWindowRateLimiter do
  let(:redis) { MockRedis.new }
  let(:limiter) { described_class.new(redis, 'user:123', 10, 60) }

  it 'allows requests within limit' do
    10.times do
      result = limiter.allow_request?
      expect(result[:allowed]).to be true
    end
  end

  it 'denies requests exceeding limit' do
    10.times { limiter.allow_request? }

    result = limiter.allow_request?
    expect(result[:allowed]).to be false
    expect(result[:remaining]).to eq(0)
  end

  it 'resets after window expires' do
    10.times { limiter.allow_request? }

    # Simulate time passing
    Timecop.travel(61.seconds.from_now) do
      result = limiter.allow_request?
      expect(result[:allowed]).to be true
    end
  end
end
```

### Load Tests

```ruby
# Simulate 1M RPS
# k6 load test
import http from 'k6/http';

export let options = {
  scenarios: {
    constant_load: {
      executor: 'constant-arrival-rate',
      rate: 1000000,  // 1M RPS
      timeUnit: '1s',
      duration: '1m',
      preAllocatedVUs: 10000,
    },
  },
};

export default function () {
  http.get('https://api.example.com/test', {
    headers: { 'X-API-Key': `key_${__VU}` },
  });
}
```

## Trade-offs & Alternatives

### Chosen: Sliding Window

**Pros:**
- Accurate rate limiting
- No burst at window boundaries
- Fair distribution

**Cons:**
- Higher memory usage (sorted sets)
- More complex implementation
- Slower than fixed window

**Alternative: Fixed Window**

**Pros:**
- Simple implementation (single counter)
- Low memory usage
- Fast (O(1) operations)

**Cons:**
- Allows 2x burst at boundaries
- Less accurate

**Decision:** Sliding window for accuracy, fixed window for high-throughput endpoints

---

### Chosen: Fail Open

**Pros:**
- Better user experience
- Prevents cascading failures
- Availability over consistency

**Cons:**
- Temporary over-limit allowed
- Potential abuse during outages

**Alternative: Fail Closed**

**Pros:**
- Strict enforcement
- Prevents abuse

**Cons:**
- Poor availability
- Cascading failures

**Decision:** Fail open with monitoring and alerts

---

### Cost Considerations

**Infrastructure:**
- Redis Cluster: $2000/month (5 regions)
- PostgreSQL: $500/month
- API Servers: $5000/month

**Total:** ~$7500/month for 1M RPS capacity
**Cost per million requests:** $0.36
