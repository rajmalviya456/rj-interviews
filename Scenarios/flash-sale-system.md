# Flash Sale System

## Problem Statement

Design a flash sale system for an e-commerce platform that handles limited inventory drops (e.g., 1000 units of a product released at exactly 12:00 PM).

**Scale Requirements:**
- 10 million users attempting to purchase simultaneously
- Peak: 500,000 requests per second in first 10 seconds
- Inventory: 100-10,000 units per sale
- Sale duration: Typically sold out in 30-120 seconds
- Global user base across multiple regions

**Business Constraints:**
- No overselling (hard constraint)
- Fair ordering (first-come-first-served within technical limits)
- Prevent bot abuse
- Handle payment failures gracefully
- Support flash sale preview/countdown

**Failure Expectations:**
- System must degrade gracefully under extreme load
- No data loss on payment failures
- Inventory must remain consistent across all failures

**Edge Cases:**
- Payment gateway timeout after inventory reserved
- User abandons cart after reservation
- Concurrent purchases of last item
- Bot traffic detection
- Cache stampede at sale start time

## Functional Requirements

- User can view upcoming flash sales
- User can join waiting room before sale starts
- User can attempt to purchase when sale goes live
- System reserves inventory for limited time (5 minutes)
- System processes payment
- System releases inventory if payment fails or times out
- Admin can configure flash sale parameters
- System prevents duplicate purchases per user
- Real-time inventory counter for users

## Non-Functional Requirements

- **Availability:** 99.99% (52 minutes downtime/year)
- **Latency:**
  - P50: < 200ms for purchase attempt
  - P99: < 2s for purchase attempt
- **Throughput:** Handle 500K RPS peak
- **Consistency:** Strong consistency for inventory, eventual for analytics
- **Durability:** Zero inventory loss, payment idempotency
- **Security:** Bot detection, rate limiting per user, DDoS protection
- **Cost:** Optimize for burst capacity, scale down after sale

## Core Engineering Challenges

1. **Inventory Overselling Prevention**
   - Race condition: Multiple users purchasing last item simultaneously
   - Distributed counter consistency across multiple app servers
   - Database lock contention at high concurrency

2. **Thundering Herd Problem**
   - Millions of users hitting system at exact same millisecond
   - Cache stampede when sale goes live
   - Database connection pool exhaustion

3. **Payment-Inventory Consistency**
   - Payment succeeds but inventory commit fails
   - Payment fails but inventory already decremented
   - Payment gateway timeout scenarios

4. **Reservation Timeout Handling**
   - Releasing expired reservations back to available pool
   - Preventing reservation of already-reserved items
   - Clock skew across distributed systems

5. **Bot Traffic**
   - Distinguishing legitimate users from bots
   - Rate limiting without impacting real users
   - Distributed rate limiter consistency

6. **Fair Queuing**
   - Preventing queue jumping
   - Handling network latency differences
   - Time synchronization across regions

## High-Level Design (HLD)

### System Architecture Overview

The flash sale system uses a **multi-tier architecture** with the following key components:

1. **Waiting Room Layer** - Queue management to prevent thundering herd
2. **API Gateway** - Rate limiting and DDoS protection
3. **Application Layer** - Stateless flash sale services
4. **Caching Layer** - Redis for high-performance inventory operations
5. **Persistence Layer** - PostgreSQL for durable order storage
6. **Async Processing** - Message queue for payment processing

### Architecture Diagram

```
                                    Users (10M concurrent)
                                           │
                                           ▼
                                    CDN (Static Assets)
                                           │
                                           ▼
                              DDoS Protection (Cloudflare)
                                           │
                                           ▼
                                  API Gateway (Rate Limiting)
                                           │
                                           ▼
                                   Waiting Room Service
                                    (Queue Management)
                                           │
                                           ▼
                              Load Balancer (Geographic)
                                           │
                    ┌──────────────────────┼──────────────────────┐
                    ▼                      ▼                      ▼
            Flash Sale API          Flash Sale API          Flash Sale API
            (Stateless)              (Stateless)              (Stateless)
                    │                      │                      │
                    └──────────────────────┼──────────────────────┘
                                           │
                    ┌──────────────────────┼──────────────────────┐
                    ▼                      ▼                      ▼
              Redis Cluster          PostgreSQL              Message Queue
           (Inventory Counter)    (Source of Truth)          (Async Tasks)
           (Distributed Lock)     (Orders, Payments)              │
                                                                   ▼
                                                          Background Workers
                                                          - Payment Processing
                                                          - Reservation Expiry
                                                          - Inventory Release
```

### Component Responsibilities

**1. CDN & DDoS Protection:**
- Serve static countdown page
- Filter malicious traffic
- Reduce origin load by 90%
- Geographic distribution

**2. API Gateway:**
- Per-user rate limiting (10 req/sec)
- Bot detection and blocking
- Request authentication
- Load balancing

**3. Waiting Room Service:**
- Queue users before sale starts
- Release users in controlled batches (1000/sec)
- Provide queue position updates
- Generate time-limited access tokens

**4. Flash Sale API:**
- Inventory reservation logic
- Order creation
- Idempotency handling
- Integration with payment queue

**5. Redis Cluster:**
- Atomic inventory operations (DECR/INCR)
- Distributed locks
- Rate limiting counters
- Reservation TTL management

**6. PostgreSQL:**
- Source of truth for orders
- Payment records
- Flash sale configuration
- Audit trail

**7. Message Queue:**
- Async payment processing
- Inventory release events
- Order notifications
- Analytics events

**8. Background Workers:**
- Payment processing
- Reservation expiry
- Inventory reconciliation
- Dead letter queue handling

### Data Flow

```
1. Pre-Sale (T-5 minutes)
   User → CDN (Countdown Page)
   User → Waiting Room Service → Redis (Queue Position)

2. Sale Start (T-0)
   Waiting Room → Release Batch (1000 users/sec)
   → Generate Access Tokens (JWT, 30s TTL)
   → Notify Users (WebSocket)

3. Purchase Attempt
   User → API Gateway (Rate Limit Check)
   → Flash Sale API → Redis (Atomic DECR inventory)
   → PostgreSQL (INSERT order with idempotency key)
   → Message Queue (PUBLISH payment event)
   → User (Response: "Reserved!")

4. Payment Processing (Async)
   Worker → Message Queue (CONSUME)
   → Payment Gateway (Charge)
   → PostgreSQL (UPDATE order status=PAID)
   → User (Notification)

5. Failure Recovery
   Reconciliation Job → PostgreSQL (Find orphaned reservations)
   → Redis (INCR inventory)
   → PostgreSQL (UPDATE order status=EXPIRED)
```

### Scalability Strategy

**Horizontal Scaling:**
- API Servers: Auto-scale 10-500 instances based on CPU/queue depth
- Workers: Scale based on message queue depth
- Redis: Cluster mode with 3-6 shards
- PostgreSQL: Read replicas for analytics queries

**Vertical Scaling:**
- Redis: r6g.4xlarge (128 GB RAM) for millions of keys
- PostgreSQL: r6g.2xlarge (64 GB RAM) for connection pooling
- API Servers: c6g.2xlarge (8 vCPU) for CPU-intensive operations

**Pre-warming:**
- Spin up instances 10 minutes before sale
- Pre-load product data into cache
- Establish database connections
- Warm up JIT compiler

**Partitioning:**
- Orders table: Partition by created_at (monthly)
- Payments table: Partition by created_at (monthly)
- Redis: Shard by product_id

### Failure Handling

**Redis Failure:**
- Fallback to PostgreSQL for inventory (slower but functional)
- Return "degraded mode" warning to users
- Automatic failover to replica (30s RTO)

**PostgreSQL Failure:**
- Failover to read replica promoted to primary (60s RTO)
- Orders in Redis queue continue processing
- Temporary queue for new orders

**Payment Gateway Failure:**
- Circuit breaker opens after 5 failures
- Queue payments for retry
- Use backup payment gateway
- Notify users of delay

**API Server Failure:**
- Health checks every 5 seconds
- Remove unhealthy instances from load balancer
- Requests automatically routed to healthy instances
- No user impact (stateless design)

**Message Queue Failure:**
- Messages persist in queue (durable)
- Workers reconnect automatically
- Dead letter queue for failed messages
- Manual intervention for DLQ

## Low-Level Design (LLD)

### Class Diagram

```
┌─────────────────────────┐
│  FlashSaleController    │
├─────────────────────────┤
│ + purchase()            │
│ + check_inventory()     │
│ - validate_access()     │
└─────────────────────────┘
            │
            │ uses
            ▼
┌─────────────────────────┐
│   InventoryManager      │
├─────────────────────────┤
│ - redis: Redis          │
│ - product_id: UUID      │
├─────────────────────────┤
│ + reserve_for_user()    │
│ + release_for_user()    │
│ - check_duplicate()     │
└─────────────────────────┘
            │
            │ uses
            ▼
┌─────────────────────────┐
│     OrderService        │
├─────────────────────────┤
│ + create_order()        │
│ - validate_idempotency()│
│ - publish_payment()     │
└─────────────────────────┘

┌─────────────────────────┐
│   WaitingRoomService    │
├─────────────────────────┤
│ - redis: Redis          │
│ - sale_id: UUID         │
├─────────────────────────┤
│ + join(user_id)         │
│ + release_batch()       │
│ + get_position()        │
└─────────────────────────┘

┌─────────────────────────┐
│     PaymentWorker       │
├─────────────────────────┤
│ - circuit_breaker       │
├─────────────────────────┤
│ + perform()             │
│ - process_payment()     │
│ - handle_failure()      │
└─────────────────────────┘

┌─────────────────────────┐
│ ReservationExpiryJob    │
├─────────────────────────┤
│ + perform()             │
│ - expire_reservations() │
│ - release_inventory()   │
└─────────────────────────┘

┌─────────────────────────┐
│ InventoryReconciliation │
├─────────────────────────┤
│ + perform()             │
│ - compare_redis_db()    │
│ - correct_mismatch()    │
└─────────────────────────┘
```

### Database Schema Details

**Flash Sales Table:**
```sql
CREATE TABLE flash_sales (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    product_id UUID REFERENCES products(id),
    total_inventory INTEGER NOT NULL,
    available_inventory INTEGER NOT NULL,
    start_time TIMESTAMP NOT NULL,
    end_time TIMESTAMP NOT NULL,
    max_per_user INTEGER DEFAULT 1,
    status VARCHAR(50) NOT NULL, -- SCHEDULED, ACTIVE, COMPLETED, CANCELLED
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),

    CONSTRAINT positive_inventory CHECK (available_inventory >= 0),
    CONSTRAINT valid_time_range CHECK (end_time > start_time)
);

CREATE INDEX idx_flash_sales_start_time ON flash_sales(start_time);
CREATE INDEX idx_flash_sales_status ON flash_sales(status) WHERE status = 'ACTIVE';
```

**Orders State Machine:**
```
RESERVED → PAID → FULFILLED
    ↓         ↓
    ↓         └──→ REFUNDED
    ↓
    └──→ EXPIRED → (inventory released)

CANCELLED (can transition from RESERVED or PAID)
```

### API Endpoints

**Purchase API:**

```ruby
# Reserve inventory and create order
POST /api/v1/flash_sales/:sale_id/purchase
Headers:
  Authorization: Bearer <access_token>
  X-Idempotency-Key: <unique_key>

Request:
{
  "product_id": "uuid",
  "quantity": 1
}

Response: 201 Created
{
  "order_id": "uuid",
  "status": "reserved",
  "reservation_expires_at": "2024-01-16T12:05:00Z",
  "payment_url": "https://payment.example.com/...",
  "remaining_inventory": 42
}

Error Responses:
- 409 Conflict: Already reserved
- 410 Gone: Sold out
- 429 Too Many Requests: Rate limit exceeded
- 403 Forbidden: Invalid access token
```

**Waiting Room API:**

```ruby
# Join waiting room
POST /api/v1/flash_sales/:sale_id/waiting_room
Headers:
  Authorization: Bearer <user_token>

Response: 200 OK
{
  "position": 1523,
  "estimated_wait_seconds": 152,
  "websocket_url": "wss://waitingroom.example.com/..."
}

# Get queue position (polling)
GET /api/v1/flash_sales/:sale_id/waiting_room/position

Response: 200 OK
{
  "position": 1234,
  "estimated_wait_seconds": 123,
  "status": "waiting" | "ready" | "expired"
}
```

### Algorithms

**1. Atomic Inventory Reservation (Lua Script):**

```ruby
# Executed atomically in Redis
ATOMIC_RESERVE_SCRIPT = <<~LUA
  local inventory_key = KEYS[1]
  local reserved_key = KEYS[2]
  local reservation_key = KEYS[3]
  local user_id = ARGV[1]
  local ttl = tonumber(ARGV[2])

  -- Check if user already has reservation
  if redis.call('EXISTS', reservation_key) == 1 then
    return {err = 'ALREADY_RESERVED'}
  end

  -- Check inventory
  local inventory = tonumber(redis.call('GET', inventory_key) or 0)
  if inventory <= 0 then
    return {err = 'SOLD_OUT'}
  end

  -- Atomic reservation
  redis.call('DECR', inventory_key)
  redis.call('SADD', reserved_key, user_id)
  redis.call('SETEX', reservation_key, ttl, '1')

  return {ok = inventory - 1}
LUA

# Usage
def reserve_inventory(product_id, user_id, ttl: 300)
  keys = [
    "inventory:product:#{product_id}",
    "reserved:product:#{product_id}",
    "reservation:user:#{user_id}:product:#{product_id}"
  ]

  result = redis.eval(ATOMIC_RESERVE_SCRIPT, keys: keys, argv: [user_id, ttl])

  if result.is_a?(Hash) && result[:err]
    raise InventoryError, result[:err]
  end

  result[:ok]  # Returns remaining inventory
end
```

**2. Waiting Room Release Algorithm:**

```ruby
def release_batch(sale_id, batch_size: 1000)
  queue_key = "waitingroom:sale:#{sale_id}"

  # Get next batch (sorted by join time)
  users = redis.zrange(queue_key, 0, batch_size - 1)

  users.each do |user_id|
    # Generate time-limited access token
    token = JWT.encode(
      {
        user_id: user_id,
        sale_id: sale_id,
        exp: 30.seconds.from_now.to_i
      },
      Rails.application.secret_key_base
    )

    # Notify user (WebSocket or push notification)
    ActionCable.server.broadcast(
      "waiting_room_#{user_id}",
      { status: 'ready', access_token: token }
    )

    # Remove from queue
    redis.zrem(queue_key, user_id)
  end

  users.size
end
```

**3. Exponential Backoff with Jitter:**

```ruby
def retry_with_backoff(max_attempts: 5, base_delay: 0.5)
  attempts = 0

  begin
    attempts += 1
    yield
  rescue => e
    if attempts < max_attempts && retryable?(e)
      # Exponential backoff: 0.5s, 1s, 2s, 4s, 8s
      delay = base_delay * (2 ** (attempts - 1))

      # Add jitter (0-10% of delay) to prevent thundering herd
      jitter = rand * delay * 0.1

      sleep(delay + jitter)
      retry
    else
      raise
    end
  end
end

# Usage
retry_with_backoff do
  InventoryManager.new(redis, product_id).reserve_for_user(user_id)
end
```

**4. Rate Limiting (Sliding Window):**

```ruby
def rate_limit_check(user_id, limit: 10, window: 1)
  key = "ratelimit:user:#{user_id}"
  now = Time.current.to_f
  window_start = now - window

  # Lua script for atomic sliding window
  lua_script = <<~LUA
    local key = KEYS[1]
    local now = tonumber(ARGV[1])
    local window_start = tonumber(ARGV[2])
    local limit = tonumber(ARGV[3])

    -- Remove old entries
    redis.call('ZREMRANGEBYSCORE', key, '-inf', window_start)

    -- Count current requests
    local count = redis.call('ZCARD', key)

    if count < limit then
      -- Add new request
      redis.call('ZADD', key, now, now)
      redis.call('EXPIRE', key, 2)  -- Cleanup after 2 seconds
      return {ok = limit - count - 1}
    else
      return {err = 'RATE_LIMIT_EXCEEDED'}
    end
  LUA

  result = redis.eval(
    lua_script,
    keys: [key],
    argv: [now, window_start, limit]
  )

  if result.is_a?(Hash) && result[:err]
    raise RateLimitError, result[:err]
  end

  result[:ok]  # Returns remaining requests
end
```

**5. Idempotency Check:**

```ruby
def create_order_idempotent(user_id:, product_id:, idempotency_key:)
  # Check cache first (fast path)
  cached_order_id = redis.get("idempotency:#{idempotency_key}")
  return Order.find(cached_order_id) if cached_order_id

  # Check database
  existing_order = Order.find_by(idempotency_key: idempotency_key)
  if existing_order
    # Cache for future requests
    redis.setex("idempotency:#{idempotency_key}", 3600, existing_order.id)
    return existing_order
  end

  # Create new order
  Order.transaction do
    order = Order.create!(
      user_id: user_id,
      product_id: product_id,
      status: 'RESERVED',
      idempotency_key: idempotency_key,
      total_amount: calculate_amount(product_id)
    )

    # Cache order ID
    redis.setex("idempotency:#{idempotency_key}", 3600, order.id)

    order
  end
rescue ActiveRecord::RecordNotUnique
  # Race condition: Another request created order
  Order.find_by!(idempotency_key: idempotency_key)
end
```

### Sequence Diagrams

**Purchase Flow with Waiting Room:**

```
User    WaitingRoom   API Gateway   FlashSaleAPI   Redis   PostgreSQL   Queue
 │           │             │              │          │         │          │
 │─Join─────>│             │              │          │         │          │
 │           │─ZADD────────────────────────────────>│         │          │
 │<─Position─│             │              │          │         │          │
 │           │             │              │          │         │          │
 │           │─Release Batch (T-0)────────────────>│         │          │
 │<─Token────│             │              │          │         │          │
 │           │             │              │          │         │          │
 │─Purchase (with token)──>│              │          │         │          │
 │           │             │─Rate Limit Check───────>│         │          │
 │           │             │<─OK──────────────────────│         │          │
 │           │             │              │          │         │          │
 │           │             │─Reserve──────>│          │         │          │
 │           │             │              │─Lua Script────────>│          │
 │           │             │              │<─DECR OK───────────│          │
 │           │             │              │          │         │          │
 │           │             │              │─Create Order───────────────>│
 │           │             │              │<─order_id──────────────────│
 │           │             │              │          │         │          │
 │           │             │              │─Publish Payment─────────────────>│
 │           │             │              │          │         │          │
 │<─201 Reserved───────────────────────────│          │         │          │
 │           │             │              │          │         │          │
 │           │             │              │          │         │      Worker
 │           │             │              │          │         │          │
 │           │             │              │          │         │<─Consume─│
 │           │             │              │          │         │          │
 │           │             │              │          │         │  Payment Gateway
 │           │             │              │          │         │          │
 │           │             │              │          │         │<─Charge──│
 │           │             │              │          │         │          │
 │           │             │              │          │         │<─UPDATE status=PAID
 │<─Notification (Payment Success)─────────────────────────────────────────│
```

### Performance Optimizations

**1. Connection Pooling:**
```ruby
# PostgreSQL connection pool
ActiveRecord::Base.establish_connection(
  adapter: 'postgresql',
  pool: 100,  # Max connections
  checkout_timeout: 5
)

# Redis connection pool
REDIS_POOL = ConnectionPool.new(size: 50, timeout: 5) do
  Redis.new(url: ENV['REDIS_URL'])
end
```

**2. Prepared Statements:**
```ruby
# Reuse prepared statements for frequent queries
Order.connection.exec_query(
  "SELECT * FROM orders WHERE idempotency_key = $1",
  "Order Lookup",
  [[nil, idempotency_key]]
)
```

**3. Batch Processing:**
```ruby
# Process expired reservations in batches
Order.where(status: 'RESERVED', reserved_at: ..5.minutes.ago)
  .find_in_batches(batch_size: 1000) do |batch|
    batch.each { |order| release_inventory(order) }
  end
```

**4. Redis Pipelining:**
```ruby
# Batch Redis commands
redis.pipelined do
  users.each do |user_id|
    redis.get("reservation:user:#{user_id}:product:#{product_id}")
  end
end
```

**5. Database Indexing:**
```sql
-- Partial index for active reservations only
CREATE INDEX idx_orders_reserved
ON orders(reserved_at)
WHERE status = 'RESERVED';

-- Covering index for common query
CREATE INDEX idx_orders_user_status
ON orders(user_id, status, created_at DESC)
INCLUDE (id, total_amount);
```

## Step-by-Step Request Flow

## Step-by-Step Request Flow

### Happy Path: Successful Purchase

1. **T-5 minutes: User joins waiting room**
   - User assigned queue position
   - WebSocket connection established for real-time updates
   - Position stored in Redis with TTL

2. **T-0: Sale goes live**
   - Waiting room releases users in batches (1000/second)
   - Prevents thundering herd
   - Users receive "proceed to purchase" token (JWT, 30s expiry)

3. **User clicks "Buy Now"**
   - Request hits API Gateway
   - Rate limiter checks: Redis INCR user:{id}:requests with 1-second TTL
   - If > 10 requests/sec → 429 Too Many Requests
   - Bot detection: Check fingerprint, behavior patterns

4. **Inventory Check (Atomic Operation)**
   ```
   Redis Transaction:
   WATCH inventory:product:123
   GET inventory:product:123
   if count > 0:
       MULTI
       DECR inventory:product:123
       SADD reserved:product:123 user:456
       SETEX reservation:user:456:product:123 300 "1"
       EXEC
   ```
   - If inventory = 0 → Return "Sold Out"
   - If EXEC fails (race condition) → Retry with exponential backoff (max 3 attempts)

5. **Create Order Record (PostgreSQL)**
   ```sql
   INSERT INTO orders (id, user_id, product_id, status, idempotency_key, created_at)
   VALUES (uuid_generate_v4(), 456, 123, 'RESERVED', 'idem_xyz', NOW())
   RETURNING id;
   ```
   - Idempotency key prevents duplicate orders on retry
   - Status: RESERVED (not yet paid)
   - Transaction timeout: 5 seconds

6. **Publish Payment Event**
   - Enqueue message to payment queue
   - Message includes: order_id, user_id, amount, idempotency_key
   - Worker picks up asynchronously

7. **Return to User**
   - Response: "Reserved! Complete payment in 5 minutes"
   - Include reservation_id and payment_url
   - Start client-side countdown timer

### Failure Scenarios

**Scenario 1: Redis DECR succeeds, PostgreSQL INSERT fails**
- Compensation: Background job monitors orphaned Redis reservations
- Every 10 seconds: Check Redis reserved set vs PostgreSQL orders
- If reservation exists in Redis but no order → INCR inventory, remove reservation

**Scenario 2: Payment gateway timeout**
- Payment worker retries with same idempotency_key (3 attempts, exponential backoff)
- After 5 minutes: Mark order as EXPIRED
- Publish inventory_release event
- Worker increments Redis inventory, removes reservation

**Scenario 3: User abandons payment**
- Reservation TTL expires (5 minutes)
- Background job (runs every 30 seconds):
  ```ruby
  expired_orders = Order.where(status: 'RESERVED', created_at: < 5.minutes.ago)
  expired_orders.each do |order|
    release_inventory(order.product_id, order.user_id)
    order.update(status: 'EXPIRED')
  end
  ```

**Scenario 4: Payment succeeds but order update fails**
- Payment service stores payment record with order_id
- Reconciliation job (runs every minute):
  - Find payments without corresponding PAID orders
  - Update order status to PAID
  - If order not found → Refund payment (compensation)

## Data Model Design

### PostgreSQL Schema

```sql
-- Products table
CREATE TABLE products (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    name VARCHAR(255) NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    created_at TIMESTAMP DEFAULT NOW()
);

-- Flash sales table
CREATE TABLE flash_sales (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    product_id UUID REFERENCES products(id),
    total_inventory INTEGER NOT NULL,
    available_inventory INTEGER NOT NULL,
    start_time TIMESTAMP NOT NULL,
    end_time TIMESTAMP NOT NULL,
    max_per_user INTEGER DEFAULT 1,
    created_at TIMESTAMP DEFAULT NOW(),

    CONSTRAINT positive_inventory CHECK (available_inventory >= 0)
);

CREATE INDEX idx_flash_sales_start_time ON flash_sales(start_time);
CREATE INDEX idx_flash_sales_product ON flash_sales(product_id);

-- Orders table
CREATE TABLE orders (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    user_id BIGINT NOT NULL,
    product_id UUID REFERENCES products(id),
    flash_sale_id UUID REFERENCES flash_sales(id),
    quantity INTEGER DEFAULT 1,
    total_amount DECIMAL(10,2) NOT NULL,
    status VARCHAR(50) NOT NULL, -- RESERVED, PAID, EXPIRED, CANCELLED
    idempotency_key VARCHAR(255) UNIQUE NOT NULL,
    reserved_at TIMESTAMP DEFAULT NOW(),
    paid_at TIMESTAMP,
    expired_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_orders_user_id ON orders(user_id);
CREATE INDEX idx_orders_status ON orders(status);
CREATE INDEX idx_orders_idempotency ON orders(idempotency_key);
CREATE INDEX idx_orders_reserved_at ON orders(reserved_at) WHERE status = 'RESERVED';

-- Payments table
CREATE TABLE payments (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    order_id UUID REFERENCES orders(id),
    user_id BIGINT NOT NULL,
    amount DECIMAL(10,2) NOT NULL,
    payment_gateway VARCHAR(50) NOT NULL,
    gateway_transaction_id VARCHAR(255),
    status VARCHAR(50) NOT NULL, -- PENDING, SUCCESS, FAILED, REFUNDED
    idempotency_key VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_payments_order_id ON payments(order_id);
CREATE INDEX idx_payments_status ON payments(status);
CREATE INDEX idx_payments_idempotency ON payments(idempotency_key);
```

### Redis Data Structures

```
# Inventory counter (atomic operations)
inventory:product:{product_id} → INTEGER

# Reserved set (who has reserved)
reserved:product:{product_id} → SET of user_ids

# User reservation (TTL = 5 minutes)
reservation:user:{user_id}:product:{product_id} → "1" (TTL: 300s)

# Rate limiting (TTL = 1 second)
ratelimit:user:{user_id} → INTEGER (TTL: 1s)

# Distributed lock for critical operations
lock:inventory:{product_id} → "lock_token" (TTL: 10s)

# Waiting room queue
waitingroom:sale:{sale_id} → SORTED SET (score = join_timestamp)
```

### Partitioning Strategy

- **Orders table:** Partition by created_at (monthly partitions)
  - Enables efficient archival of old orders
  - Query pattern: Most queries filter by recent dates

- **Payments table:** Partition by created_at (monthly partitions)

- **Flash sales:** No partitioning (small table, < 10K rows)

### Read vs Write Path

**Write Path (Purchase):**
1. Redis DECR (inventory check + reservation)
2. PostgreSQL INSERT (order creation)
3. Message queue PUBLISH (async payment)

**Read Path (Inventory Display):**
1. Redis GET (real-time inventory count)
2. Cache in CDN edge (1-second TTL)
3. Fallback to PostgreSQL if Redis unavailable

## Concurrency & Consistency Strategy

### Inventory Consistency: Pessimistic Locking with Redis

**Why Redis over PostgreSQL for inventory?**
- PostgreSQL row-level locks cause severe contention at 500K RPS
- Redis single-threaded model provides natural serialization
- Redis DECR is atomic (no race conditions)

**Implementation:**

```ruby
class InventoryManager
  def initialize(redis, product_id)
    @redis = redis
    @product_id = product_id
    @inventory_key = "inventory:product:#{product_id}"
  end

  # Atomic inventory reservation
  def reserve_for_user(user_id)
    # Lua script ensures atomicity
    lua_script = <<~LUA
      local inventory_key = KEYS[1]
      local reserved_key = KEYS[2]
      local reservation_key = KEYS[3]
      local user_id = ARGV[1]

      -- Check if user already has reservation
      if redis.call('EXISTS', reservation_key) == 1 then
        return {err = 'ALREADY_RESERVED'}
      end

      -- Check inventory
      local inventory = tonumber(redis.call('GET', inventory_key) or 0)
      if inventory <= 0 then
        return {err = 'SOLD_OUT'}
      end

      -- Atomic reservation
      redis.call('DECR', inventory_key)
      redis.call('SADD', reserved_key, user_id)
      redis.call('SETEX', reservation_key, 300, '1')  -- 5 min TTL

      return {ok = inventory - 1}
    LUA

    keys = [
      @inventory_key,
      "reserved:product:#{@product_id}",
      "reservation:user:#{user_id}:product:#{@product_id}"
    ]

    result = @redis.eval(lua_script, keys: keys, argv: [user_id])

    if result.is_a?(Hash) && result[:err]
      raise InventoryError, result[:err]
    end

    result[:ok]  # Returns remaining inventory
  rescue Redis::BaseError => e
    # Fallback to PostgreSQL if Redis unavailable
    reserve_with_postgres(user_id)
  end

  # Release reservation (payment failed/expired)
  def release_for_user(user_id)
    lua_script = <<~LUA
      local inventory_key = KEYS[1]
      local reserved_key = KEYS[2]
      local reservation_key = KEYS[3]
      local user_id = ARGV[1]

      -- Only release if reservation exists
      if redis.call('EXISTS', reservation_key) == 1 then
        redis.call('INCR', inventory_key)
        redis.call('SREM', reserved_key, user_id)
        redis.call('DEL', reservation_key)
        return 1
      end

      return 0
    LUA

    keys = [
      @inventory_key,
      "reserved:product:#{@product_id}",
      "reservation:user:#{user_id}:product:#{@product_id}"
    ]

    @redis.eval(lua_script, keys: keys, argv: [user_id])
  end
end
```

### Idempotency Strategy

**Problem:** User clicks "Buy" multiple times due to slow response

**Solution:** Idempotency keys

```ruby
class OrderService
  def create_order(user_id:, product_id:, idempotency_key:)
    # Check if order already exists with this idempotency key
    existing_order = Order.find_by(idempotency_key: idempotency_key)
    return existing_order if existing_order

    Order.transaction do
      order = Order.create!(
        user_id: user_id,
        product_id: product_id,
        status: 'RESERVED',
        idempotency_key: idempotency_key,
        total_amount: calculate_amount(product_id)
      )

      # Publish payment event
      PaymentQueue.publish(
        order_id: order.id,
        amount: order.total_amount,
        idempotency_key: "payment_#{idempotency_key}"
      )

      order
    end
  rescue ActiveRecord::RecordNotUnique
    # Race condition: Another request created order with same key
    Order.find_by!(idempotency_key: idempotency_key)
  end
end
```

### Distributed Locking for Critical Operations

**Use Case:** Reconciliation jobs that release expired reservations

```ruby
class ReservationExpiryJob
  def perform
    # Acquire distributed lock to prevent multiple workers
    lock_key = "lock:reservation_expiry"
    lock_token = SecureRandom.uuid

    acquired = redis.set(lock_key, lock_token, nx: true, ex: 60)
    return unless acquired

    begin
      expire_reservations
    ensure
      # Release lock only if we still own it
      lua_script = <<~LUA
        if redis.call('GET', KEYS[1]) == ARGV[1] then
          return redis.call('DEL', KEYS[1])
        end
        return 0
      LUA

      redis.eval(lua_script, keys: [lock_key], argv: [lock_token])
    end
  end

  private

  def expire_reservations
    expired_orders = Order.where(
      status: 'RESERVED',
      reserved_at: ..5.minutes.ago
    ).limit(1000)

    expired_orders.each do |order|
      InventoryManager.new(redis, order.product_id)
        .release_for_user(order.user_id)

      order.update!(status: 'EXPIRED', expired_at: Time.current)
    end
  end
end
```

## Ruby Implementation Examples

### Circuit Breaker for Payment Gateway

```ruby
class PaymentGatewayCircuitBreaker
  FAILURE_THRESHOLD = 5
  TIMEOUT_SECONDS = 60

  def initialize(redis)
    @redis = redis
    @state_key = "circuit_breaker:payment_gateway"
  end

  def call(&block)
    state = current_state

    case state
    when 'open'
      # Circuit is open, fail fast
      raise CircuitBreakerOpen, "Payment gateway circuit is open"
    when 'half_open'
      # Try one request to test if service recovered
      attempt_request(&block)
    else  # 'closed'
      # Normal operation
      attempt_request(&block)
    end
  end

  private

  def current_state
    @redis.get(@state_key) || 'closed'
  end

  def attempt_request(&block)
    result = block.call
    record_success
    result
  rescue => e
    record_failure
    raise
  end

  def record_success
    @redis.del("#{@state_key}:failures")

    # If we were half-open, close the circuit
    if current_state == 'half_open'
      @redis.set(@state_key, 'closed')
    end
  end

  def record_failure
    failures = @redis.incr("#{@state_key}:failures")

    if failures >= FAILURE_THRESHOLD
      # Open the circuit
      @redis.setex(@state_key, TIMEOUT_SECONDS, 'open')

      # After timeout, move to half-open
      # (In production, use a background job for this)
    end
  end
end

# Usage in payment worker
class PaymentWorker
  def perform(order_id, amount, idempotency_key)
    circuit_breaker = PaymentGatewayCircuitBreaker.new(redis)

    circuit_breaker.call do
      PaymentGateway.charge(
        amount: amount,
        idempotency_key: idempotency_key
      )
    end

    # Update order status
    order = Order.find(order_id)
    order.update!(status: 'PAID', paid_at: Time.current)
  rescue CircuitBreakerOpen
    # Retry later
    PaymentWorker.perform_in(30.seconds, order_id, amount, idempotency_key)
  rescue PaymentGateway::Error => e
    # Handle payment failure
    handle_payment_failure(order_id, e)
  end
end
```

### Retry with Exponential Backoff

```ruby
class RetryableOperation
  MAX_ATTEMPTS = 5
  BASE_DELAY = 0.5  # seconds

  def self.with_retry(max_attempts: MAX_ATTEMPTS, &block)
    attempts = 0

    begin
      attempts += 1
      block.call
    rescue => e
      if attempts < max_attempts && retryable_error?(e)
        delay = BASE_DELAY * (2 ** (attempts - 1))  # Exponential backoff
        jitter = rand * delay * 0.1  # Add jitter to prevent thundering herd

        sleep(delay + jitter)
        retry
      else
        raise
      end
    end
  end

  def self.retryable_error?(error)
    error.is_a?(Redis::BaseConnectionError) ||
      error.is_a?(PG::ConnectionBad) ||
      error.is_a?(Timeout::Error)
  end
end

# Usage
RetryableOperation.with_retry do
  InventoryManager.new(redis, product_id).reserve_for_user(user_id)
end
```

### Waiting Room Implementation

```ruby
class WaitingRoomService
  RELEASE_RATE = 1000  # users per second

  def initialize(redis, sale_id)
    @redis = redis
    @sale_id = sale_id
    @queue_key = "waitingroom:sale:#{sale_id}"
  end

  # User joins waiting room
  def join(user_id)
    score = Time.current.to_f
    @redis.zadd(@queue_key, score, user_id)

    # Return position in queue
    position = @redis.zrank(@queue_key, user_id)
    {
      position: position + 1,
      estimated_wait: (position / RELEASE_RATE.to_f).ceil
    }
  end

  # Background job: Release users from waiting room
  def release_batch
    now = Time.current.to_f

    # Get next batch of users
    users = @redis.zrange(@queue_key, 0, RELEASE_RATE - 1)

    users.each do |user_id|
      # Generate access token (JWT)
      token = generate_access_token(user_id)

      # Send via WebSocket or polling endpoint
      notify_user(user_id, token)

      # Remove from queue
      @redis.zrem(@queue_key, user_id)
    end

    users.size
  end

  private

  def generate_access_token(user_id)
    payload = {
      user_id: user_id,
      sale_id: @sale_id,
      exp: 30.seconds.from_now.to_i
    }

    JWT.encode(payload, Rails.application.secret_key_base)
  end
end
```

## Scaling Strategy

### Horizontal Scaling

**Application Servers:**
- Auto-scale based on CPU > 70% or request queue depth > 100
- Pre-warm instances 10 minutes before sale
- Minimum: 10 instances, Maximum: 500 instances
- Scale-up time: 2 minutes (use pre-warmed pool)

**Redis Cluster:**
- 3-node cluster with replication (1 primary, 2 replicas per shard)
- Shard by product_id for inventory data
- Separate cluster for rate limiting (can tolerate data loss)

**PostgreSQL:**
- Primary-replica setup (1 primary, 2 read replicas)
- Write traffic: Primary only
- Read traffic: Load balance across replicas
- Connection pooling: PgBouncer (max 100 connections per instance)

**Message Queue (RabbitMQ/SQS):**
- Separate queues for different priorities:
  - High: Payment processing
  - Medium: Inventory release
  - Low: Analytics events
- Auto-scale workers based on queue depth

### Vertical Scaling

**Redis:**
- Instance type: r6g.4xlarge (128 GB RAM)
- Reason: In-memory operations, need high memory for millions of keys

**PostgreSQL:**
- Instance type: r6g.2xlarge (64 GB RAM)
- Reason: Enough for connection pooling and query cache

### Caching Strategy

**L1 Cache (Application):**
- Product details (price, name): 5-minute TTL
- Flash sale metadata: 1-minute TTL

**L2 Cache (Redis):**
- Inventory count: No TTL (source of truth during sale)
- User reservations: 5-minute TTL (auto-expiry)

**L3 Cache (CDN):**
- Static assets: 1-year TTL
- API responses (inventory count): 1-second TTL

## High Availability Strategy

### Multi-AZ Deployment

```
Region: us-east-1

AZ-1a:                    AZ-1b:                    AZ-1c:
- App Servers (3)         - App Servers (3)         - App Servers (3)
- Redis Primary           - Redis Replica           - Redis Replica
- PostgreSQL Primary      - PostgreSQL Replica      - PostgreSQL Replica
- RabbitMQ Node 1         - RabbitMQ Node 2         - RabbitMQ Node 3
```

**Failover Strategy:**
- Redis: Automatic failover with Sentinel (30-second RTO)
- PostgreSQL: Automatic failover with Patroni (60-second RTO)
- App Servers: Health checks every 5 seconds, remove unhealthy instances

### Circuit Breaker Pattern

Implemented for:
- Payment gateway calls
- Database queries (fallback to cached data)
- External API calls

### Graceful Degradation

**Priority Levels:**
1. **Critical:** Inventory reservation, payment processing
2. **Important:** Order creation, user notifications
3. **Nice-to-have:** Analytics, real-time inventory updates

**Degradation Strategy:**
- If Redis unavailable: Fallback to PostgreSQL (slower but functional)
- If payment gateway slow: Queue payments for async processing
- If database slow: Return cached inventory (with warning)

## Failsafe & Rollback Strategy

### Compensation Mechanisms

**Scenario: Payment succeeds, order update fails**

```ruby
class PaymentReconciliationJob
  # Runs every 1 minute
  def perform
    # Find payments without corresponding PAID orders
    orphaned_payments = Payment.joins(:order)
      .where(payments: { status: 'SUCCESS' })
      .where.not(orders: { status: 'PAID' })
      .where('payments.created_at > ?', 10.minutes.ago)

    orphaned_payments.each do |payment|
      order = payment.order

      if order.status == 'RESERVED'
        # Update order to PAID
        order.update!(status: 'PAID', paid_at: payment.created_at)
        Rails.logger.info("Reconciled order #{order.id}")
      elsif order.status == 'EXPIRED'
        # Order expired but payment succeeded - REFUND
        refund_payment(payment)
        Rails.logger.warn("Refunded payment #{payment.id} for expired order")
      end
    end
  end

  private

  def refund_payment(payment)
    PaymentGateway.refund(
      transaction_id: payment.gateway_transaction_id,
      amount: payment.amount,
      idempotency_key: "refund_#{payment.id}"
    )

    payment.update!(status: 'REFUNDED')
  end
end
```

### Inventory Reconciliation

```ruby
class InventoryReconciliationJob
  # Runs every 5 minutes
  def perform
    FlashSale.active.each do |sale|
      redis_inventory = redis.get("inventory:product:#{sale.product_id}").to_i

      # Count actual orders
      db_sold = Order.where(
        flash_sale_id: sale.id,
        status: ['RESERVED', 'PAID']
      ).sum(:quantity)

      expected_inventory = sale.total_inventory - db_sold

      if redis_inventory != expected_inventory
        Rails.logger.error(
          "Inventory mismatch for sale #{sale.id}: " \
          "Redis=#{redis_inventory}, Expected=#{expected_inventory}"
        )

        # Correct Redis to match database (source of truth)
        redis.set("inventory:product:#{sale.product_id}", expected_inventory)
      end
    end
  end
end
```

### Dead Letter Queue Handling

```ruby
class DeadLetterQueueProcessor
  # Runs every 10 minutes
  def perform
    dlq_messages = fetch_from_dlq('payment_dlq')

    dlq_messages.each do |message|
      order_id = message[:order_id]
      order = Order.find(order_id)

      # Analyze failure reason
      if message[:error_type] == 'PaymentGatewayTimeout'
        # Retry with different gateway
        retry_with_backup_gateway(order)
      elsif message[:error_type] == 'InvalidPaymentMethod'
        # Notify user, release inventory
        notify_user_payment_failed(order.user_id)
        release_inventory(order)
      else
        # Unknown error - manual intervention needed
        alert_ops_team(message)
      end
    end
  end
end
```

## Zero Downtime Deployment Strategy

### Blue-Green Deployment

```
Production Traffic
        │
        ▼
    Load Balancer
        │
        ├─────────────┬─────────────┐
        ▼             ▼             ▼
    Blue (v1.0)   Blue (v1.0)   Blue (v1.0)

    [Deploy v1.1 to Green]

        ▼             ▼             ▼
    Green (v1.1)  Green (v1.1)  Green (v1.1)

    [Run smoke tests on Green]
    [Switch traffic to Green]

Production Traffic
        │
        ▼
    Load Balancer
        │
        ├─────────────┬─────────────┐
        ▼             ▼             ▼
    Green (v1.1)  Green (v1.1)  Green (v1.1)
```

### Database Migration Strategy

**Backward-Compatible Migrations:**

```ruby
# Step 1: Add new column (nullable)
class AddPaymentMethodToOrders < ActiveRecord::Migration[7.0]
  def change
    add_column :orders, :payment_method, :string, null: true
  end
end

# Deploy code that writes to both old and new fields

# Step 2: Backfill data
class BackfillPaymentMethod < ActiveRecord::Migration[7.0]
  def up
    Order.where(payment_method: nil).find_in_batches do |batch|
      batch.each do |order|
        order.update_column(:payment_method, infer_payment_method(order))
      end
    end
  end
end

# Step 3: Make column non-nullable
class MakePaymentMethodNonNullable < ActiveRecord::Migration[7.0]
  def change
    change_column_null :orders, :payment_method, false
  end
end
```

### Feature Flags

```ruby
class FlashSaleController < ApplicationController
  def create_order
    if FeatureFlag.enabled?(:new_inventory_system, user: current_user)
      # New implementation
      NewInventoryService.reserve(product_id, current_user.id)
    else
      # Old implementation
      LegacyInventoryService.reserve(product_id, current_user.id)
    end
  end
end

# Gradual rollout
FeatureFlag.enable_percentage(:new_inventory_system, 10)  # 10% of users
# Monitor metrics
FeatureFlag.enable_percentage(:new_inventory_system, 50)  # 50% of users
# Full rollout
FeatureFlag.enable(:new_inventory_system)
```

## Observability & Monitoring

### Key Metrics

**Business Metrics:**
- Total sales per flash sale
- Conversion rate (reservations → payments)
- Average time to sell out
- Revenue per second

**System Metrics:**
- Request rate (RPS)
- Error rate (4xx, 5xx)
- P50, P95, P99 latency
- Redis hit rate
- Database connection pool utilization
- Queue depth (payment queue)

**Custom Metrics:**
```ruby
class MetricsCollector
  def self.record_purchase_attempt(product_id, success:, latency_ms:)
    StatsD.increment('flash_sale.purchase_attempt',
      tags: ["product:#{product_id}", "success:#{success}"])

    StatsD.histogram('flash_sale.purchase_latency', latency_ms,
      tags: ["product:#{product_id}"])
  end

  def self.record_inventory_level(product_id, level)
    StatsD.gauge('flash_sale.inventory', level,
      tags: ["product:#{product_id}"])
  end
end
```

### Distributed Tracing

```ruby
# Using OpenTelemetry
class FlashSaleController < ApplicationController
  def create_order
    tracer = OpenTelemetry.tracer_provider.tracer('flash_sale')

    tracer.in_span('create_order') do |span|
      span.set_attribute('user.id', current_user.id)
      span.set_attribute('product.id', params[:product_id])

      # Inventory check
      tracer.in_span('inventory.check') do
        inventory_manager.reserve_for_user(current_user.id)
      end

      # Order creation
      tracer.in_span('order.create') do
        OrderService.create_order(...)
      end
    end
  end
end
```

### Alerting Thresholds

```yaml
alerts:
  - name: HighErrorRate
    condition: error_rate > 5%
    duration: 1m
    severity: critical

  - name: HighLatency
    condition: p99_latency > 2s
    duration: 2m
    severity: warning

  - name: InventoryMismatch
    condition: redis_inventory != db_inventory
    duration: 0s
    severity: critical

  - name: PaymentQueueBacklog
    condition: queue_depth > 10000
    duration: 5m
    severity: warning
```

## Testing Strategy

### Unit Tests

```ruby
RSpec.describe InventoryManager do
  let(:redis) { MockRedis.new }
  let(:product_id) { 123 }
  let(:manager) { described_class.new(redis, product_id) }

  before do
    redis.set("inventory:product:#{product_id}", 10)
  end

  describe '#reserve_for_user' do
    it 'decrements inventory atomically' do
      expect {
        manager.reserve_for_user(456)
      }.to change {
        redis.get("inventory:product:#{product_id}").to_i
      }.from(10).to(9)
    end

    it 'prevents double reservation' do
      manager.reserve_for_user(456)

      expect {
        manager.reserve_for_user(456)
      }.to raise_error(InventoryError, 'ALREADY_RESERVED')
    end

    it 'prevents overselling' do
      redis.set("inventory:product:#{product_id}", 0)

      expect {
        manager.reserve_for_user(456)
      }.to raise_error(InventoryError, 'SOLD_OUT')
    end
  end
end
```

### Integration Tests

```ruby
RSpec.describe 'Flash Sale Purchase Flow', type: :request do
  let(:flash_sale) { create(:flash_sale, total_inventory: 100) }
  let(:user) { create(:user) }

  before do
    # Initialize Redis inventory
    redis.set("inventory:product:#{flash_sale.product_id}", 100)
  end

  it 'completes full purchase flow' do
    # Reserve inventory
    post '/api/flash_sales/purchase', params: {
      product_id: flash_sale.product_id,
      idempotency_key: 'test_key_123'
    }, headers: auth_headers(user)

    expect(response).to have_http_status(:created)
    order = Order.last
    expect(order.status).to eq('RESERVED')

    # Process payment (async)
    PaymentWorker.drain  # Process background jobs

    order.reload
    expect(order.status).to eq('PAID')

    # Verify inventory decremented
    inventory = redis.get("inventory:product:#{flash_sale.product_id}").to_i
    expect(inventory).to eq(99)
  end
end
```

### Load Testing

```ruby
# Using k6 or Apache JMeter
# load_test.js
import http from 'k6/http';
import { check, sleep } from 'k6';

export let options = {
  stages: [
    { duration: '30s', target: 1000 },   // Ramp up to 1K users
    { duration: '1m', target: 10000 },   // Ramp up to 10K users
    { duration: '30s', target: 50000 },  // Spike to 50K users
    { duration: '2m', target: 50000 },   // Sustain 50K users
    { duration: '30s', target: 0 },      // Ramp down
  ],
  thresholds: {
    http_req_duration: ['p(95)<2000'],  // 95% of requests < 2s
    http_req_failed: ['rate<0.05'],     // Error rate < 5%
  },
};

export default function () {
  const url = 'https://api.example.com/flash_sales/purchase';
  const payload = JSON.stringify({
    product_id: 123,
    idempotency_key: `key_${__VU}_${__ITER}`,
  });

  const params = {
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${__ENV.AUTH_TOKEN}`,
    },
  };

  const res = http.post(url, payload, params);

  check(res, {
    'status is 201 or 409': (r) => r.status === 201 || r.status === 409,
    'response time < 2s': (r) => r.timings.duration < 2000,
  });

  sleep(1);
}
```

### Chaos Testing

```ruby
# Using Chaos Monkey or Toxiproxy
class ChaosTest
  def test_redis_failure
    # Simulate Redis failure
    Toxiproxy[:redis].down do
      # System should fallback to PostgreSQL
      response = purchase_product(product_id: 123, user_id: 456)
      expect(response.status).to eq(201)
      expect(response.body['warning']).to include('degraded mode')
    end
  end

  def test_payment_gateway_timeout
    # Simulate slow payment gateway
    Toxiproxy[:payment_gateway].toxic(:latency, latency: 10000) do
      # Circuit breaker should open
      expect {
        PaymentWorker.new.perform(order_id, amount, idempotency_key)
      }.to raise_error(CircuitBreakerOpen)
    end
  end
end
```

## Trade-offs & Alternatives

### Chosen: Redis for Inventory

**Pros:**
- Atomic operations (DECR, INCR)
- Sub-millisecond latency
- Handles 500K RPS easily
- Simple consistency model (single-threaded)

**Cons:**
- In-memory only (data loss risk)
- Requires reconciliation with PostgreSQL
- Additional infrastructure complexity

**Alternative: PostgreSQL with Row-Level Locks**

**Pros:**
- Single source of truth
- ACID guarantees
- No reconciliation needed

**Cons:**
- Lock contention at high concurrency
- Latency: 10-50ms vs Redis <1ms
- Connection pool exhaustion

**Decision:** Redis for hot path, PostgreSQL as source of truth

---

### Chosen: Waiting Room

**Pros:**
- Prevents thundering herd
- Better user experience (queue position)
- Protects backend from overload

**Cons:**
- Additional complexity
- Requires WebSocket infrastructure
- Users may abandon queue

**Alternative: No Waiting Room (First-Come-First-Served)**

**Pros:**
- Simpler implementation
- Lower latency for users

**Cons:**
- System overload risk
- Poor user experience (constant retries)
- Unfair (network latency advantage)

**Decision:** Waiting room for sales with >100K expected users

---

### Chosen: Async Payment Processing

**Pros:**
- Faster response to user
- Decouples inventory from payment
- Can retry payment failures

**Cons:**
- Eventual consistency
- Requires reconciliation
- More complex error handling

**Alternative: Synchronous Payment**

**Pros:**
- Immediate confirmation
- Simpler consistency model

**Cons:**
- Slower user experience
- Payment gateway becomes bottleneck
- Harder to scale

**Decision:** Async for better scalability, with strong reconciliation

---

### Cost Considerations

**Infrastructure Costs (per flash sale):**
- Redis Cluster: $500/month (reserved) + $200/hour (burst)
- PostgreSQL: $800/month (reserved)
- App Servers: $1000/month (baseline) + $50/hour (burst)
- Load Balancer: $100/month
- Message Queue: $200/month

**Optimization:**
- Use spot instances for burst capacity (70% cost savings)
- Scale down to baseline after sale
- Use CDN to reduce origin traffic (90% reduction)

**Total Cost per Sale:** ~$500 (assuming 2-hour burst)
**Revenue per Sale:** $100K-$1M (depending on product)
**Cost Ratio:** 0.05-0.5%
