# Content Delivery Network (CDN)

## Problem Statement

Design a global Content Delivery Network that serves static and dynamic content with low latency to users worldwide, handling cache invalidation, origin failover, and DDoS protection.

**Scale Requirements:**
- 10 million requests per second globally
- 100+ edge locations worldwide
- 10 PB of cached content
- 99.99% cache hit rate target
- Sub-50ms latency for 95% of requests
- Support for 100 TB/day of new content

**Business Constraints:**
- Minimize origin server load (< 1% of total requests)
- Support instant cache purging
- Handle traffic spikes (10x normal load)
- Provide real-time analytics
- Support custom SSL certificates
- Geographic content restrictions
- Cost optimization (bandwidth, storage)

**Failure Expectations:**
- Origin server failures must not cause downtime
- Edge server failures must be transparent
- Network partitions must not affect availability
- DDoS attacks must be mitigated

**Edge Cases:**
- Cache stampede on popular content
- Stale content serving during origin outage
- Cache invalidation propagation delays
- Large file uploads and downloads
- Streaming video with adaptive bitrate
- WebSocket connections

## Functional Requirements

- Serve static assets (images, CSS, JS, videos)
- Serve dynamic content with edge caching
- Support cache invalidation (purge, refresh)
- Provide DDoS protection
- Support custom SSL/TLS certificates
- Enable geographic restrictions
- Provide real-time analytics
- Support HTTP/2 and HTTP/3
- Enable compression (gzip, brotli)
- Support range requests for large files
- Provide origin failover
- Enable A/B testing at edge

## Non-Functional Requirements

- **Availability:** 99.99%
- **Latency:** P95 < 50ms, P99 < 100ms
- **Throughput:** 10M RPS globally
- **Cache Hit Rate:** > 99%
- **Consistency:** Eventual consistency for cache invalidation
- **Scalability:** Linear scaling with edge locations
- **Security:** DDoS protection, WAF, SSL/TLS

## Core Engineering Challenges

1. **Cache Coherence**
   - Invalidating content across 100+ edge locations
   - Handling stale content
   - Cache stampede prevention
   - Versioning strategy

2. **Origin Shield**
   - Reducing origin load
   - Handling origin failures
   - Request coalescing
   - Failover logic

3. **Geographic Routing**
   - Latency-based routing
   - Anycast DNS
   - Health-based routing
   - Load balancing

4. **Large File Handling**
   - Chunked transfer
   - Range requests
   - Partial content caching
   - Bandwidth optimization

5. **DDoS Mitigation**
   - Rate limiting at edge
   - Traffic pattern analysis
   - Automatic blocking
   - Challenge-response

6. **Cache Eviction**
   - LRU vs LFU
   - Size-based eviction
   - TTL management
   - Hot content retention

## High-Level Design (HLD)

### System Architecture Overview

The CDN uses a **multi-tier caching architecture** with the following key components:

1. **Edge Servers** - Distributed globally (100+ locations) for low-latency content delivery
2. **Origin Shield** - Mid-tier cache layer to reduce origin load
3. **Origin Servers** - Source of truth for content
4. **Control Plane** - Manages cache invalidation, configuration, and routing
5. **Analytics Pipeline** - Real-time metrics and logging
6. **DDoS Protection Layer** - Rate limiting and traffic filtering at edge

### Architecture Diagram

```
                              Users (Global)
                                    │
                                    ▼
                              DNS (Anycast)
                              GeoDNS Routing
                                    │
        ┌───────────────────────────┼───────────────────────────┐
        ▼                           ▼                           ▼
    Edge Location 1          Edge Location 2          Edge Location 3
    (US-East)                (EU-West)                (AP-South)
        │                           │                           │
        ▼                           ▼                           ▼
    Edge Cache                  Edge Cache                  Edge Cache
    (Nginx/Varnish)            (Nginx/Varnish)            (Nginx/Varnish)
    - L1 Cache (RAM)           - L1 Cache (RAM)           - L1 Cache (RAM)
    - L2 Cache (SSD)           - L2 Cache (SSD)           - L2 Cache (SSD)
        │                           │                           │
        └───────────────────────────┼───────────────────────────┘
                                    │
                                    ▼
                            Regional Shield
                            (Cache Aggregation)
                                    │
                    ┌───────────────┼───────────────┐
                    ▼               ▼               ▼
              Origin 1        Origin 2        Origin 3
              (Primary)       (Backup)        (Backup)
                    │               │               │
                    └───────────────┼───────────────┘
                                    │
                                    ▼
                            Object Storage
                            (S3/GCS)
```

### Component Responsibilities

**1. DNS (Anycast):**
- Route users to nearest edge location based on latency
- Health-based routing (exclude unhealthy edges)
- Geographic restrictions enforcement
- Load balancing across edge locations

**2. Edge Servers:**
- L1 cache (RAM): Hot content (10-100 GB)
- L2 cache (SSD): Warm content (1-10 TB)
- Request validation and sanitization
- DDoS protection (rate limiting, challenge-response)
- SSL/TLS termination
- Compression (gzip, brotli)
- HTTP/2 and HTTP/3 support

**3. Origin Shield:**
- Mid-tier cache layer (regional)
- Request coalescing (collapse multiple requests for same content)
- Reduce origin load by 90-99%
- Cache popular content longer
- Handle cache stampede

**4. Origin Servers:**
- Source of truth for content
- Generate dynamic content
- Handle cache misses
- Provide content metadata (TTL, cache-control headers)
- Multi-region deployment for redundancy

**5. Control Plane:**
- Cache invalidation (purge, refresh)
- Configuration management
- SSL certificate management
- Analytics and monitoring
- A/B testing configuration

**6. Analytics Pipeline:**
- Real-time request logging
- Cache hit/miss metrics
- Bandwidth usage tracking
- Error rate monitoring
- Geographic distribution analysis

### Data Flow

```
1. Cache Hit (Edge)
   User → DNS (Anycast) → Edge Server
   → Check L1 cache (RAM) → HIT
   → Return content (< 10ms)

2. Cache Hit (Shield)
   User → DNS → Edge Server
   → Check L1 cache → MISS
   → Check L2 cache (SSD) → MISS
   → Origin Shield → HIT
   → Store in Edge L2 cache
   → Return content (< 50ms)

3. Cache Miss (Origin)
   User → DNS → Edge Server
   → Check L1/L2 cache → MISS
   → Origin Shield → MISS
   → Origin Server → Fetch content
   → Store in Shield cache
   → Store in Edge L2 cache
   → Return content (< 200ms)

4. Cache Invalidation
   Control Plane → Publish invalidation event
   → All Edge Servers subscribe
   → Remove content from L1/L2 cache
   → Next request fetches fresh content

5. DDoS Protection
   User → Edge Server
   → Rate limit check (per IP)
   → If exceeded: Challenge-response (CAPTCHA)
   → If failed: Block IP (1 hour)
   → If passed: Allow request
```

### Scalability Strategy

**Horizontal Scaling:**
- Edge Servers: 100+ locations, 10-50 servers per location
- Origin Shield: 10-20 regional shields
- Origin Servers: Auto-scale based on cache miss rate
- Control Plane: Distributed across regions

**Vertical Scaling:**
- Edge Servers: c6g.2xlarge (8 vCPU, 16 GB RAM, 1 TB SSD)
- Origin Shield: r6g.4xlarge (16 vCPU, 128 GB RAM, 10 TB SSD)
- Origin Servers: c6g.xlarge (4 vCPU, 8 GB RAM)

**Partitioning:**
- Content: Shard by URL hash across edge servers
- Logs: Partition by date and edge location
- Analytics: Time-series database (ClickHouse)

**Caching:**
- L1 (RAM): 10-100 GB, LRU eviction, < 1ms latency
- L2 (SSD): 1-10 TB, LFU eviction, < 10ms latency
- Shield: 10-100 TB, TTL-based eviction, < 50ms latency

### Failure Handling

**Edge Server Failure:**
- DNS health checks (every 10 seconds)
- Remove unhealthy edge from DNS rotation
- Users automatically routed to next nearest edge
- RTO: < 30 seconds, RPO: 0 (stateless)

**Origin Shield Failure:**
- Bypass shield, fetch directly from origin
- Automatic failover to backup shield
- Increased origin load temporarily
- RTO: < 10 seconds, RPO: 0

**Origin Server Failure:**
- Serve stale content from cache (stale-while-revalidate)
- Automatic failover to backup origin
- Alert operations team
- RTO: < 30 seconds, RPO: 0

**Cache Stampede:**
- Request coalescing at origin shield
- Only one request to origin for same content
- Other requests wait for first response
- Distribute cached content to all waiting requests

**DDoS Attack:**
- Rate limiting at edge (per IP, per URL)
- Challenge-response for suspicious traffic
- Automatic IP blocking (temporary)
- Traffic pattern analysis (ML-based)
- Anycast absorption (distribute attack across edges)

## Low-Level Design (LLD)

### Class Diagram

```
┌─────────────────────────────┐
│   EdgeServer                │
├─────────────────────────────┤
│ - l1_cache: RAMCache        │
│ - l2_cache: SSDCache        │
│ - origin_shield: Shield     │
├─────────────────────────────┤
│ + handle_request(req)       │
│ - check_cache(url)          │
│ - fetch_from_shield(url)    │
│ - store_in_cache(url, data) │
└─────────────────────────────┘
            │
            │ uses
            ▼
┌─────────────────────────────┐
│   CacheManager              │
├─────────────────────────────┤
│ - l1: RAMCache              │
│ - l2: SSDCache              │
│ - eviction_policy: Policy   │
├─────────────────────────────┤
│ + get(key)                  │
│ + set(key, value, ttl)      │
│ + delete(key)               │
│ + evict()                   │
└─────────────────────────────┘
            │
            │ uses
            ▼
┌─────────────────────────────┐
│   OriginShield              │
├─────────────────────────────┤
│ - cache: Cache              │
│ - origin: OriginClient      │
│ - coalescer: RequestCoal    │
├─────────────────────────────┤
│ + fetch(url)                │
│ - coalesce_requests(url)    │
│ - fetch_from_origin(url)    │
└─────────────────────────────┘

┌─────────────────────────────┐
│   DDoSProtection            │
├─────────────────────────────┤
│ - rate_limiter: RateLimiter │
│ - ip_blocker: IPBlocker     │
├─────────────────────────────┤
│ + check_request(req)        │
│ - is_rate_limited(ip)       │
│ - is_blocked(ip)            │
│ + block_ip(ip, duration)    │
└─────────────────────────────┘

┌─────────────────────────────┐
│   CacheInvalidator          │
├─────────────────────────────┤
│ + purge(url_pattern)        │
│ + refresh(url)              │
│ - publish_event(event)      │
└─────────────────────────────┘
```

### Database Schema Details

**Content Metadata Table:**
```sql
CREATE TABLE content_metadata (
    id BIGSERIAL PRIMARY KEY,
    url VARCHAR(2048) UNIQUE NOT NULL,
    content_type VARCHAR(100) NOT NULL,
    content_length BIGINT NOT NULL,
    etag VARCHAR(255),
    last_modified TIMESTAMP,
    cache_control VARCHAR(255),
    ttl INTEGER DEFAULT 3600, -- seconds
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_content_url ON content_metadata(url);
CREATE INDEX idx_content_updated ON content_metadata(updated_at DESC);
```

**Cache Invalidation Events Table:**
```sql
CREATE TABLE cache_invalidation_events (
    id BIGSERIAL PRIMARY KEY,
    url_pattern VARCHAR(2048) NOT NULL,
    invalidation_type VARCHAR(50) NOT NULL, -- PURGE, REFRESH
    status VARCHAR(50) NOT NULL, -- PENDING, IN_PROGRESS, COMPLETED
    edge_locations_count INTEGER,
    completed_locations_count INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT NOW(),
    completed_at TIMESTAMP
);

CREATE INDEX idx_invalidation_status ON cache_invalidation_events(status, created_at DESC);
```

**Request Logs Table (Time-Series):**
```sql
CREATE TABLE request_logs (
    timestamp TIMESTAMP NOT NULL,
    edge_location VARCHAR(50) NOT NULL,
    url VARCHAR(2048) NOT NULL,
    status_code INTEGER NOT NULL,
    cache_status VARCHAR(20) NOT NULL, -- HIT, MISS, STALE
    response_time_ms INTEGER NOT NULL,
    bytes_sent BIGINT NOT NULL,
    client_ip INET NOT NULL,
    user_agent TEXT,
    referer TEXT
) PARTITION BY RANGE (timestamp);

-- Daily partitions
CREATE TABLE request_logs_2024_01_15 PARTITION OF request_logs
    FOR VALUES FROM ('2024-01-15') TO ('2024-01-16');

CREATE INDEX idx_logs_timestamp ON request_logs(timestamp DESC);
CREATE INDEX idx_logs_url ON request_logs(url, timestamp DESC);
CREATE INDEX idx_logs_cache_status ON request_logs(cache_status, timestamp DESC);
```

### API Endpoints

**Content Delivery API:**

```ruby
# Fetch content (handled by edge server)
GET /images/logo.png
Headers:
  Accept-Encoding: gzip, br
  If-None-Match: "abc123"
  Range: bytes=0-1023

Response: 200 OK
Headers:
  Content-Type: image/png
  Content-Length: 50000
  Cache-Control: public, max-age=3600
  ETag: "abc123"
  X-Cache: HIT
  X-Edge-Location: us-east-1
  Age: 120

# Partial content (range request)
Response: 206 Partial Content
Headers:
  Content-Range: bytes 0-1023/50000
  Content-Length: 1024
```

**Cache Invalidation API:**

```ruby
# Purge content from all edges
POST /api/v1/cache/purge
{
  "url_pattern": "/images/*",
  "invalidation_type": "PURGE"  # or "REFRESH"
}

Response: 200 OK
{
  "invalidation_id": "inv_123456",
  "status": "IN_PROGRESS",
  "edge_locations_count": 120,
  "estimated_completion_time": "2024-01-16T12:05:00Z"
}

# Check invalidation status
GET /api/v1/cache/invalidation/:id

Response: 200 OK
{
  "invalidation_id": "inv_123456",
  "status": "COMPLETED",
  "completed_locations": 120,
  "total_locations": 120,
  "completed_at": "2024-01-16T12:04:30Z"
}
```

**Analytics API:**

```ruby
# Get cache statistics
GET /api/v1/analytics/cache?start_date=2024-01-15&end_date=2024-01-16

Response: 200 OK
{
  "cache_hit_rate": 99.2,
  "total_requests": 1000000000,
  "cache_hits": 992000000,
  "cache_misses": 8000000,
  "bandwidth_saved_gb": 45000,
  "avg_response_time_ms": 35
}
```

### Algorithms

**1. Two-Tier Cache Lookup:**

```ruby
class EdgeServer
  L1_CACHE_SIZE = 100.gigabytes  # RAM
  L2_CACHE_SIZE = 10.terabytes   # SSD

  def handle_request(url)
    # Check L1 cache (RAM)
    content = l1_cache.get(url)
    if content
      log_cache_hit('L1', url)
      return content
    end

    # Check L2 cache (SSD)
    content = l2_cache.get(url)
    if content
      log_cache_hit('L2', url)
      # Promote to L1 cache
      l1_cache.set(url, content, ttl: 3600)
      return content
    end

    # Cache miss, fetch from origin shield
    content = fetch_from_shield(url)

    # Store in both caches
    l2_cache.set(url, content, ttl: 86400)  # 24 hours
    l1_cache.set(url, content, ttl: 3600)   # 1 hour

    log_cache_miss(url)
    content
  end
end
```

**2. Request Coalescing (Cache Stampede Prevention):**

```ruby
class OriginShield
  def initialize
    @in_flight_requests = {}
    @mutex = Mutex.new
  end

  def fetch(url)
    # Check if request is already in flight
    promise = @mutex.synchronize do
      if @in_flight_requests[url]
        # Return existing promise
        @in_flight_requests[url]
      else
        # Create new promise
        promise = Concurrent::Promise.new do
          fetch_from_origin(url)
        end

        @in_flight_requests[url] = promise
        promise.execute
      end
    end

    # Wait for result
    result = promise.value

    # Clean up
    @mutex.synchronize do
      @in_flight_requests.delete(url)
    end

    result
  end

  private

  def fetch_from_origin(url)
    origin_client.get(url)
  end
end
```

**3. LRU Cache Eviction:**

```ruby
class LRUCache
  def initialize(max_size)
    @max_size = max_size
    @cache = {}
    @lru_list = []  # Most recently used at end
  end

  def get(key)
    return nil unless @cache.key?(key)

    # Move to end (most recently used)
    @lru_list.delete(key)
    @lru_list.push(key)

    @cache[key]
  end

  def set(key, value, ttl:)
    # Evict if at capacity
    if @cache.size >= @max_size && !@cache.key?(key)
      evict_lru
    end

    # Update cache
    @cache[key] = { value: value, expires_at: Time.current + ttl }

    # Update LRU list
    @lru_list.delete(key)
    @lru_list.push(key)
  end

  private

  def evict_lru
    # Remove least recently used
    lru_key = @lru_list.shift
    @cache.delete(lru_key)
  end
end
```

**4. Cache Invalidation with Pub/Sub:**

```ruby
class CacheInvalidator
  def purge(url_pattern)
    # Create invalidation event
    event = CacheInvalidationEvent.create!(
      url_pattern: url_pattern,
      invalidation_type: 'PURGE',
      status: 'PENDING',
      edge_locations_count: EdgeLocation.count
    )

    # Publish to all edge servers
    redis.publish('cache:invalidation', {
      event_id: event.id,
      url_pattern: url_pattern,
      type: 'PURGE'
    }.to_json)

    event
  end
end

class EdgeServer
  def subscribe_to_invalidations
    redis.subscribe('cache:invalidation') do |on|
      on.message do |channel, message|
        data = JSON.parse(message)

        # Purge matching URLs from cache
        purge_pattern(data['url_pattern'])

        # Acknowledge completion
        acknowledge_invalidation(data['event_id'])
      end
    end
  end

  private

  def purge_pattern(pattern)
    # Convert glob pattern to regex
    regex = Regexp.new(pattern.gsub('*', '.*'))

    # Remove matching keys from L1 and L2 cache
    l1_cache.keys.each do |key|
      l1_cache.delete(key) if key.match?(regex)
    end

    l2_cache.keys.each do |key|
      l2_cache.delete(key) if key.match?(regex)
    end
  end
end
```

**5. Stale-While-Revalidate:**

```ruby
class EdgeServer
  def handle_request_with_swr(url)
    content = l1_cache.get(url)

    if content
      # Check if content is stale
      if content[:expires_at] < Time.current
        # Serve stale content
        # Async revalidate in background
        RevalidateJob.perform_later(url)
      end

      return content[:value]
    end

    # Cache miss, fetch from origin
    fetch_from_shield(url)
  end
end

class RevalidateJob < ApplicationJob
  def perform(url)
    # Fetch fresh content from origin
    fresh_content = origin_shield.fetch(url)

    # Update cache
    edge_server.l1_cache.set(url, fresh_content, ttl: 3600)
    edge_server.l2_cache.set(url, fresh_content, ttl: 86400)
  end
end
```

**6. DDoS Rate Limiting:**

```ruby
class DDoSProtection
  RATE_LIMIT = 100  # requests per minute
  BLOCK_DURATION = 3600  # 1 hour

  def check_request(ip_address, url)
    key = "rate_limit:#{ip_address}"

    # Increment request count
    count = redis.incr(key)
    redis.expire(key, 60) if count == 1

    if count > RATE_LIMIT
      # Check if already blocked
      if redis.exists("blocked:#{ip_address}")
        return { allowed: false, reason: 'IP_BLOCKED' }
      end

      # Block IP
      redis.setex("blocked:#{ip_address}", BLOCK_DURATION, '1')

      return { allowed: false, reason: 'RATE_LIMIT_EXCEEDED' }
    end

    { allowed: true }
  end
end
```

### Sequence Diagrams

**Cache Hit Flow:**

```
User   DNS   Edge   L1   L2
 │      │      │     │    │
 │─Req──>│      │     │    │
 │      │      │     │    │
 │<─IP──│      │     │    │
 │      │      │     │    │
 │─GET──────────>│    │    │
 │      │      │     │    │
 │      │      │─Get─>│   │
 │      │      │<─HIT─│   │
 │      │      │     │    │
 │<─200 OK─────│     │    │
 │  (< 10ms)   │     │    │
```

**Cache Miss Flow:**

```
User   Edge   Shield   Origin
 │      │       │        │
 │─GET──>│       │        │
 │      │       │        │
 │      │─Miss──│        │
 │      │       │        │
 │      │───Fetch──>│     │
 │      │       │        │
 │      │       │─Coalesce>│
 │      │       │<─Content─│
 │      │       │        │
 │      │<──Content───────│
 │      │       │        │
 │      │─Store in L2    │
 │      │       │        │
 │<─200 OK     │        │
 │  (< 200ms)  │        │
```

**Cache Invalidation Flow:**

```
Admin   Control   Redis   Edge1   Edge2
 │        │        │       │       │
 │─Purge──>│        │       │       │
 │        │        │       │       │
 │        │─Publish────────>│       │
 │        │        │       │       │
 │        │        │───────────────>│
 │        │        │       │       │
 │        │        │       │─Purge─│
 │        │        │       │       │
 │        │        │       │       │─Purge
 │        │        │       │       │
 │        │        │       │─ACK───>│
 │        │        │       │       │
 │        │        │       │       │─ACK──>│
 │        │        │<───────────────────────│
 │        │        │       │       │
 │<─200 OK│        │       │       │
```

### Performance Optimizations

**1. HTTP/2 Server Push:**
```ruby
# Push critical resources before client requests them
class EdgeServer
  def handle_html_request(url)
    html = fetch_content(url)

    # Parse HTML for critical resources
    critical_resources = parse_critical_resources(html)

    # Push resources to client
    critical_resources.each do |resource_url|
      push_resource(resource_url)
    end

    html
  end
end
```

**2. Brotli Compression:**
```ruby
# Compress content at edge
class EdgeServer
  def compress_content(content, accept_encoding)
    if accept_encoding.include?('br')
      # Brotli compression (better than gzip)
      Brotli.deflate(content, quality: 11)
    elsif accept_encoding.include?('gzip')
      # Fallback to gzip
      Zlib::Deflate.deflate(content)
    else
      content
    end
  end
end
```

**3. Adaptive TTL:**
```ruby
# Adjust TTL based on content popularity
class EdgeServer
  def calculate_ttl(url)
    # Get request count for URL
    request_count = redis.get("request_count:#{url}").to_i

    case request_count
    when 0..100
      3600      # 1 hour for unpopular content
    when 101..1000
      7200      # 2 hours for moderately popular
    when 1001..10000
      14400     # 4 hours for popular
    else
      86400     # 24 hours for very popular
    end
  end
end
```

**4. Prefetching:**
```ruby
# Prefetch content based on access patterns
class ContentPrefetcher
  def prefetch_related_content(url)
    # Analyze access patterns
    related_urls = analyze_access_patterns(url)

    # Prefetch in background
    related_urls.each do |related_url|
      PrefetchJob.perform_later(related_url)
    end
  end
end
```

**5. Connection Pooling:**
```ruby
# Reuse connections to origin
ORIGIN_POOL = ConnectionPool.new(size: 100, timeout: 5) do
  HTTP.persistent(ENV['ORIGIN_URL'])
end

def fetch_from_origin(url)
  ORIGIN_POOL.with do |http|
    http.get(url)
  end
end
```

## Step-by-Step Request Flow

### Cache Hit Flow

1. **User requests content**
   ```
   GET https://cdn.example.com/images/logo.png
   ```

2. **DNS resolution**
   - GeoDNS returns nearest edge location IP
   - Based on user's geographic location
   - Health-checked edge servers only

3. **Edge cache lookup**
   ```nginx
   # Nginx cache lookup
   location / {
       proxy_cache edge_cache;
       proxy_cache_key "$scheme$request_method$host$request_uri";
       proxy_cache_valid 200 1h;
       proxy_cache_valid 404 1m;

       add_header X-Cache-Status $upstream_cache_status;
   }
   ```

4. **Cache HIT**
   - Content served from RAM (L1) or SSD (L2)
   - Response time: < 10ms
   - Headers: `X-Cache-Status: HIT`

### Cache Miss Flow

1. **Cache MISS at edge**
   - Edge cache doesn't have content
   - Headers: `X-Cache-Status: MISS`

2. **Check regional shield**
   ```
   Edge → Regional Shield
   ```
   - Regional shield may have content
   - Reduces origin load

3. **Shield MISS → Origin request**
   ```
   Regional Shield → Origin Server
   ```
   - Request coalescing: Multiple edge requests → Single origin request
   - Origin returns content

4. **Cache at shield and edge**
   ```
   Origin → Shield (cache) → Edge (cache) → User
   ```

5. **Subsequent requests**
   - Served from edge cache
   - Cache HIT

### Cache Invalidation Flow

1. **Purge request**
   ```
   POST /api/v1/purge
   {
     "urls": ["/images/logo.png"],
     "type": "instant"
   }
   ```

2. **Publish to invalidation queue**
   ```ruby
   CacheInvalidationQueue.publish({
     urls: ['/images/logo.png'],
     timestamp: Time.current.to_i
   })
   ```

3. **Edge locations consume invalidation**
   ```ruby
   # Each edge location
   invalidation = CacheInvalidationQueue.consume

   invalidation['urls'].each do |url|
     # Purge from cache
     cache.delete(cache_key_for(url))
   end
   ```

4. **Propagation time**
   - Target: < 5 seconds globally
   - Eventual consistency

## Data Model Design

### Cache Key Structure

```
# Cache key format
{scheme}:{method}:{host}:{path}:{query}:{vary_headers}

Examples:
https:GET:cdn.example.com:/images/logo.png::
https:GET:api.example.com:/users/123:?format=json:accept-encoding=gzip
```

### Cache Metadata (Redis)

```
# Cache entry metadata
cache:metadata:{cache_key} → HASH
  - url: original URL
  - origin: origin server
  - size: content size in bytes
  - created_at: cache creation timestamp
  - ttl: time to live
  - hit_count: number of cache hits
  - last_accessed: last access timestamp
```

### Analytics Data (ClickHouse)

```sql
-- Request logs
CREATE TABLE request_logs (
    timestamp DateTime,
    edge_location String,
    client_ip String,
    request_method String,
    request_url String,
    response_status UInt16,
    response_size UInt64,
    cache_status String,  -- HIT, MISS, STALE, BYPASS
    response_time_ms UInt32,
    origin_time_ms UInt32,
    user_agent String,
    referer String
) ENGINE = MergeTree()
PARTITION BY toYYYYMM(timestamp)
ORDER BY (timestamp, edge_location);
```

## Concurrency & Consistency Strategy

### Request Coalescing (Thundering Herd Prevention)

```ruby
class RequestCoalescer
  def fetch_with_coalescing(cache_key, &block)
    # Check if request already in flight
    lock_key = "fetch_lock:#{cache_key}"

    # Try to acquire lock
    lock_acquired = redis.set(lock_key, worker_id, nx: true, ex: 30)

    if lock_acquired
      # We're the first request, fetch from origin
      begin
        content = block.call

        # Store in cache
        cache.set(cache_key, content)

        # Notify waiting requests
        redis.publish("fetch_complete:#{cache_key}", content)

        content
      ensure
        redis.del(lock_key)
      end
    else
      # Another request is fetching, wait for result
      wait_for_fetch_completion(cache_key)
    end
  end

  private

  def wait_for_fetch_completion(cache_key, timeout: 30)
    start_time = Time.current

    # Subscribe to completion notification
    redis.subscribe("fetch_complete:#{cache_key}") do |on|
      on.message do |channel, content|
        return content
      end
    end

    # Timeout fallback
    if Time.current - start_time > timeout
      # Fetch from origin ourselves
      fetch_from_origin(cache_key)
    end
  end
end
```

### Stale-While-Revalidate

```nginx
# Nginx configuration
location / {
    proxy_cache edge_cache;
    proxy_cache_valid 200 1h;

    # Serve stale content while revalidating
    proxy_cache_use_stale error timeout updating http_500 http_502 http_503 http_504;
    proxy_cache_background_update on;

    # Revalidate in background
    proxy_cache_revalidate on;
}
```

## Ruby Implementation Examples

### CDN Edge Server (Simplified)

```ruby
class CDNEdgeServer
  def initialize
    @cache = CacheStore.new
    @origin = OriginClient.new
    @coalescer = RequestCoalescer.new
  end

  def handle_request(request)
    cache_key = generate_cache_key(request)

    # Check cache
    cached_content = @cache.get(cache_key)

    if cached_content
      # Cache HIT
      record_metrics('HIT', request)
      return build_response(cached_content, cache_status: 'HIT')
    end

    # Cache MISS - fetch from origin with coalescing
    content = @coalescer.fetch_with_coalescing(cache_key) do
      fetch_from_origin(request)
    end

    record_metrics('MISS', request)
    build_response(content, cache_status: 'MISS')
  end

  private

  def generate_cache_key(request)
    # Include vary headers in cache key
    vary_headers = extract_vary_headers(request)

    "#{request.scheme}:#{request.method}:#{request.host}:#{request.path}:#{request.query}:#{vary_headers}"
  end

  def fetch_from_origin(request)
    # Try regional shield first
    content = fetch_from_shield(request)
    return content if content

    # Shield miss - fetch from origin
    @origin.fetch(request.url)
  end

  def fetch_from_shield(request)
    shield_url = "http://shield.#{region}.example.com#{request.path}"

    begin
      HTTP.get(shield_url, timeout: 5)
    rescue HTTP::TimeoutError
      nil
    end
  end
end
```

### Cache Invalidation Service

```ruby
class CacheInvalidationService
  def purge(urls, type: 'instant')
    case type
    when 'instant'
      purge_instant(urls)
    when 'lazy'
      purge_lazy(urls)
    when 'soft'
      soft_purge(urls)
    end
  end

  private

  def purge_instant(urls)
    # Publish to all edge locations
    invalidation_message = {
      type: 'purge',
      urls: urls,
      timestamp: Time.current.to_i
    }

    # Publish to message queue
    EDGE_LOCATIONS.each do |location|
      CacheInvalidationQueue.publish(
        invalidation_message,
        routing_key: "edge.#{location}"
      )
    end

    # Wait for acknowledgments
    wait_for_purge_completion(urls)
  end

  def purge_lazy(urls)
    # Set TTL to 0, let natural expiration handle it
    urls.each do |url|
      cache_key = generate_cache_key(url)
      redis.expire("cache:#{cache_key}", 0)
    end
  end

  def soft_purge(urls)
    # Mark as stale, serve stale while revalidating
    urls.each do |url|
      cache_key = generate_cache_key(url)
      redis.hset("cache:metadata:#{cache_key}", 'stale', '1')
    end
  end

  def wait_for_purge_completion(urls, timeout: 10)
    start_time = Time.current

    loop do
      # Check if all edges acknowledged
      acks = redis.scard("purge_acks:#{urls.hash}")

      if acks >= EDGE_LOCATIONS.size
        return true
      elsif Time.current - start_time > timeout
        Rails.logger.warn("Purge timeout for #{urls}")
        return false
      end

      sleep 0.1
    end
  end
end
```

### Origin Shield

```ruby
class OriginShield
  def initialize
    @cache = CacheStore.new(size: '100GB')
    @origin_pool = OriginConnectionPool.new(size: 100)
  end

  def fetch(url)
    cache_key = generate_cache_key(url)

    # Check shield cache
    cached = @cache.get(cache_key)
    return cached if cached

    # Fetch from origin with connection pooling
    @origin_pool.with do |origin_client|
      content = origin_client.get(url)

      # Cache at shield
      @cache.set(cache_key, content, ttl: 1.hour)

      content
    end
  rescue OriginError => e
    # Origin failure - serve stale if available
    serve_stale_or_error(cache_key, e)
  end

  private

  def serve_stale_or_error(cache_key, error)
    stale_content = @cache.get_stale(cache_key)

    if stale_content
      Rails.logger.warn("Serving stale content due to origin error: #{error.message}")
      stale_content
    else
      raise error
    end
  end
end
```

### DDoS Protection

```ruby
class DDoSProtection
  RATE_LIMIT = 100  # requests per second per IP

  def check_request(request)
    client_ip = request.ip

    # Rate limiting
    if rate_limit_exceeded?(client_ip)
      return { allowed: false, reason: 'rate_limit' }
    end

    # Challenge-response for suspicious traffic
    if suspicious_traffic?(request)
      return { allowed: false, reason: 'challenge_required' }
    end

    # Pattern-based blocking
    if matches_attack_pattern?(request)
      return { allowed: false, reason: 'blocked' }
    end

    { allowed: true }
  end

  private

  def rate_limit_exceeded?(client_ip)
    key = "rate_limit:#{client_ip}"

    count = redis.incr(key)
    redis.expire(key, 1) if count == 1

    count > RATE_LIMIT
  end

  def suspicious_traffic?(request)
    # Check for bot-like behavior
    user_agent = request.headers['User-Agent']

    # No user agent
    return true if user_agent.blank?

    # Known bot patterns
    return true if user_agent =~ /bot|crawler|spider/i

    # Unusual request patterns
    request_rate = get_request_rate(request.ip)
    return true if request_rate > 1000  # 1000 req/sec

    false
  end

  def matches_attack_pattern?(request)
    # SQL injection patterns
    return true if request.query_string =~ /union.*select|drop.*table/i

    # XSS patterns
    return true if request.query_string =~ /<script|javascript:/i

    # Path traversal
    return true if request.path =~ /\.\.\//

    false
  end
end
```

### Adaptive Bitrate Streaming

```ruby
class AdaptiveBitrateStreaming
  BITRATES = [
    { quality: '1080p', bitrate: 5_000_000 },
    { quality: '720p', bitrate: 2_500_000 },
    { quality: '480p', bitrate: 1_000_000 },
    { quality: '360p', bitrate: 500_000 }
  ].freeze

  def generate_manifest(video_id, client_bandwidth)
    video = Video.find(video_id)

    # Select appropriate bitrates based on client bandwidth
    suitable_bitrates = BITRATES.select do |br|
      br[:bitrate] <= client_bandwidth * 0.8  # 80% of bandwidth
    end

    # Generate HLS manifest
    generate_hls_manifest(video, suitable_bitrates)
  end

  private

  def generate_hls_manifest(video, bitrates)
    manifest = "#EXTM3U\n"
    manifest += "#EXT-X-VERSION:3\n"

    bitrates.each do |br|
      manifest += "#EXT-X-STREAM-INF:BANDWIDTH=#{br[:bitrate]},RESOLUTION=#{br[:quality]}\n"
      manifest += "#{video.id}/#{br[:quality]}/playlist.m3u8\n"
    end

    manifest
  end
end
```

## Scaling Strategy

### Horizontal Scaling

**Edge Locations:**
- Add new edge locations based on traffic patterns
- Each location: 10-100 servers
- Auto-scale within location based on load

**Origin Servers:**
- Auto-scale based on cache miss rate
- Minimum: 10 servers
- Maximum: 100 servers

### Vertical Scaling

**Edge Servers:**
- Instance type: c6g.4xlarge (16 vCPU, 32 GB RAM)
- Reason: CPU-intensive (compression, SSL)
- SSD: 1 TB NVMe for L2 cache

### Geographic Expansion

```ruby
# Add new edge location
class EdgeLocationProvisioner
  def provision(region, capacity)
    # Deploy edge servers
    deploy_edge_servers(region, capacity)

    # Configure DNS
    add_to_geodns(region)

    # Warm cache
    warm_cache(region)

    # Enable traffic
    enable_traffic(region)
  end
end
```

## High Availability Strategy

### Multi-Origin Failover

```nginx
# Nginx upstream configuration
upstream origin_servers {
    server origin1.example.com:443 max_fails=3 fail_timeout=30s;
    server origin2.example.com:443 backup;
    server origin3.example.com:443 backup;
}

location / {
    proxy_pass https://origin_servers;
    proxy_next_upstream error timeout http_500 http_502 http_503;
}
```

### Edge Server Health Checks

```ruby
class EdgeHealthChecker
  def perform
    edge_servers = EdgeServer.all

    edge_servers.each do |server|
      health = check_health(server)

      if health[:healthy]
        # Add to DNS pool
        dns.add_record(server.ip)
      else
        # Remove from DNS pool
        dns.remove_record(server.ip)

        # Alert ops team
        alert_unhealthy_server(server)
      end
    end
  end

  private

  def check_health(server)
    response = HTTP.get("#{server.url}/health", timeout: 5)

    {
      healthy: response.status == 200,
      latency: response.time,
      cache_hit_rate: response.parse['cache_hit_rate']
    }
  rescue HTTP::TimeoutError
    { healthy: false }
  end
end
```

## Observability & Monitoring

### Key Metrics

```ruby
class CDNMetrics
  def self.record_request(request, response, cache_status)
    StatsD.increment('cdn.requests',
      tags: [
        "edge:#{edge_location}",
        "cache_status:#{cache_status}",
        "status:#{response.status}"
      ])

    StatsD.histogram('cdn.response_time', response.time,
      tags: ["edge:#{edge_location}"])

    StatsD.histogram('cdn.response_size', response.size,
      tags: ["content_type:#{response.content_type}"])

    if cache_status == 'MISS'
      StatsD.histogram('cdn.origin_time', response.origin_time)
    end
  end

  def self.record_cache_hit_rate(edge_location, hit_rate)
    StatsD.gauge('cdn.cache_hit_rate', hit_rate,
      tags: ["edge:#{edge_location}"])
  end
end
```

### Real-Time Analytics

```ruby
class CDNAnalytics
  def get_stats(time_range: 1.hour)
    {
      total_requests: count_requests(time_range),
      cache_hit_rate: calculate_hit_rate(time_range),
      bandwidth_used: calculate_bandwidth(time_range),
      top_content: get_top_content(time_range),
      geographic_distribution: get_geo_distribution(time_range),
      error_rate: calculate_error_rate(time_range)
    }
  end

  private

  def calculate_hit_rate(time_range)
    hits = redis.get("stats:hits:#{time_range}").to_i
    total = redis.get("stats:total:#{time_range}").to_i

    return 0 if total.zero?

    (hits.to_f / total * 100).round(2)
  end
end
```

### Alerting

```yaml
alerts:
  - name: LowCacheHitRate
    condition: cdn.cache_hit_rate < 95%
    duration: 10m
    severity: warning

  - name: HighOriginLoad
    condition: cdn.origin_requests > 1000/sec
    duration: 5m
    severity: critical

  - name: EdgeServerDown
    condition: edge.health_check_failed > 0
    duration: 1m
    severity: critical

  - name: DDoSAttack
    condition: cdn.requests > 100000/sec from single IP
    duration: 1m
    severity: critical
```

## Testing Strategy

### Load Testing

```ruby
# Simulate 10M RPS
# Using Apache JMeter or Gatling

class CDNLoadTest
  def run
    # Distribute load across edge locations
    edge_locations.each do |location|
      spawn_load_generator(location, rps: 100_000)
    end

    # Monitor metrics
    monitor_performance
  end
end
```

### Cache Invalidation Testing

```ruby
RSpec.describe CacheInvalidationService do
  it 'purges content from all edge locations' do
    urls = ['/images/logo.png']

    service.purge(urls, type: 'instant')

    # Verify purged from all edges
    EDGE_LOCATIONS.each do |location|
      cache = EdgeCache.new(location)
      expect(cache.get(urls.first)).to be_nil
    end
  end
end
```

## Trade-offs & Alternatives

### Chosen: Multi-Tier Caching

**Pros:**
- High cache hit rate
- Low origin load
- Fast response times

**Cons:**
- Complex invalidation
- Higher infrastructure cost

**Alternative: Single-Tier Edge Caching**

**Pros:**
- Simpler architecture
- Easier invalidation

**Cons:**
- Higher origin load
- Lower cache hit rate

**Decision:** Multi-tier for better performance

---

### Cost Considerations

**Infrastructure (per edge location):**
- Edge Servers: $5000/month (10 servers)
- Bandwidth: $0.05/GB
- Storage: $0.02/GB/month

**Total (100 locations):** ~$500K/month + bandwidth costs
**Cost per request:** $0.000005 (0.0005 cents)
