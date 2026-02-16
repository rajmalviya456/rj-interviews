# Multi-Region Payment System

## Problem Statement

Design a globally distributed payment processing system that handles transactions across multiple regions with strong consistency guarantees, regulatory compliance, and high availability.

**Scale Requirements:**
- 50,000 transactions per second globally
- 100+ countries supported
- Multi-currency support (150+ currencies)
- Average transaction value: $50-$5000
- Peak load: 5x normal during holidays
- 99.999% uptime requirement (5 minutes downtime/year)

**Business Constraints:**
- Zero tolerance for double-charging
- Zero tolerance for lost payments
- PCI-DSS compliance required
- GDPR, SOC2, and regional data residency requirements
- Chargebacks must be traceable
- Settlement within 24 hours
- Support for refunds, partial refunds, and disputes

**Failure Expectations:**
- System must handle payment gateway failures
- Database failures must not lose transaction data
- Network partitions between regions
- Graceful degradation during regional outages

**Edge Cases:**
- Concurrent payment attempts with same card
- Payment gateway timeout after charge succeeds
- Currency conversion rate changes mid-transaction
- User cancels payment after processing starts
- Duplicate payment requests (retry storms)
- Cross-border transactions with different regulations

## Functional Requirements

- Process credit card, debit card, and digital wallet payments
- Support multiple payment gateways (Stripe, PayPal, Adyen)
- Handle currency conversion in real-time
- Implement fraud detection
- Support 3D Secure authentication
- Process refunds and partial refunds
- Handle chargebacks and disputes
- Generate payment receipts
- Provide real-time payment status
- Support recurring payments/subscriptions
- Implement payment retry logic
- Provide merchant dashboard for analytics

## Non-Functional Requirements

- **Availability:** 99.999% (5 minutes downtime/year)
- **Latency:**
  - P50: < 500ms end-to-end
  - P99: < 2s end-to-end
- **Throughput:** 50K TPS globally
- **Consistency:** Strong consistency for payment state
- **Durability:** Zero data loss (payments, refunds, disputes)
- **Security:** PCI-DSS Level 1 compliance
- **Accuracy:** 100% accuracy in payment amounts
- **Auditability:** Complete audit trail for all transactions

## Core Engineering Challenges

1. **Distributed Transactions**
   - Two-phase commit across payment gateway and database
   - Handling partial failures (gateway succeeds, DB fails)
   - Idempotency across retries
   - Saga pattern for long-running transactions

2. **Strong Consistency**
   - Preventing double-charging
   - Ensuring exactly-once payment processing
   - Handling concurrent payment attempts
   - Distributed locking for critical operations

3. **Multi-Region Coordination**
   - Data residency requirements (EU data stays in EU)
   - Cross-region transaction routing
   - Eventual consistency for analytics
   - Strong consistency for payment state

4. **Payment Gateway Integration**
   - Multiple gateway support with failover
   - Gateway-specific error handling
   - Webhook processing and verification
   - Timeout and retry strategies

5. **Currency Conversion**
   - Real-time exchange rates
   - Rate locking during transaction
   - Handling rate fluctuations
   - Multi-currency settlement

6. **Fraud Detection**
   - Real-time risk scoring
   - Velocity checks (multiple payments in short time)
   - Geolocation verification
   - Device fingerprinting
   - Machine learning model integration

## High-Level Design (HLD)

### System Architecture Overview

The multi-region payment system uses a **regional-first architecture with strong consistency** and the following key components:

1. **Regional Payment APIs** - Process payments in user's region for low latency
2. **Payment Gateway Orchestrator** - Manage multiple payment gateways with failover
3. **Fraud Detection Service** - Real-time risk scoring before payment processing
4. **Transaction Coordinator** - Ensure exactly-once payment processing with Saga pattern
5. **Regional Databases** - Strong consistency within region, async replication across regions
6. **Audit Service** - Complete audit trail for compliance

### Architecture Diagram

```
                                Users (Global)
                                      │
                                      ▼
                          Global Load Balancer
                          (GeoDNS Routing)
                                      │
        ┌─────────────────────────────┼─────────────────────────────┐
        ▼                             ▼                             ▼
    Region: US-EAST              Region: EU-WEST              Region: AP-SOUTH
        │                             │                             │
        ▼                             ▼                             ▼
  Regional LB                   Regional LB                   Regional LB
        │                             │                             │
        ▼                             ▼                             ▼
  Payment API                   Payment API                   Payment API
  (Stateless)                   (Stateless)                   (Stateless)
        │                             │                             │
        ├─────────────────────────────┼─────────────────────────────┤
        │                             │                             │
        ▼                             ▼                             ▼
  Fraud Detection              Fraud Detection              Fraud Detection
  Service                      Service                      Service
        │                             │                             │
        ▼                             ▼                             ▼
  Payment Gateway              Payment Gateway              Payment Gateway
  Orchestrator                 Orchestrator                 Orchestrator
        │                             │                             │
        ├──────────┬──────────┬───────┼──────────┬──────────┬───────┤
        ▼          ▼          ▼       ▼          ▼          ▼       ▼
    Stripe     PayPal     Adyen   Stripe     PayPal     Adyen   Stripe...
        │                             │                             │
        ▼                             ▼                             ▼
  PostgreSQL                    PostgreSQL                    PostgreSQL
  (Primary)                     (Primary)                     (Primary)
  + Replicas                    + Replicas                    + Replicas
        │                             │                             │
        └─────────────────────────────┼─────────────────────────────┘
                                      │
                                      ▼
                          Cross-Region Replication
                          (Async for Analytics)
                                      │
                                      ▼
                              Data Warehouse
                              (Analytics)
```

### Component Responsibilities

**1. Global Load Balancer (GeoDNS):**
- Route users to nearest region based on geolocation
- Health check regional endpoints
- Failover to backup regions during outages
- DDoS protection and rate limiting

**2. Payment API (Regional):**
- Accept payment requests with idempotency keys
- Validate payment data (card number, CVV, amount)
- Coordinate with fraud detection service
- Orchestrate payment gateway calls
- Ensure exactly-once processing

**3. Fraud Detection Service:**
- Real-time risk scoring (0-100)
- Velocity checks (multiple payments from same user/card)
- Geolocation verification (IP vs billing address)
- Device fingerprinting
- ML model inference for fraud patterns
- Block high-risk transactions

**4. Payment Gateway Orchestrator:**
- Manage multiple payment gateways (Stripe, PayPal, Adyen)
- Gateway selection based on: currency, region, cost, success rate
- Automatic failover on gateway errors
- Retry logic with exponential backoff
- Webhook processing and verification

**5. Transaction Coordinator:**
- Implement Saga pattern for distributed transactions
- Coordinate payment gateway call + database write
- Handle compensating transactions (refunds on failure)
- Ensure idempotency with deduplication
- Distributed locking for concurrent payments

**6. Regional PostgreSQL:**
- Store payment records with strong consistency
- Transaction log for audit trail
- Read replicas for analytics queries
- Async replication to other regions
- Point-in-time recovery

**7. Audit Service:**
- Log all payment events (initiated, authorized, captured, failed)
- Immutable audit trail for compliance
- Support for PCI-DSS, GDPR, SOC2 audits
- Retention policies per regulation

### Data Flow

```
1. Payment Request
   User → Global LB → Regional LB → Payment API
   → Extract: user_id, amount, currency, payment_method, idempotency_key

2. Fraud Detection
   Payment API → Fraud Detection Service
   → Check: velocity, geolocation, device fingerprint, ML model
   → Response: risk_score (0-100), decision (ALLOW/BLOCK/REVIEW)
   → If BLOCK: Return 403 Forbidden
   → If REVIEW: Queue for manual review

3. Payment Processing (Saga Pattern)
   Payment API → Transaction Coordinator
   → Step 1: Reserve payment in DB (status=PENDING)
   → Step 2: Call Payment Gateway (Stripe/PayPal/Adyen)
   → Step 3: Update DB (status=AUTHORIZED or FAILED)
   → If failure: Compensating transaction (release reservation)

4. Payment Gateway Call
   Transaction Coordinator → Gateway Orchestrator
   → Select gateway (based on currency, region, cost)
   → Call gateway API with idempotency key
   → Handle response: SUCCESS, FAILURE, TIMEOUT
   → On TIMEOUT: Poll gateway for status (max 3 retries)

5. Database Write
   Transaction Coordinator → PostgreSQL
   → Insert payment record (ACID transaction)
   → Update user balance/credits
   → Log audit event
   → Commit transaction

6. Response to User
   Payment API → User
   → 200 OK: {payment_id, status, amount, currency}
   → 402 Payment Required: {error, reason}
   → 429 Too Many Requests: {retry_after}
```

### Scalability Strategy

**Horizontal Scaling:**
- Payment APIs: Auto-scale based on request rate (10-100 instances per region)
- Fraud Detection: Dedicated service pool (5-20 instances per region)
- Gateway Orchestrator: Stateless, scale independently
- PostgreSQL: Read replicas for analytics (3-10 per region)

**Vertical Scaling:**
- Payment API: c6g.xlarge (4 vCPU, 8 GB RAM)
- Fraud Detection: c6g.2xlarge (8 vCPU, 16 GB RAM) for ML inference
- PostgreSQL: r6g.4xlarge (16 vCPU, 128 GB RAM)

**Partitioning:**
- Database: Shard by user_id hash (16 shards per region)
- Payment records: Partition by created_at (monthly partitions)
- Audit logs: Partition by date (daily partitions)

**Caching:**
- Fraud rules: Redis cache (1-minute TTL)
- Currency exchange rates: Redis cache (5-minute TTL)
- User payment methods: Redis cache (10-minute TTL)
- Gateway configurations: In-memory cache (1-hour TTL)

### Failure Handling

**Payment Gateway Failure:**
- Automatic failover to backup gateway (Stripe → PayPal → Adyen)
- Circuit breaker pattern (open after 5 failures in 1 minute)
- Retry with exponential backoff (1s, 2s, 4s, 8s, 16s)
- Queue failed payments for manual processing
- Alert operations team (PagerDuty)
- RTO: < 30 seconds, RPO: 0 (no data loss)

**Database Failure:**
- Automatic failover to read replica (Patroni)
- Promote replica to primary (< 30s)
- Replay WAL logs for zero data loss
- Queue writes during failover
- RTO: < 30 seconds, RPO: 0 (no data loss)

**Fraud Detection Service Failure:**
- Fail open: Allow payments with warning flag
- Use cached fraud rules
- Queue for post-processing fraud check
- Alert security team
- RTO: < 1 minute, RPO: N/A

**Network Partition:**
- Regional isolation: Each region operates independently
- Cross-region replication paused during partition
- Reconciliation after partition heals
- Conflict resolution: Last-write-wins for analytics, manual for payments

**Timeout Handling:**
- Payment gateway timeout: 30 seconds
- Poll gateway for status (max 3 retries, 5s interval)
- If still unknown: Mark as PENDING_VERIFICATION
- Background job polls gateway every 1 minute
- Manual intervention after 1 hour

## Low-Level Design (LLD)

### Class Diagram

```
┌─────────────────────────────┐
│   PaymentController         │
├─────────────────────────────┤
│ + create_payment(params)    │
│ + get_payment_status(id)    │
│ + refund_payment(id)        │
└─────────────────────────────┘
            │
            │ uses
            ▼
┌─────────────────────────────┐
│   PaymentService            │
├─────────────────────────────┤
│ - fraud_detector            │
│ - gateway_orchestrator      │
│ - transaction_coordinator   │
├─────────────────────────────┤
│ + process_payment(params)   │
│ + validate_payment()        │
│ - check_idempotency()       │
└─────────────────────────────┘
            │
            │ uses
            ▼
┌─────────────────────────────┐
│   TransactionCoordinator    │
├─────────────────────────────┤
│ - db: Database              │
│ - gateway: GatewayOrch      │
├─────────────────────────────┤
│ + execute_saga(payment)     │
│ - reserve_payment()         │
│ - charge_gateway()          │
│ - finalize_payment()        │
│ - compensate()              │
└─────────────────────────────┘
            │
            │ uses
            ▼
┌─────────────────────────────┐
│   GatewayOrchestrator       │
├─────────────────────────────┤
│ - gateways: Array           │
│ - circuit_breakers: Hash    │
├─────────────────────────────┤
│ + charge(payment)           │
│ + refund(payment_id)        │
│ - select_gateway()          │
│ - handle_timeout()          │
│ - retry_with_backoff()      │
└─────────────────────────────┘
            │
            │ uses
            ▼
┌─────────────────────────────┐
│   StripeGateway             │
├─────────────────────────────┤
│ + charge(amount, card)      │
│ + refund(charge_id)         │
│ + verify_webhook()          │
└─────────────────────────────┘

┌─────────────────────────────┐
│   FraudDetectionService     │
├─────────────────────────────┤
│ - ml_model: Model           │
│ - rules_engine: Engine      │
├─────────────────────────────┤
│ + score_payment(payment)    │
│ - check_velocity()          │
│ - check_geolocation()       │
│ - check_device()            │
└─────────────────────────────┘

┌─────────────────────────────┐
│   AuditService              │
├─────────────────────────────┤
│ + log_event(event)          │
│ + get_audit_trail(id)       │
└─────────────────────────────┘
```

### Database Schema Details

**Payments Table:**
```sql
CREATE TABLE payments (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    idempotency_key VARCHAR(255) UNIQUE NOT NULL,
    user_id BIGINT NOT NULL,
    amount DECIMAL(19, 4) NOT NULL,
    currency VARCHAR(3) NOT NULL,
    status VARCHAR(50) NOT NULL, -- PENDING, AUTHORIZED, CAPTURED, FAILED, REFUNDED
    payment_method_type VARCHAR(50) NOT NULL, -- card, wallet, bank_transfer
    payment_method_id VARCHAR(255),
    gateway VARCHAR(50) NOT NULL, -- stripe, paypal, adyen
    gateway_transaction_id VARCHAR(255),
    gateway_response JSONB,
    fraud_score INTEGER, -- 0-100
    fraud_decision VARCHAR(20), -- ALLOW, BLOCK, REVIEW
    error_code VARCHAR(50),
    error_message TEXT,
    metadata JSONB,
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),
    captured_at TIMESTAMP,

    CONSTRAINT positive_amount CHECK (amount > 0),
    CONSTRAINT valid_status CHECK (status IN ('PENDING', 'AUTHORIZED', 'CAPTURED', 'FAILED', 'REFUNDED'))
) PARTITION BY RANGE (created_at);

-- Monthly partitions
CREATE TABLE payments_2024_01 PARTITION OF payments
    FOR VALUES FROM ('2024-01-01') TO ('2024-02-01');

CREATE INDEX idx_payments_user_id ON payments(user_id, created_at DESC);
CREATE INDEX idx_payments_idempotency ON payments(idempotency_key);
CREATE INDEX idx_payments_status ON payments(status, created_at DESC);
CREATE INDEX idx_payments_gateway_txn ON payments(gateway_transaction_id);
```

**Refunds Table:**
```sql
CREATE TABLE refunds (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    payment_id UUID NOT NULL REFERENCES payments(id),
    amount DECIMAL(19, 4) NOT NULL,
    reason VARCHAR(255),
    status VARCHAR(50) NOT NULL, -- PENDING, COMPLETED, FAILED
    gateway_refund_id VARCHAR(255),
    created_at TIMESTAMP DEFAULT NOW(),
    completed_at TIMESTAMP,

    CONSTRAINT positive_refund_amount CHECK (amount > 0)
);

CREATE INDEX idx_refunds_payment_id ON refunds(payment_id);
CREATE INDEX idx_refunds_status ON refunds(status, created_at DESC);
```

**Audit Events Table:**
```sql
CREATE TABLE audit_events (
    id BIGSERIAL PRIMARY KEY,
    payment_id UUID NOT NULL,
    event_type VARCHAR(50) NOT NULL, -- INITIATED, AUTHORIZED, CAPTURED, FAILED, REFUNDED
    actor VARCHAR(255), -- user_id, system, admin_id
    details JSONB NOT NULL,
    ip_address INET,
    user_agent TEXT,
    created_at TIMESTAMP DEFAULT NOW()
) PARTITION BY RANGE (created_at);

-- Daily partitions for audit logs
CREATE TABLE audit_events_2024_01_15 PARTITION OF audit_events
    FOR VALUES FROM ('2024-01-15') TO ('2024-01-16');

CREATE INDEX idx_audit_payment_id ON audit_events(payment_id, created_at DESC);
CREATE INDEX idx_audit_event_type ON audit_events(event_type, created_at DESC);
```

### API Endpoints

**Payment Processing API:**

```ruby
# Create payment
POST /api/v1/payments
{
  "amount": 100.00,
  "currency": "USD",
  "payment_method": {
    "type": "card",
    "card_number": "4242424242424242",
    "exp_month": 12,
    "exp_year": 2025,
    "cvv": "123"
  },
  "idempotency_key": "550e8400-e29b-41d4-a716-446655440000",
  "metadata": {
    "order_id": "ORD-12345",
    "customer_id": "CUST-67890"
  }
}

Response: 200 OK
{
  "payment_id": "pay_1234567890",
  "status": "CAPTURED",
  "amount": 100.00,
  "currency": "USD",
  "created_at": "2024-01-16T12:00:00Z"
}

Response: 402 Payment Required
{
  "error": "payment_failed",
  "message": "Insufficient funds",
  "payment_id": "pay_1234567890"
}

# Get payment status
GET /api/v1/payments/:id

Response: 200 OK
{
  "payment_id": "pay_1234567890",
  "status": "CAPTURED",
  "amount": 100.00,
  "currency": "USD",
  "gateway": "stripe",
  "created_at": "2024-01-16T12:00:00Z",
  "captured_at": "2024-01-16T12:00:05Z"
}

# Refund payment
POST /api/v1/payments/:id/refund
{
  "amount": 50.00,  # Partial refund
  "reason": "Customer request"
}

Response: 200 OK
{
  "refund_id": "ref_9876543210",
  "payment_id": "pay_1234567890",
  "amount": 50.00,
  "status": "COMPLETED"
}
```

**Webhook API:**

```ruby
# Process payment gateway webhook
POST /webhooks/stripe
Headers:
  Stripe-Signature: t=1234567890,v1=abc123...

Body:
{
  "type": "payment_intent.succeeded",
  "data": {
    "object": {
      "id": "pi_1234567890",
      "amount": 10000,
      "currency": "usd",
      "status": "succeeded"
    }
  }
}

Response: 200 OK
```

### Algorithms

**1. Saga Pattern for Distributed Transactions:**

```ruby
class TransactionCoordinator
  def execute_saga(payment_params)
    # Step 1: Reserve payment in database
    payment = reserve_payment(payment_params)

    begin
      # Step 2: Charge payment gateway
      gateway_response = charge_gateway(payment)

      # Step 3: Finalize payment
      finalize_payment(payment, gateway_response)

      payment
    rescue => e
      # Compensating transaction: Release reservation
      compensate(payment, e)
      raise
    end
  end

  private

  def reserve_payment(params)
    Payment.transaction do
      payment = Payment.create!(
        idempotency_key: params[:idempotency_key],
        user_id: params[:user_id],
        amount: params[:amount],
        currency: params[:currency],
        status: 'PENDING',
        payment_method_type: params[:payment_method][:type]
      )

      # Log audit event
      AuditService.log_event(
        payment_id: payment.id,
        event_type: 'INITIATED',
        actor: params[:user_id],
        details: params
      )

      payment
    end
  end

  def charge_gateway(payment)
    gateway_orchestrator.charge(
      amount: payment.amount,
      currency: payment.currency,
      payment_method: payment.payment_method,
      idempotency_key: payment.idempotency_key
    )
  end

  def finalize_payment(payment, gateway_response)
    Payment.transaction do
      payment.update!(
        status: 'CAPTURED',
        gateway_transaction_id: gateway_response[:transaction_id],
        gateway_response: gateway_response,
        captured_at: Time.current
      )

      # Log audit event
      AuditService.log_event(
        payment_id: payment.id,
        event_type: 'CAPTURED',
        actor: 'system',
        details: gateway_response
      )
    end
  end

  def compensate(payment, error)
    Payment.transaction do
      payment.update!(
        status: 'FAILED',
        error_code: error.class.name,
        error_message: error.message
      )

      # Log audit event
      AuditService.log_event(
        payment_id: payment.id,
        event_type: 'FAILED',
        actor: 'system',
        details: { error: error.message }
      )
    end
  end
end
```

**2. Idempotency Check:**

```ruby
class PaymentService
  def process_payment(params)
    # Check for existing payment with same idempotency key
    existing_payment = Payment.find_by(idempotency_key: params[:idempotency_key])

    if existing_payment
      # Return existing payment (idempotent)
      return existing_payment
    end

    # Acquire distributed lock to prevent concurrent processing
    lock_key = "payment:lock:#{params[:idempotency_key]}"

    redis.with_lock(lock_key, ttl: 30) do
      # Double-check after acquiring lock
      existing_payment = Payment.find_by(idempotency_key: params[:idempotency_key])
      return existing_payment if existing_payment

      # Process new payment
      transaction_coordinator.execute_saga(params)
    end
  end
end
```

**3. Gateway Selection Algorithm:**

```ruby
class GatewayOrchestrator
  GATEWAYS = {
    stripe: { cost: 0.029, success_rate: 0.98, currencies: ['USD', 'EUR', 'GBP'] },
    paypal: { cost: 0.034, success_rate: 0.95, currencies: ['USD', 'EUR', 'GBP', 'JPY'] },
    adyen: { cost: 0.025, success_rate: 0.97, currencies: ['USD', 'EUR', 'GBP', 'JPY', 'INR'] }
  }

  def select_gateway(currency:, region:, amount:)
    # Filter gateways that support the currency
    available_gateways = GATEWAYS.select do |name, config|
      config[:currencies].include?(currency) && circuit_breaker_closed?(name)
    end

    # Select gateway with lowest cost and highest success rate
    selected = available_gateways.min_by do |name, config|
      # Score = cost * amount - (success_rate * 100)
      # Lower score is better
      (config[:cost] * amount) - (config[:success_rate] * 100)
    end

    selected&.first || raise(NoGatewayAvailableError)
  end

  def circuit_breaker_closed?(gateway_name)
    key = "circuit_breaker:#{gateway_name}"
    failures = redis.get(key).to_i

    # Open circuit breaker if > 5 failures in last minute
    failures < 5
  end
end
```

**4. Fraud Detection Algorithm:**

```ruby
class FraudDetectionService
  FRAUD_RULES = {
    velocity: { max_payments_per_hour: 10, max_amount_per_hour: 1000 },
    geolocation: { max_distance_km: 500 },
    device: { max_devices_per_user: 3 }
  }

  def score_payment(payment_params)
    scores = []

    # Velocity check
    scores << check_velocity(payment_params[:user_id])

    # Geolocation check
    scores << check_geolocation(payment_params[:user_id], payment_params[:ip_address])

    # Device fingerprint check
    scores << check_device(payment_params[:user_id], payment_params[:device_fingerprint])

    # ML model inference
    scores << ml_model.predict(payment_params)

    # Aggregate scores (weighted average)
    total_score = (scores[0] * 0.3) + (scores[1] * 0.2) + (scores[2] * 0.2) + (scores[3] * 0.3)

    decision = case total_score
    when 0..30 then 'ALLOW'
    when 31..70 then 'REVIEW'
    else 'BLOCK'
    end

    { score: total_score, decision: decision }
  end

  private

  def check_velocity(user_id)
    # Count payments in last hour
    recent_payments = Payment.where(
      user_id: user_id,
      created_at: 1.hour.ago..Time.current
    )

    count = recent_payments.count
    total_amount = recent_payments.sum(:amount)

    score = 0
    score += 50 if count > FRAUD_RULES[:velocity][:max_payments_per_hour]
    score += 50 if total_amount > FRAUD_RULES[:velocity][:max_amount_per_hour]

    score
  end

  def check_geolocation(user_id, ip_address)
    # Get user's last known location
    last_location = UserLocation.where(user_id: user_id).last
    current_location = GeoIP.lookup(ip_address)

    return 0 unless last_location

    # Calculate distance
    distance_km = Geocoder::Calculations.distance_between(
      [last_location.lat, last_location.lon],
      [current_location.lat, current_location.lon]
    )

    # Impossible travel detection
    time_diff_hours = (Time.current - last_location.created_at) / 3600.0
    max_possible_distance = time_diff_hours * 900  # 900 km/h (airplane speed)

    distance_km > max_possible_distance ? 100 : 0
  end

  def check_device(user_id, device_fingerprint)
    # Count unique devices for user
    device_count = UserDevice.where(user_id: user_id).distinct.count(:fingerprint)

    device_count > FRAUD_RULES[:device][:max_devices_per_user] ? 50 : 0
  end
end
```

**5. Retry with Exponential Backoff:**

```ruby
class GatewayOrchestrator
  MAX_RETRIES = 5
  BASE_DELAY = 1  # second

  def charge_with_retry(payment)
    retries = 0

    begin
      gateway = select_gateway(
        currency: payment.currency,
        region: payment.region,
        amount: payment.amount
      )

      gateway_client(gateway).charge(
        amount: payment.amount,
        currency: payment.currency,
        payment_method: payment.payment_method,
        idempotency_key: payment.idempotency_key
      )
    rescue GatewayTimeoutError, GatewayUnavailableError => e
      retries += 1

      if retries <= MAX_RETRIES
        # Exponential backoff with jitter
        delay = BASE_DELAY * (2 ** (retries - 1)) + rand(0..1.0)

        Rails.logger.warn("Gateway error, retrying in #{delay}s: #{e.message}")
        sleep(delay)

        # Increment circuit breaker counter
        increment_circuit_breaker(gateway)

        retry
      else
        # Max retries exceeded, fail payment
        raise PaymentProcessingError, "Max retries exceeded: #{e.message}"
      end
    end
  end

  private

  def increment_circuit_breaker(gateway_name)
    key = "circuit_breaker:#{gateway_name}"
    redis.incr(key)
    redis.expire(key, 60)  # Reset after 1 minute
  end
end
```

### Sequence Diagrams

**Payment Processing Flow:**

```
User    API    Fraud    Gateway    DB    Audit
 │       │       │         │        │      │
 │──Pay──>│       │         │        │      │
 │       │       │         │        │      │
 │       │──Check Idempotency──────>│      │
 │       │<──Not Found──────────────│      │
 │       │       │         │        │      │
 │       │──Score Payment──>│        │      │
 │       │<──ALLOW (score=25)│       │      │
 │       │       │         │        │      │
 │       │──Reserve Payment─────────>│      │
 │       │<──Payment (PENDING)───────│      │
 │       │       │         │        │      │
 │       │───────────────Log Event───────────>│
 │       │       │         │        │      │
 │       │──────────Charge─>│        │      │
 │       │<─────────Success─│        │      │
 │       │       │         │        │      │
 │       │──Finalize Payment────────>│      │
 │       │<──Payment (CAPTURED)──────│      │
 │       │       │         │        │      │
 │       │───────────────Log Event───────────>│
 │       │       │         │        │      │
 │<─200 OK│       │         │        │      │
```

**Payment Failure with Compensation:**

```
User    API    Gateway    DB
 │       │       │        │
 │──Pay──>│       │        │
 │       │       │        │
 │       │──Reserve Payment>│
 │       │<──Payment (PENDING)
 │       │       │        │
 │       │──Charge>│       │
 │       │<──ERROR─│       │
 │       │       │        │
 │       │──Compensate────>│
 │       │  (Mark FAILED)  │
 │       │<──Updated───────│
 │       │       │        │
 │<─402──│       │        │
```

### Performance Optimizations

**1. Connection Pooling:**
```ruby
# Database connection pool
DATABASE_POOL = ConnectionPool.new(size: 100, timeout: 5) do
  ActiveRecord::Base.connection
end

# Redis connection pool
REDIS_POOL = ConnectionPool.new(size: 50, timeout: 1) do
  Redis.new(url: ENV['REDIS_URL'])
end

# Gateway client pool
GATEWAY_POOL = ConnectionPool.new(size: 20, timeout: 10) do
  Stripe::Client.new(api_key: ENV['STRIPE_API_KEY'])
end
```

**2. Caching Exchange Rates:**
```ruby
class CurrencyConverter
  CACHE_TTL = 300  # 5 minutes

  def get_exchange_rate(from_currency, to_currency)
    cache_key = "exchange_rate:#{from_currency}:#{to_currency}"

    Rails.cache.fetch(cache_key, expires_in: CACHE_TTL) do
      # Fetch from external API
      ExchangeRateAPI.get_rate(from_currency, to_currency)
    end
  end
end
```

**3. Batch Webhook Processing:**
```ruby
# Process webhooks in batches
class WebhookProcessor
  def process_batch(webhooks)
    Payment.transaction do
      webhooks.each do |webhook|
        payment = Payment.find_by(gateway_transaction_id: webhook[:transaction_id])
        payment&.update!(status: webhook[:status])
      end
    end
  end
end
```

**4. Read Replicas for Analytics:**
```ruby
# Use read replica for non-critical queries
class PaymentAnalytics
  def self.total_revenue(start_date, end_date)
    Payment.connection.execute(
      "SELECT SUM(amount) FROM payments WHERE created_at BETWEEN ? AND ?",
      start_date,
      end_date
    ).first['sum']
  end
end

# Configure read replica
ActiveRecord::Base.connected_to(role: :reading) do
  PaymentAnalytics.total_revenue(1.month.ago, Time.current)
end
```

**5. Async Audit Logging:**
```ruby
# Log audit events asynchronously
class AuditService
  def self.log_event(event_params)
    AuditLogJob.perform_later(event_params)
  end
end

class AuditLogJob < ApplicationJob
  queue_as :audit

  def perform(event_params)
    AuditEvent.create!(event_params)
  end
end
```

## Step-by-Step Request Flow

### Happy Path: Successful Payment

1. **User initiates payment**
   - Request: `POST /api/v1/payments`
   - Body: `{ amount: 100.00, currency: 'USD', payment_method: {...}, idempotency_key: 'uuid' }`
   - Routed to nearest region

2. **Idempotency check**
   ```ruby
   existing_payment = Payment.find_by(idempotency_key: params[:idempotency_key])
   return existing_payment if existing_payment
   ```

3. **Fraud detection**
   - Extract user metadata (IP, device fingerprint, location)
   - Call fraud detection service
   - Risk score: 0-100 (0 = safe, 100 = fraudulent)
   - If score > 80: Reject immediately
   - If score 50-80: Require 3D Secure
   - If score < 50: Proceed

4. **Currency conversion (if needed)**
   ```ruby
   if params[:currency] != merchant.settlement_currency
     exchange_rate = CurrencyService.get_rate(params[:currency], merchant.settlement_currency)
     settlement_amount = params[:amount] * exchange_rate
     # Lock rate for 5 minutes
     CurrencyService.lock_rate(payment_id, exchange_rate)
   end
   ```

5. **Create payment record (PENDING state)**
   ```sql
   INSERT INTO payments (
     id, user_id, merchant_id, amount, currency,
     status, idempotency_key, fraud_score, created_at
   ) VALUES (
     uuid_generate_v4(), 123, 456, 100.00, 'USD',
     'PENDING', 'idem_xyz', 25, NOW()
   );
   ```

6. **Call payment gateway**
   ```ruby
   gateway_response = PaymentGatewayOrchestrator.charge(
     amount: payment.amount,
     currency: payment.currency,
     payment_method: payment_method_token,
     idempotency_key: payment.idempotency_key
   )
   ```

7. **Update payment status**
   ```ruby
   if gateway_response.success?
     payment.update!(
       status: 'SUCCEEDED',
       gateway_transaction_id: gateway_response.transaction_id,
       gateway_name: gateway_response.gateway,
       completed_at: Time.current
     )
   else
     payment.update!(
       status: 'FAILED',
       failure_reason: gateway_response.error_message,
       failed_at: Time.current
     )
   end
   ```

8. **Publish events**
   ```ruby
   EventBus.publish('payment.succeeded', payment.to_event)
   # Triggers: Receipt generation, analytics, merchant notification
   ```

9. **Return response**
   ```json
   {
     "id": "pay_123",
     "status": "succeeded",
     "amount": 100.00,
     "currency": "USD",
     "created_at": "2024-01-15T10:30:00Z"
   }
   ```

### Failure Scenarios

**Scenario 1: Gateway timeout after charge succeeds**

Problem: Gateway charges card but times out before responding

Solution: Webhook reconciliation

```ruby
class PaymentWebhookController < ApplicationController
  def stripe_webhook
    event = Stripe::Webhook.construct_event(
      request.body.read,
      request.headers['Stripe-Signature'],
      ENV['STRIPE_WEBHOOK_SECRET']
    )

    case event.type
    when 'charge.succeeded'
      # Find payment by gateway transaction ID
      payment = Payment.find_by(
        gateway_transaction_id: event.data.object.id,
        status: 'PENDING'
      )

      if payment
        payment.update!(
          status: 'SUCCEEDED',
          completed_at: Time.current
        )
        EventBus.publish('payment.succeeded', payment.to_event)
      end
    end

    head :ok
  end
end

# Reconciliation job (runs every 5 minutes)
class PaymentReconciliationJob
  def perform
    # Find payments stuck in PENDING for > 5 minutes
    stuck_payments = Payment.where(
      status: 'PENDING',
      created_at: ..5.minutes.ago
    )

    stuck_payments.each do |payment|
      # Query gateway for actual status
      gateway_status = PaymentGatewayOrchestrator.get_status(
        payment.gateway_transaction_id
      )

      payment.update!(status: gateway_status)
    end
  end
end
```

**Scenario 2: Database failure after gateway charge**

Problem: Payment succeeds at gateway but DB update fails

Solution: Write-ahead log + retry

```ruby
class PaymentProcessor
  def process_payment(payment_params)
    # Write to WAL before calling gateway
    wal_entry = WriteAheadLog.create!(
      operation: 'payment_charge',
      payload: payment_params.to_json,
      status: 'PENDING'
    )

    begin
      # Call gateway
      gateway_response = PaymentGatewayOrchestrator.charge(payment_params)

      # Update database
      payment = Payment.create!(
        **payment_params,
        status: gateway_response.success? ? 'SUCCEEDED' : 'FAILED',
        gateway_transaction_id: gateway_response.transaction_id
      )

      # Mark WAL entry as complete
      wal_entry.update!(status: 'COMPLETED', payment_id: payment.id)

      payment
    rescue => e
      # Mark WAL entry as failed
      wal_entry.update!(
        status: 'FAILED',
        error_message: e.message,
        gateway_transaction_id: gateway_response&.transaction_id
      )

      # Retry later
      PaymentRetryJob.perform_later(wal_entry.id)
      raise
    end
  end
end

class PaymentRetryJob < ApplicationJob
  def perform(wal_entry_id)
    wal_entry = WriteAheadLog.find(wal_entry_id)

    # If gateway transaction ID exists, payment succeeded at gateway
    if wal_entry.gateway_transaction_id
      # Create payment record
      payment_params = JSON.parse(wal_entry.payload)
      Payment.create!(
        **payment_params,
        status: 'SUCCEEDED',
        gateway_transaction_id: wal_entry.gateway_transaction_id
      )

      wal_entry.update!(status: 'COMPLETED')
    else
      # Retry entire operation
      PaymentProcessor.new.process_payment(JSON.parse(wal_entry.payload))
    end
  end
end
```

**Scenario 3: Duplicate payment request**

Problem: User clicks "Pay" multiple times

Solution: Idempotency keys

```ruby
class PaymentsController < ApplicationController
  def create
    idempotency_key = request.headers['Idempotency-Key'] || params[:idempotency_key]

    raise ArgumentError, 'Idempotency key required' unless idempotency_key

    # Check for existing payment
    existing_payment = Payment.find_by(idempotency_key: idempotency_key)

    if existing_payment
      # Return existing payment (idempotent)
      render json: existing_payment, status: :ok
    else
      # Create new payment
      payment = PaymentProcessor.new.process_payment(
        **payment_params,
        idempotency_key: idempotency_key
      )

      render json: payment, status: :created
    end
  rescue ActiveRecord::RecordNotUnique
    # Race condition: Another request created payment with same key
    existing_payment = Payment.find_by!(idempotency_key: idempotency_key)
    render json: existing_payment, status: :ok
  end
end
```

## Data Model Design

### PostgreSQL Schema

```sql
-- Payments table (partitioned by created_at)
CREATE TABLE payments (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    user_id BIGINT NOT NULL,
    merchant_id BIGINT NOT NULL,
    amount DECIMAL(19,4) NOT NULL,  -- Support up to 4 decimal places
    currency VARCHAR(3) NOT NULL,   -- ISO 4217 currency code
    settlement_amount DECIMAL(19,4),
    settlement_currency VARCHAR(3),
    exchange_rate DECIMAL(19,8),
    status VARCHAR(50) NOT NULL,    -- PENDING, SUCCEEDED, FAILED, REFUNDED
    payment_method_type VARCHAR(50) NOT NULL,  -- card, wallet, bank_transfer
    payment_method_last4 VARCHAR(4),
    idempotency_key VARCHAR(255) UNIQUE NOT NULL,
    gateway_name VARCHAR(50),       -- stripe, paypal, adyen
    gateway_transaction_id VARCHAR(255),
    fraud_score INTEGER,            -- 0-100
    failure_reason TEXT,
    metadata JSONB,                 -- Additional data
    created_at TIMESTAMP NOT NULL DEFAULT NOW(),
    completed_at TIMESTAMP,
    failed_at TIMESTAMP,

    CONSTRAINT positive_amount CHECK (amount > 0),
    CONSTRAINT valid_status CHECK (status IN ('PENDING', 'SUCCEEDED', 'FAILED', 'REFUNDED', 'DISPUTED'))
) PARTITION BY RANGE (created_at);

-- Monthly partitions
CREATE TABLE payments_2024_01 PARTITION OF payments
    FOR VALUES FROM ('2024-01-01') TO ('2024-02-01');

CREATE INDEX idx_payments_user_id ON payments(user_id, created_at DESC);
CREATE INDEX idx_payments_merchant_id ON payments(merchant_id, created_at DESC);
CREATE INDEX idx_payments_status ON payments(status) WHERE status = 'PENDING';
CREATE INDEX idx_payments_gateway_txn ON payments(gateway_transaction_id);
CREATE INDEX idx_payments_idempotency ON payments(idempotency_key);

-- Refunds table
CREATE TABLE refunds (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    payment_id UUID REFERENCES payments(id) NOT NULL,
    amount DECIMAL(19,4) NOT NULL,
    currency VARCHAR(3) NOT NULL,
    reason VARCHAR(255),
    status VARCHAR(50) NOT NULL,  -- PENDING, SUCCEEDED, FAILED
    gateway_refund_id VARCHAR(255),
    idempotency_key VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP NOT NULL DEFAULT NOW(),
    completed_at TIMESTAMP,

    CONSTRAINT refund_amount_valid CHECK (amount > 0)
);

CREATE INDEX idx_refunds_payment_id ON refunds(payment_id);
CREATE INDEX idx_refunds_status ON refunds(status);

-- Payment events (audit trail)
CREATE TABLE payment_events (
    id BIGSERIAL PRIMARY KEY,
    payment_id UUID REFERENCES payments(id) NOT NULL,
    event_type VARCHAR(50) NOT NULL,  -- created, authorized, captured, failed, refunded
    event_data JSONB,
    created_at TIMESTAMP NOT NULL DEFAULT NOW()
) PARTITION BY RANGE (created_at);

CREATE INDEX idx_payment_events_payment_id ON payment_events(payment_id, created_at DESC);

-- Write-ahead log (for failure recovery)
CREATE TABLE write_ahead_log (
    id BIGSERIAL PRIMARY KEY,
    operation VARCHAR(50) NOT NULL,
    payload JSONB NOT NULL,
    status VARCHAR(50) NOT NULL,  -- PENDING, COMPLETED, FAILED
    payment_id UUID,
    gateway_transaction_id VARCHAR(255),
    error_message TEXT,
    created_at TIMESTAMP NOT NULL DEFAULT NOW(),
    updated_at TIMESTAMP NOT NULL DEFAULT NOW()
);

CREATE INDEX idx_wal_status ON write_ahead_log(status, created_at) WHERE status = 'PENDING';
```

### Data Residency Strategy

```ruby
# Route to correct database based on user location
class PaymentDatabaseRouter
  def self.db_for_user(user)
    case user.country_code
    when 'US', 'CA', 'MX'
      :us_east
    when *EU_COUNTRIES
      :eu_west
    when *APAC_COUNTRIES
      :ap_south
    else
      :us_east  # Default
    end
  end
end

# Usage
class Payment < ApplicationRecord
  connects_to database: { writing: :primary, reading: :replica }

  def self.create_for_user(user, payment_params)
    db = PaymentDatabaseRouter.db_for_user(user)

    connected_to(database: db) do
      create!(payment_params)
    end
  end
end
```

## Concurrency & Consistency Strategy

### Distributed Locking for Duplicate Prevention

```ruby
class PaymentProcessor
  def process_payment(payment_params)
    idempotency_key = payment_params[:idempotency_key]
    lock_key = "payment_lock:#{idempotency_key}"

    # Acquire distributed lock
    lock_acquired = redis.set(lock_key, SecureRandom.uuid, nx: true, ex: 30)

    unless lock_acquired
      # Another request is processing this payment
      sleep 0.1
      # Return existing payment
      return Payment.find_by!(idempotency_key: idempotency_key)
    end

    begin
      # Check again for existing payment (double-check locking)
      existing = Payment.find_by(idempotency_key: idempotency_key)
      return existing if existing

      # Process payment
      process_payment_internal(payment_params)
    ensure
      redis.del(lock_key)
    end
  end
end
```

### Saga Pattern for Refunds

```ruby
class RefundSaga
  def execute(payment_id, refund_amount)
    payment = Payment.find(payment_id)

    # Step 1: Create refund record
    refund = create_refund_record(payment, refund_amount)

    begin
      # Step 2: Call gateway to process refund
      gateway_response = call_gateway_refund(payment, refund_amount)

      # Step 3: Update refund status
      refund.update!(
        status: 'SUCCEEDED',
        gateway_refund_id: gateway_response.refund_id,
        completed_at: Time.current
      )

      # Step 4: Update payment status if fully refunded
      update_payment_status(payment, refund)

      # Step 5: Publish event
      EventBus.publish('refund.succeeded', refund.to_event)

      refund
    rescue => e
      # Compensation: Mark refund as failed
      refund.update!(status: 'FAILED', error_message: e.message)

      # Retry later
      RefundRetryJob.perform_later(refund.id)
      raise
    end
  end

  private

  def create_refund_record(payment, amount)
    Refund.create!(
      payment_id: payment.id,
      amount: amount,
      currency: payment.currency,
      status: 'PENDING',
      idempotency_key: SecureRandom.uuid
    )
  end

  def call_gateway_refund(payment, amount)
    gateway = PaymentGatewayOrchestrator.gateway_for(payment.gateway_name)
    gateway.refund(
      transaction_id: payment.gateway_transaction_id,
      amount: amount,
      idempotency_key: refund.idempotency_key
    )
  end

  def update_payment_status(payment, refund)
    total_refunded = payment.refunds.where(status: 'SUCCEEDED').sum(:amount)

    if total_refunded >= payment.amount
      payment.update!(status: 'REFUNDED')
    end
  end
end
```

## Ruby Implementation Examples

### Payment Gateway Orchestrator

```ruby
class PaymentGatewayOrchestrator
  GATEWAYS = {
    stripe: StripeGateway,
    paypal: PayPalGateway,
    adyen: AdyenGateway
  }.freeze

  def self.charge(payment_params)
    # Select gateway based on priority and availability
    gateway = select_gateway(payment_params)

    # Attempt charge with retry
    attempt_charge_with_retry(gateway, payment_params)
  rescue => e
    # Failover to backup gateway
    backup_gateway = select_backup_gateway(gateway)
    attempt_charge_with_retry(backup_gateway, payment_params)
  end

  private

  def self.select_gateway(payment_params)
    # Priority: Stripe > PayPal > Adyen
    # Check circuit breaker status
    [:stripe, :paypal, :adyen].each do |gateway_name|
      gateway = GATEWAYS[gateway_name].new

      unless circuit_breaker_open?(gateway_name)
        return gateway
      end
    end

    raise 'All payment gateways unavailable'
  end

  def self.attempt_charge_with_retry(gateway, payment_params, max_attempts: 3)
    attempts = 0

    begin
      attempts += 1
      gateway.charge(payment_params)
    rescue GatewayTimeoutError => e
      if attempts < max_attempts
        sleep(2 ** attempts)  # Exponential backoff
        retry
      else
        raise
      end
    rescue GatewayError => e
      record_gateway_failure(gateway.name)
      raise
    end
  end

  def self.circuit_breaker_open?(gateway_name)
    failures = redis.get("gateway_failures:#{gateway_name}").to_i
    failures >= 5
  end

  def self.record_gateway_failure(gateway_name)
    redis.incr("gateway_failures:#{gateway_name}")
    redis.expire("gateway_failures:#{gateway_name}", 60)
  end
end
```

### Fraud Detection Service

```ruby
class FraudDetectionService
  def calculate_risk_score(payment_params, user_context)
    score = 0

    # Velocity check: Multiple payments in short time
    recent_payments = Payment.where(
      user_id: payment_params[:user_id],
      created_at: 5.minutes.ago..Time.current
    ).count

    score += 20 if recent_payments > 3
    score += 40 if recent_payments > 5

    # Geolocation check: Payment from unusual location
    if unusual_location?(user_context[:ip_address], payment_params[:user_id])
      score += 30
    end

    # Amount check: Unusually large payment
    avg_payment = calculate_average_payment(payment_params[:user_id])
    if payment_params[:amount] > avg_payment * 5
      score += 25
    end

    # Device fingerprint check
    if new_device?(user_context[:device_fingerprint], payment_params[:user_id])
      score += 15
    end

    # ML model prediction
    ml_score = call_ml_model(payment_params, user_context)
    score += ml_score

    # Cap at 100
    [score, 100].min
  end

  private

  def unusual_location?(ip_address, user_id)
    location = GeoIP.lookup(ip_address)

    recent_locations = Payment.where(
      user_id: user_id,
      created_at: 30.days.ago..Time.current
    ).pluck(:ip_country).uniq

    !recent_locations.include?(location.country_code)
  end

  def calculate_average_payment(user_id)
    Payment.where(
      user_id: user_id,
      status: 'SUCCEEDED',
      created_at: 90.days.ago..Time.current
    ).average(:amount) || 0
  end

  def new_device?(device_fingerprint, user_id)
    !Payment.exists?(
      user_id: user_id,
      metadata: { device_fingerprint: device_fingerprint }
    )
  end

  def call_ml_model(payment_params, user_context)
    # Call ML service (e.g., SageMaker endpoint)
    response = HTTP.post(
      ENV['ML_FRAUD_DETECTION_ENDPOINT'],
      json: {
        amount: payment_params[:amount],
        currency: payment_params[:currency],
        user_id: payment_params[:user_id],
        ip_address: user_context[:ip_address],
        device_fingerprint: user_context[:device_fingerprint]
      }
    )

    response.parse['risk_score']
  end
end
```

### Currency Conversion Service

```ruby
class CurrencyConversionService
  def get_rate(from_currency, to_currency)
    # Check cache first (1-minute TTL)
    cache_key = "exchange_rate:#{from_currency}:#{to_currency}"

    Rails.cache.fetch(cache_key, expires_in: 1.minute) do
      fetch_rate_from_provider(from_currency, to_currency)
    end
  end

  def lock_rate(payment_id, exchange_rate)
    # Lock rate for 5 minutes to prevent rate fluctuation during payment
    redis.setex("locked_rate:#{payment_id}", 300, exchange_rate.to_s)
  end

  def get_locked_rate(payment_id)
    rate = redis.get("locked_rate:#{payment_id}")
    rate&.to_f
  end

  private

  def fetch_rate_from_provider(from_currency, to_currency)
    # Call external API (e.g., OpenExchangeRates, XE)
    response = HTTP.get(
      "https://api.exchangerate.host/latest",
      params: {
        base: from_currency,
        symbols: to_currency
      }
    )

    data = response.parse
    data['rates'][to_currency]
  end
end
```

## Scaling Strategy

### Horizontal Scaling

**API Servers:**
- Auto-scale based on request rate
- Minimum: 10 instances per region
- Maximum: 100 instances per region

**Database:**
- Primary-replica setup per region
- 1 primary + 3 read replicas
- Partition by created_at (monthly partitions)

### Vertical Scaling

**PostgreSQL:**
- Instance type: r6g.4xlarge (128 GB RAM)
- Reason: Large transaction volume, complex queries

### Sharding Strategy

```ruby
# Shard by merchant_id for merchant-specific queries
class Payment < ApplicationRecord
  def self.shard_key(merchant_id)
    merchant_id % 10  # 10 shards
  end

  def self.for_merchant(merchant_id)
    shard = shard_key(merchant_id)
    connected_to(shard: "shard_#{shard}") do
      where(merchant_id: merchant_id)
    end
  end
end
```

## High Availability Strategy

### Multi-AZ Deployment

```
Region: US-EAST-1

AZ-1a:                    AZ-1b:                    AZ-1c:
- API Servers (5)         - API Servers (5)         - API Servers (5)
- PostgreSQL Primary      - PostgreSQL Replica      - PostgreSQL Replica
- Redis Primary           - Redis Replica           - Redis Replica
```

### Automatic Failover

```ruby
# Database failover with Patroni
# Automatic promotion of replica to primary
# RTO: 30 seconds

# Application-level retry
class PaymentProcessor
  def process_payment_with_failover(payment_params)
    process_payment(payment_params)
  rescue PG::ConnectionBad, PG::UnableToSend
    # Wait for failover
    sleep 5
    retry
  end
end
```

## Observability & Monitoring

### Key Metrics

```ruby
class PaymentMetrics
  def self.record_payment(payment, latency_ms)
    StatsD.increment('payment.processed',
      tags: [
        "status:#{payment.status}",
        "gateway:#{payment.gateway_name}",
        "currency:#{payment.currency}"
      ])

    StatsD.histogram('payment.latency', latency_ms,
      tags: ["gateway:#{payment.gateway_name}"])

    StatsD.histogram('payment.amount', payment.amount,
      tags: ["currency:#{payment.currency}"])

    if payment.status == 'FAILED'
      StatsD.increment('payment.failed',
        tags: ["reason:#{payment.failure_reason}"])
    end
  end
end
```

### Alerting

```yaml
alerts:
  - name: HighPaymentFailureRate
    condition: payment.failed / payment.processed > 0.05
    duration: 5m
    severity: critical

  - name: PaymentGatewayDown
    condition: gateway_failures > 10
    duration: 1m
    severity: critical

  - name: HighFraudScore
    condition: avg(fraud_score) > 60
    duration: 10m
    severity: warning
```

## Testing Strategy

### Unit Tests

```ruby
RSpec.describe PaymentProcessor do
  describe '#process_payment' do
    it 'creates payment with SUCCEEDED status' do
      payment_params = {
        user_id: 123,
        amount: 100.00,
        currency: 'USD',
        idempotency_key: 'test_key'
      }

      payment = described_class.new.process_payment(payment_params)

      expect(payment.status).to eq('SUCCEEDED')
      expect(payment.amount).to eq(100.00)
    end

    it 'is idempotent' do
      payment_params = {
        user_id: 123,
        amount: 100.00,
        currency: 'USD',
        idempotency_key: 'test_key'
      }

      payment1 = described_class.new.process_payment(payment_params)
      payment2 = described_class.new.process_payment(payment_params)

      expect(payment1.id).to eq(payment2.id)
    end
  end
end
```

## Trade-offs & Alternatives

### Chosen: Regional Databases

**Pros:**
- Data residency compliance
- Lower latency
- Regional independence

**Cons:**
- Complex cross-region queries
- Data duplication for analytics

**Decision:** Regional databases with async replication for analytics

---

### Cost Considerations

**Infrastructure (per region):**
- PostgreSQL: $2000/month
- API Servers: $3000/month
- Redis: $500/month

**Total (3 regions):** ~$16,500/month
**Transaction cost:** $0.001 per transaction
