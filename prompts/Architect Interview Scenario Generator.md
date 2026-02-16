# Architect Interview Scenario Generator Prompt

## Objective

Generate multiple advanced, real-world system design scenarios suitable for Architect / Principal Engineer level interviews.

Each scenario must be created as a separate Markdown file inside:

```
/scenarios
```

Each file should contain a complete end-to-end architecture design with diagrams, failure handling, scaling strategy, consistency decisions, and Ruby-based implementation examples.

---

# Instructions for the Agent

You are a Senior Principal Architect designing production-grade distributed systems.

Your task:

1. Create at least 10 advanced architecture interview scenarios.
2. Create one `.md` file per scenario.
3. Use lowercase kebab-case file naming:

```
/scenarios/<problem-name>.md
```

Example:

```
/scenarios/flash-sale-system.md
/scenarios/distributed-rate-limiter.md
/scenarios/multi-region-payment-system.md
```

---

# Required Structure for Every Scenario File

Each file MUST follow this structure strictly.

---

# 1. Title

Clear system design problem title.

---

# 2. Problem Statement

Include:

* Real-world context
* Scale numbers (QPS, users, data size)
* Business constraints
* Failure expectations
* Edge cases
* Regulatory or compliance constraints (if relevant)

---

# 3. Functional Requirements

Bullet list of all required features.

---

# 4. Non-Functional Requirements

Include:

* Availability target (e.g., 99.99%)
* Latency expectations
* Throughput requirements
* Consistency model
* Durability requirements
* Security expectations
* Cost awareness (if relevant)

---

# 5. Core Engineering Challenges

Explain what makes the problem difficult:

* Concurrency issues
* Race conditions
* Distributed locking
* Cache stampede
* Idempotency
* Event ordering
* Cross-region replication
* CAP tradeoffs
* Partial failures
* Thundering herd

---

# 6. High-Level Architecture (ASCII Diagram Required)

Use ASCII diagrams only. Example format:

```
Users
  │
  ▼
CDN
  │
  ▼
Load Balancer
  │
  ▼
API Gateway
  │
  ▼
Microservices
  ├── Service A
  ├── Service B
  └── Service C
```

Explain each layer and what problem it eliminates.

---

# 7. Step-by-Step Request Flow

Explain:

* Request lifecycle
* Failure handling at each step
* Retry logic
* Timeouts
* Backpressure handling
* What happens during partial system failure

---

# 8. Data Model Design

Include:

* Database schema
* Indexing strategy
* Partitioning / sharding strategy
* Read vs write path
* Storage engine decisions

Use SQL examples where applicable.

---

# 9. Concurrency & Consistency Strategy

Explain:

* Optimistic vs pessimistic locking
* Distributed locks (if applicable)
* Idempotency key strategy
* Retry + exponential backoff
* Strong vs eventual consistency
* Trade-offs chosen

---

# 10. Ruby Implementation Examples

Use Ruby code to demonstrate core distributed concepts.

Examples may include:

* Redis locking
* Circuit breaker implementation
* Retry with exponential backoff
* Saga pattern
* Background job processing
* Transaction handling
* Idempotent API handling
* Event publishing

Code must:

* Be production-style
* Include comments explaining reasoning
* Avoid pseudo-code where possible

---

# 11. Scaling Strategy

Explain:

* Horizontal scaling
* Vertical scaling
* Autoscaling triggers
* Database scaling
* Read replicas
* Caching layers
* Queue scaling
* Worker scaling

---

# 12. High Availability Strategy

Cover:

* Multi-AZ deployment
* Multi-region deployment
* Active-active vs active-passive
* Health checks
* Circuit breakers
* Graceful degradation
* Backpressure handling

---

# 13. Failsafe & Rollback Strategy

Explain clearly:

* What happens if DB commit fails after payment succeeds
* Compensation mechanism
* Reconciliation jobs
* Dead-letter queue handling
* Lock expiry edge cases

---

# 14. Zero Downtime Deployment Strategy

Include:

* Blue-green deployment
* Rolling updates
* Schema migration strategy
* Backward compatibility
* Feature flags
* Safe rollback

---

# 15. Observability & Monitoring

Include:

* Metrics (QPS, latency, error rate)
* Distributed tracing
* Structured logging
* Alert thresholds
* SLIs / SLOs

---

# 16. Testing Strategy

Cover:

* Unit tests
* Integration tests
* Load testing
* Chaos testing
* Failure injection
* Data consistency tests

Include small Ruby test examples if relevant.

---

# 17. Trade-offs & Alternatives

Explain:

* What was chosen
* What was rejected
* Why
* Operational cost considerations
* Complexity trade-offs

---

# Quality Requirements

* Architect-level depth
* No shallow explanations
* Failure-aware design
* Explicit trade-off reasoning
* Clear elimination of bottlenecks
* No fluff
* Production-ready thinking

---

# Optional: Create Index File

Create:

```
/scenarios/README.md
```

Include:

* List of all scenarios
* Short description (2–3 lines each)
* Difficulty level
* Core distributed system topics covered

---

# End Goal

The `/scenarios` directory should become a complete Architect-level system design preparation repository containing:

* Deep distributed system challenges
* End-to-end solutions
* Ruby implementation samples
* Scaling strategies
* Failure recovery patterns
* High-availability strategies
* Consistency trade-off discussions

This repository should be suitable for preparing for Staff / Principal / Architect interviews at high-scale product com
