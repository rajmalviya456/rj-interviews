# Distributed Job Scheduler

## Problem Statement

Design a distributed job scheduling system that can execute millions of scheduled tasks reliably across a cluster of workers with exactly-once execution guarantees.

**Scale Requirements:**
- 10 million scheduled jobs
- 100,000 jobs executed per minute
- Support for one-time and recurring jobs
- Job execution latency: < 5 seconds from scheduled time
- Support for cron-like schedules
- Global deployment across 5 regions

**Business Constraints:**
- Exactly-once execution (no duplicate runs)
- No missed executions
- Support job dependencies (DAG execution)
- Job retry with exponential backoff
- Dead letter queue for failed jobs
- Job priority levels
- Support for long-running jobs (hours)
- Job cancellation support

**Failure Expectations:**
- Worker failures must not lose jobs
- Scheduler failures must not cause duplicate execution
- Network partitions must not cause job loss
- Database failures must be recoverable

**Edge Cases:**
- Clock skew across distributed workers
- Job scheduled in the past
- Overlapping recurring job executions
- Worker crashes mid-execution
- Job execution time exceeds schedule interval
- Concurrent job cancellation requests

## Functional Requirements

- Schedule one-time jobs at specific time
- Schedule recurring jobs (cron syntax)
- Execute jobs with exactly-once guarantee
- Support job dependencies (run job B after job A)
- Retry failed jobs with configurable strategy
- Cancel scheduled jobs
- Pause/resume job execution
- Query job status and history
- Support job priorities
- Provide job execution logs
- Support job timeouts
- Handle job failures gracefully

## Non-Functional Requirements

- **Availability:** 99.99%
- **Latency:** Jobs execute within 5 seconds of scheduled time
- **Throughput:** 100K jobs/minute
- **Consistency:** Exactly-once execution
- **Durability:** Zero job loss
- **Scalability:** Support 10M+ scheduled jobs
- **Reliability:** 99.9% successful execution rate

## Core Engineering Challenges

1. **Exactly-Once Execution**
   - Preventing duplicate execution on worker failure
   - Handling scheduler failover
   - Idempotency guarantees
   - Distributed locking

2. **Time-Based Scheduling**
   - Clock synchronization across workers
   - Handling clock skew
   - Efficient time-based queries
   - Cron expression parsing

3. **High Throughput**
   - 100K jobs/minute = 1666 jobs/second
   - Efficient job polling
   - Worker coordination
   - Queue management

4. **Job Dependencies**
   - DAG execution
   - Handling circular dependencies
   - Partial failure recovery
   - Dependency tracking

5. **Worker Coordination**
   - Job distribution across workers
   - Load balancing
   - Worker health monitoring
   - Graceful shutdown

6. **Failure Recovery**
   - Worker crash recovery
   - Job state recovery
   - Orphaned job detection
   - Retry logic

## High-Level Design (HLD)

### System Architecture Overview

The distributed job scheduler follows a **leader-follower pattern** with the following key components:

1. **Scheduler Cluster** - Multiple scheduler instances with leader election
2. **Message Queue** - Decouples scheduling from execution
3. **Worker Pool** - Horizontally scalable job executors
4. **Persistent Storage** - PostgreSQL for job state
5. **Distributed Coordination** - Redis for locks and leader election

### Architecture Diagram

```
                            Job Schedulers
                                  │
                                  ▼
                          Scheduler Cluster
                          (Leader Election)
                                  │
                    ┌─────────────┼─────────────┐
                    ▼             ▼             ▼
              Scheduler 1   Scheduler 2   Scheduler 3
              (Leader)      (Standby)     (Standby)
                    │
                    ▼
              Job Enqueuer
              (Polls DB for due jobs)
                    │
                    ▼
              Message Queue
              (RabbitMQ/SQS)
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
    Worker 1    Worker 2    Worker 3
    (Executor)  (Executor)  (Executor)
        │           │           │
        └───────────┼───────────┘
                    │
                    ▼
              PostgreSQL
              (Job State)
                    │
                    ▼
              Redis
              (Distributed Locks)
```

### Component Responsibilities

**1. Scheduler Cluster:**
- Leader election using Redis
- Poll database for due jobs (leader only)
- Enqueue jobs to message queue
- Handle scheduler failover

**2. Job Enqueuer:**
- Query jobs with `next_run_at <= NOW()`
- Acquire distributed lock per job
- Publish to message queue
- Update job status to QUEUED

**3. Message Queue:**
- Durable message storage
- Load balancing across workers
- Message acknowledgment
- Dead letter queue for failures

**4. Worker Pool:**
- Consume jobs from queue
- Acquire execution lock
- Execute job logic
- Update job status
- Handle retries and failures

**5. PostgreSQL:**
- Source of truth for job state
- Job definitions and schedules
- Execution history
- Dependency tracking

**6. Redis:**
- Distributed locks (job execution)
- Leader election
- Idempotency tracking
- Worker heartbeats

### Data Flow

```
1. Job Creation
   API → PostgreSQL (INSERT job)

2. Job Scheduling
   Scheduler (Leader) → PostgreSQL (SELECT due jobs)
   → Redis (acquire lock)
   → Message Queue (PUBLISH)
   → PostgreSQL (UPDATE status=QUEUED)

3. Job Execution
   Worker → Message Queue (CONSUME)
   → Redis (acquire execution lock)
   → Execute Job Logic
   → PostgreSQL (UPDATE status=COMPLETED)
   → Message Queue (ACK)

4. Job Retry (on failure)
   Worker → PostgreSQL (UPDATE attempt_number, next_run_at)
   → Scheduler picks up again
```

### Scalability Strategy

**Horizontal Scaling:**
- Workers: Scale based on queue depth
- Schedulers: Fixed 3-5 instances (only leader active)
- Database: Read replicas for queries

**Vertical Scaling:**
- Database: Increase resources for large job tables
- Redis: Increase memory for more locks

**Partitioning:**
- Jobs table: Partition by created_at (monthly)
- Execution history: Partition by executed_at

### Failure Handling

**Scheduler Failure:**
- Automatic leader re-election
- Standby scheduler becomes leader
- RTO: < 10 seconds

**Worker Failure:**
- Job remains in queue (not ACKed)
- Requeued automatically
- Orphaned job detector recovers stuck jobs

**Database Failure:**
- Read replicas for failover
- Jobs in queue continue executing
- New scheduling paused until recovery

**Message Queue Failure:**
- Jobs remain in database
- Scheduler retries enqueue
- Workers reconnect automatically

## Low-Level Design (LLD)

### Class Diagram

```
┌─────────────────────────┐
│   JobSchedulerService   │
├─────────────────────────┤
│ - redis: Redis          │
│ - scheduler_id: String  │
├─────────────────────────┤
│ + run()                 │
│ + poll_and_enqueue()    │
│ - enqueue_job(job)      │
└─────────────────────────┘
            │
            │ uses
            ▼
┌─────────────────────────┐
│ SchedulerLeaderElection │
├─────────────────────────┤
│ - redis: Redis          │
│ - scheduler_id: String  │
├─────────────────────────┤
│ + acquire_leadership()  │
│ + run_as_leader()       │
│ - renew_leadership()    │
└─────────────────────────┘

┌─────────────────────────┐
│      JobWorker          │
├─────────────────────────┤
│ - worker_id: String     │
│ - redis: Redis          │
│ - running: Boolean      │
├─────────────────────────┤
│ + start()               │
│ + stop()                │
│ - process_jobs()        │
│ - register_worker()     │
│ - start_heartbeat()     │
└─────────────────────────┘
            │
            │ uses
            ▼
┌─────────────────────────┐
│      JobExecutor        │
├─────────────────────────┤
│ - redis: Redis          │
│ - worker_id: String     │
├─────────────────────────┤
│ + execute_with_lock()   │
│ - execute_job_logic()   │
│ - release_lock_safely() │
└─────────────────────────┘

┌─────────────────────────┐
│   JobRetryHandler       │
├─────────────────────────┤
│ - worker_id: String     │
├─────────────────────────┤
│ + handle_failure()      │
│ - calculate_backoff()   │
└─────────────────────────┘

┌─────────────────────────┐
│ JobDependencyResolver   │
├─────────────────────────┤
│ + can_execute?(job)     │
│ + execute_with_deps()   │
│ - trigger_dependent()   │
└─────────────────────────┘
```

### Database Schema Details

**Jobs Table:**
```sql
CREATE TABLE jobs (
    id UUID PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    schedule VARCHAR(255),           -- Cron expression
    payload JSONB NOT NULL,
    status VARCHAR(50) NOT NULL,     -- State machine
    priority INTEGER DEFAULT 0,      -- Higher = more important
    timeout_seconds INTEGER,
    max_attempts INTEGER DEFAULT 3,
    attempt_number INTEGER DEFAULT 0,
    next_run_at TIMESTAMP,           -- Indexed for polling
    queued_at TIMESTAMP,
    started_at TIMESTAMP,
    completed_at TIMESTAMP,
    execution_time_ms INTEGER,
    failure_reason TEXT,
    created_at TIMESTAMP NOT NULL,
    updated_at TIMESTAMP NOT NULL
);

-- Critical index for scheduler polling
CREATE INDEX idx_jobs_next_run
ON jobs(status, next_run_at)
WHERE status = 'SCHEDULED';

-- Index for status queries
CREATE INDEX idx_jobs_status
ON jobs(status, created_at DESC);
```

**Job State Machine:**
```
SCHEDULED → QUEUED → RUNNING → COMPLETED
    ↓          ↓         ↓
    └──────────┴─────────┴──→ FAILED → SCHEDULED (retry)
                                  ↓
                              DEAD_LETTER (max attempts)

CANCELLED (can transition from any state)
WAITING_DEPENDENCIES (blocked on other jobs)
```

### API Endpoints

**Job Management API:**

```ruby
# Create job
POST /api/v1/jobs
{
  "name": "send_report",
  "schedule": "0 9 * * *",  # Cron
  "payload": { "report_type": "sales" },
  "timeout_seconds": 3600,
  "max_attempts": 3,
  "priority": 5
}

Response: 201 Created
{
  "id": "job_123",
  "status": "scheduled",
  "next_run_at": "2024-01-16T09:00:00Z"
}

# Get job status
GET /api/v1/jobs/:id

Response: 200 OK
{
  "id": "job_123",
  "name": "send_report",
  "status": "completed",
  "attempt_number": 1,
  "execution_time_ms": 1234,
  "completed_at": "2024-01-16T09:00:01Z"
}

# Cancel job
DELETE /api/v1/jobs/:id

Response: 200 OK
{
  "id": "job_123",
  "status": "cancelled"
}

# List jobs
GET /api/v1/jobs?status=scheduled&limit=100

Response: 200 OK
{
  "jobs": [...],
  "total": 1500,
  "page": 1
}
```

### Algorithms

**1. Leader Election Algorithm:**

```ruby
# Redis-based leader election with TTL
def acquire_leadership
  loop do
    # Try to set leader key with NX (only if not exists)
    became_leader = redis.set(
      LEADER_KEY,
      scheduler_id,
      nx: true,      # Only set if not exists
      ex: LEADER_TTL # Expire in 10 seconds
    )

    if became_leader
      run_as_leader
    else
      sleep 5  # Wait before retry
    end
  end
end

def run_as_leader
  loop do
    # Renew leadership before TTL expires
    renewed = redis.set(
      LEADER_KEY,
      scheduler_id,
      xx: true,      # Only set if exists
      ex: LEADER_TTL
    )

    break unless renewed  # Lost leadership

    poll_and_enqueue_jobs
    sleep 1
  end
end
```

**2. Job Polling Algorithm:**

```ruby
def poll_and_enqueue_jobs
  # Query with limit to prevent overwhelming system
  due_jobs = Job.where(
    status: 'SCHEDULED',
    next_run_at: ..Time.current
  ).order(priority: :desc, next_run_at: :asc)
   .limit(1000)

  due_jobs.each do |job|
    # Acquire lock to prevent duplicate enqueue
    lock_key = "job_enqueue_lock:#{job.id}"

    lock_acquired = redis.set(
      lock_key,
      scheduler_id,
      nx: true,
      ex: 60
    )

    next unless lock_acquired

    begin
      # Double-check job status (may have changed)
      job.reload
      next unless job.status == 'SCHEDULED'

      # Enqueue to message queue
      JobQueue.publish(job.to_message)

      # Update status atomically
      job.update!(
        status: 'QUEUED',
        queued_at: Time.current
      )
    ensure
      redis.del(lock_key)
    end
  end
end
```

**3. Exactly-Once Execution Algorithm:**

```ruby
def execute_with_lock(job)
  lock_key = "job_execution:#{job.id}"
  lock_token = SecureRandom.uuid

  # Acquire execution lock
  lock_acquired = redis.set(
    lock_key,
    lock_token,
    nx: true,
    ex: job.timeout_seconds
  )

  return unless lock_acquired

  begin
    # Update status to RUNNING
    job.update!(
      status: 'RUNNING',
      started_at: Time.current,
      attempt_number: job.attempt_number + 1
    )

    # Execute job
    result = execute_job_logic(job)

    # Update status to COMPLETED
    job.update!(
      status: 'COMPLETED',
      completed_at: Time.current,
      execution_time_ms: calculate_duration_ms
    )

  rescue => e
    handle_failure(job, e)
  ensure
    # Release lock using Lua script (atomic check-and-delete)
    release_lock_safely(lock_key, lock_token)
  end
end

def release_lock_safely(lock_key, lock_token)
  lua_script = <<~LUA
    if redis.call('GET', KEYS[1]) == ARGV[1] then
      return redis.call('DEL', KEYS[1])
    end
    return 0
  LUA

  redis.eval(lua_script, keys: [lock_key], argv: [lock_token])
end
```

**4. Exponential Backoff Algorithm:**

```ruby
def calculate_backoff(attempt_number)
  # Base delay: 2^attempt seconds
  base_delay = 2 ** attempt_number

  # Cap at 1 hour
  base_delay = [base_delay, 3600].min

  # Add jitter (0-10% of base delay)
  jitter = rand(0..(base_delay * 0.1))

  base_delay + jitter
end

# Examples:
# Attempt 1: 2s + jitter
# Attempt 2: 4s + jitter
# Attempt 3: 8s + jitter
# Attempt 4: 16s + jitter
# Attempt 10: 1024s → capped at 3600s
```

**5. Orphaned Job Detection Algorithm:**

```ruby
def detect_orphaned_jobs
  # Find jobs stuck in RUNNING state
  orphaned_jobs = Job.where(
    status: 'RUNNING',
    started_at: ..10.minutes.ago
  )

  orphaned_jobs.each do |job|
    lock_key = "job_execution:#{job.id}"

    # Check if execution lock still exists
    if redis.exists?(lock_key)
      # Job still running, skip
      next
    else
      # Job orphaned (worker crashed)
      Rails.logger.warn("Orphaned job detected: #{job.id}")

      # Mark as failed
      job.update!(
        status: 'FAILED',
        failure_reason: 'Worker crashed or timed out'
      )

      # Retry if attempts remaining
      retry_job(job) if job.attempt_number < job.max_attempts
    end
  end
end
```

### Sequence Diagrams

**Job Execution Flow:**

```
User          API         Scheduler      Queue       Worker      Database      Redis
 │             │              │            │           │            │            │
 │─POST job───>│              │            │           │            │            │
 │             │─INSERT──────>│            │           │            │            │
 │             │<─job_id──────│            │           │            │            │
 │<─201────────│              │            │           │            │            │
 │             │              │            │           │            │            │
 │             │              │─SELECT due jobs────────>│            │            │
 │             │              │<─jobs────────────────────│            │            │
 │             │              │                         │            │            │
 │             │              │─────────────────────────────────────>│─SET lock──>│
 │             │              │<────────────────────────────────────────lock OK───│
 │             │              │                         │            │            │
 │             │              │─PUBLISH────>│           │            │            │
 │             │              │─UPDATE status=QUEUED───>│            │            │
 │             │              │            │            │            │            │
 │             │              │            │<─CONSUME───│            │            │
 │             │              │            │            │            │            │
 │             │              │            │            │───────────────SET lock─>│
 │             │              │            │            │<──────────────lock OK───│
 │             │              │            │            │            │            │
 │             │              │            │            │─UPDATE status=RUNNING──>│
 │             │              │            │            │            │            │
 │             │              │            │            │─Execute Job Logic       │
 │             │              │            │            │            │            │
 │             │              │            │            │─UPDATE status=COMPLETED>│
 │             │              │            │            │            │            │
 │             │              │            │            │───────────────DEL lock─>│
 │             │              │            │<─ACK───────│            │            │
```

### Performance Optimizations

**1. Batch Job Polling:**
```ruby
# Poll 1000 jobs at once instead of one-by-one
due_jobs = Job.where(...).limit(1000)
```

**2. Connection Pooling:**
```ruby
# Reuse database connections
ActiveRecord::Base.connection_pool.size = 100
```

**3. Prepared Statements:**
```ruby
# Use prepared statements for frequent queries
Job.connection.exec_query(
  "SELECT * FROM jobs WHERE status = $1 AND next_run_at <= $2",
  "Job Poll",
  [[nil, 'SCHEDULED'], [nil, Time.current]]
)
```

**4. Index Optimization:**
```sql
-- Partial index for active jobs only
CREATE INDEX idx_jobs_next_run
ON jobs(status, next_run_at)
WHERE status = 'SCHEDULED';
```

**5. Redis Pipelining:**
```ruby
# Batch Redis commands
redis.pipelined do
  jobs.each do |job|
    redis.set("lock:#{job.id}", worker_id, nx: true, ex: 60)
  end
end
```

## Step-by-Step Request Flow

### Job Scheduling Flow

1. **User schedules a job**
   ```
   POST /api/v1/jobs
   {
     "name": "send_daily_report",
     "schedule": "0 9 * * *",  // Daily at 9 AM
     "payload": { "report_type": "sales" },
     "retry_policy": { "max_attempts": 3, "backoff": "exponential" }
   }
   ```

2. **Validate schedule**
   ```ruby
   cron = Fugit::Cron.parse(params[:schedule])
   raise InvalidScheduleError unless cron

   next_run = cron.next_time
   ```

3. **Create job record**
   ```sql
   INSERT INTO jobs (
     id, name, schedule, payload, status, next_run_at, created_at
   ) VALUES (
     uuid_generate_v4(), 'send_daily_report', '0 9 * * *',
     '{"report_type":"sales"}', 'SCHEDULED', '2024-01-16 09:00:00', NOW()
   );
   ```

4. **Return job ID**
   ```json
   {
     "id": "job_123",
     "status": "scheduled",
     "next_run_at": "2024-01-16T09:00:00Z"
   }
   ```

### Job Execution Flow

1. **Scheduler polls for due jobs (every 1 second)**
   ```ruby
   due_jobs = Job.where(
     status: 'SCHEDULED',
     next_run_at: ..Time.current
   ).limit(1000)
   ```

2. **Enqueue jobs to message queue**
   ```ruby
   due_jobs.each do |job|
     # Acquire lock to prevent duplicate enqueue
     lock_key = "job_lock:#{job.id}"
     lock_acquired = redis.set(lock_key, worker_id, nx: true, ex: 60)

     next unless lock_acquired

     # Enqueue job
     JobQueue.publish(job.to_message)

     # Update status
     job.update!(status: 'QUEUED', queued_at: Time.current)
   end
   ```

3. **Worker picks up job from queue**
   ```ruby
   message = JobQueue.consume
   job_data = JSON.parse(message.body)
   ```

4. **Execute job with exactly-once guarantee**
   ```ruby
   execution_lock_key = "job_execution:#{job_data['id']}"
   lock_token = SecureRandom.uuid

   # Acquire execution lock
   lock_acquired = redis.set(
     execution_lock_key,
     lock_token,
     nx: true,
     ex: job_data['timeout'] || 3600
   )

   return unless lock_acquired

   begin
     # Execute job
     execute_job(job_data)

     # Mark as completed
     Job.find(job_data['id']).update!(
       status: 'COMPLETED',
       completed_at: Time.current
     )

     # Schedule next run if recurring
     schedule_next_run(job_data['id']) if job_data['schedule']
   rescue => e
     handle_job_failure(job_data['id'], e)
   ensure
     # Release lock
     release_lock(execution_lock_key, lock_token)
   end
   ```

5. **Update job status**
   ```ruby
   job.update!(
     status: 'COMPLETED',
     completed_at: Time.current,
     execution_time_ms: execution_time
   )
   ```

### Failure Scenarios

**Scenario 1: Worker crashes mid-execution**

Solution: Orphaned job detection

```ruby
class OrphanedJobDetector
  # Runs every 1 minute
  def perform
    # Find jobs in RUNNING state for > timeout duration
    orphaned_jobs = Job.where(
      status: 'RUNNING',
      started_at: ..10.minutes.ago
    )

    orphaned_jobs.each do |job|
      # Check if execution lock still exists
      lock_key = "job_execution:#{job.id}"

      if redis.exists?(lock_key)
        # Job still running, extend timeout
        next
      else
        # Job orphaned, retry
        job.update!(status: 'FAILED', failure_reason: 'Worker crashed')
        retry_job(job)
      end
    end
  end
end
```

**Scenario 2: Duplicate execution due to network partition**

Solution: Idempotency keys

```ruby
class JobExecutor
  def execute(job)
    idempotency_key = "job_execution:#{job.id}:#{job.attempt_number}"

    # Check if already executed
    if redis.exists?("job_result:#{idempotency_key}")
      Rails.logger.info("Job #{job.id} already executed, skipping")
      return
    end

    # Execute job
    result = perform_job(job)

    # Store result with idempotency key
    redis.setex("job_result:#{idempotency_key}", 24.hours.to_i, result.to_json)
  end
end
```

**Scenario 3: Scheduler leader failure**

Solution: Leader election with Redis

```ruby
class SchedulerLeaderElection
  LEADER_KEY = 'scheduler:leader'
  LEADER_TTL = 10  # seconds

  def acquire_leadership
    loop do
      # Try to become leader
      became_leader = redis.set(
        LEADER_KEY,
        scheduler_id,
        nx: true,
        ex: LEADER_TTL
      )

      if became_leader
        Rails.logger.info("Became scheduler leader")
        run_as_leader
      else
        # Wait and retry
        sleep 5
      end
    end
  end

  def run_as_leader
    loop do
      # Renew leadership
      renewed = redis.set(
        LEADER_KEY,
        scheduler_id,
        xx: true,
        ex: LEADER_TTL
      )

      break unless renewed

      # Poll and enqueue jobs
      poll_and_enqueue_jobs

      sleep 1
    end
  end
end
```

## Data Model Design

### PostgreSQL Schema

```sql
-- Jobs table
CREATE TABLE jobs (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    name VARCHAR(255) NOT NULL,
    schedule VARCHAR(255),  -- Cron expression, NULL for one-time jobs
    payload JSONB NOT NULL,
    status VARCHAR(50) NOT NULL,  -- SCHEDULED, QUEUED, RUNNING, COMPLETED, FAILED, CANCELLED
    priority INTEGER DEFAULT 0,
    timeout_seconds INTEGER DEFAULT 3600,
    max_attempts INTEGER DEFAULT 3,
    attempt_number INTEGER DEFAULT 0,
    next_run_at TIMESTAMP,
    queued_at TIMESTAMP,
    started_at TIMESTAMP,
    completed_at TIMESTAMP,
    execution_time_ms INTEGER,
    failure_reason TEXT,
    created_at TIMESTAMP NOT NULL DEFAULT NOW(),
    updated_at TIMESTAMP NOT NULL DEFAULT NOW(),

    INDEX idx_jobs_next_run (status, next_run_at) WHERE status = 'SCHEDULED',
    INDEX idx_jobs_status (status, created_at DESC)
);

-- Job executions (audit trail)
CREATE TABLE job_executions (
    id BIGSERIAL PRIMARY KEY,
    job_id UUID REFERENCES jobs(id) NOT NULL,
    attempt_number INTEGER NOT NULL,
    status VARCHAR(50) NOT NULL,
    started_at TIMESTAMP NOT NULL,
    completed_at TIMESTAMP,
    execution_time_ms INTEGER,
    worker_id VARCHAR(255),
    error_message TEXT,
    output JSONB,

    INDEX idx_executions_job_id (job_id, started_at DESC)
);

-- Job dependencies
CREATE TABLE job_dependencies (
    id BIGSERIAL PRIMARY KEY,
    job_id UUID REFERENCES jobs(id) NOT NULL,
    depends_on_job_id UUID REFERENCES jobs(id) NOT NULL,
    created_at TIMESTAMP NOT NULL DEFAULT NOW(),

    UNIQUE(job_id, depends_on_job_id),
    INDEX idx_dependencies_job (job_id)
);

-- Recurring job history
CREATE TABLE recurring_job_runs (
    id BIGSERIAL PRIMARY KEY,
    job_id UUID REFERENCES jobs(id) NOT NULL,
    scheduled_at TIMESTAMP NOT NULL,
    executed_at TIMESTAMP,
    status VARCHAR(50) NOT NULL,
    execution_time_ms INTEGER,

    INDEX idx_recurring_runs_job (job_id, scheduled_at DESC)
) PARTITION BY RANGE (scheduled_at);
```

### Redis Data Structures

```
# Distributed locks
job_lock:{job_id} → worker_id (TTL: 60s)
job_execution:{job_id} → lock_token (TTL: job timeout)

# Leader election
scheduler:leader → scheduler_id (TTL: 10s)

# Idempotency
job_result:{job_id}:{attempt} → result JSON (TTL: 24h)

# Worker heartbeat
worker:{worker_id}:heartbeat → timestamp (TTL: 30s)
```

## Concurrency & Consistency Strategy

### Exactly-Once Execution with Distributed Locks

```ruby
class JobExecutor
  def execute_with_lock(job)
    lock_key = "job_execution:#{job.id}"
    lock_token = SecureRandom.uuid

    # Acquire lock with timeout
    lock_acquired = redis.set(
      lock_key,
      lock_token,
      nx: true,
      ex: job.timeout_seconds
    )

    unless lock_acquired
      Rails.logger.warn("Job #{job.id} already being executed")
      return
    end

    begin
      # Update status to RUNNING
      job.update!(
        status: 'RUNNING',
        started_at: Time.current,
        attempt_number: job.attempt_number + 1
      )

      # Execute job
      result = execute_job_logic(job)

      # Update status to COMPLETED
      job.update!(
        status: 'COMPLETED',
        completed_at: Time.current,
        execution_time_ms: (Time.current - job.started_at) * 1000
      )

      # Record execution
      JobExecution.create!(
        job_id: job.id,
        attempt_number: job.attempt_number,
        status: 'COMPLETED',
        started_at: job.started_at,
        completed_at: Time.current,
        worker_id: worker_id,
        output: result
      )

      result
    rescue => e
      handle_execution_failure(job, e)
      raise
    ensure
      # Release lock (only if we still own it)
      release_lock_safely(lock_key, lock_token)
    end
  end

  private

  def release_lock_safely(lock_key, lock_token)
    lua_script = <<~LUA
      if redis.call('GET', KEYS[1]) == ARGV[1] then
        return redis.call('DEL', KEYS[1])
      end
      return 0
    LUA

    redis.eval(lua_script, keys: [lock_key], argv: [lock_token])
  end
end
```

### Job Dependency Resolution

```ruby
class JobDependencyResolver
  def can_execute?(job)
    dependencies = JobDependency.where(job_id: job.id)

    dependencies.all? do |dep|
      dependent_job = Job.find(dep.depends_on_job_id)
      dependent_job.status == 'COMPLETED'
    end
  end

  def execute_with_dependencies(job)
    # Check dependencies
    unless can_execute?(job)
      Rails.logger.info("Job #{job.id} waiting for dependencies")
      return
    end

    # Execute job
    JobExecutor.new.execute_with_lock(job)

    # Trigger dependent jobs
    trigger_dependent_jobs(job)
  end

  private

  def trigger_dependent_jobs(completed_job)
    dependent_jobs = Job.joins(:job_dependencies)
      .where(job_dependencies: { depends_on_job_id: completed_job.id })
      .where(status: 'WAITING_DEPENDENCIES')

    dependent_jobs.each do |job|
      if can_execute?(job)
        job.update!(status: 'SCHEDULED', next_run_at: Time.current)
      end
    end
  end
end
```

## Ruby Implementation Examples

### Job Scheduler Service

```ruby
class JobSchedulerService
  def initialize(redis)
    @redis = redis
    @scheduler_id = "scheduler_#{Socket.gethostname}_#{Process.pid}"
  end

  def run
    # Try to become leader
    SchedulerLeaderElection.new(@redis, @scheduler_id).acquire_leadership
  end

  def poll_and_enqueue_jobs
    # Find jobs due for execution
    due_jobs = Job.where(
      status: 'SCHEDULED',
      next_run_at: ..Time.current
    ).order(priority: :desc, next_run_at: :asc)
     .limit(1000)

    due_jobs.each do |job|
      enqueue_job(job)
    end
  end

  private

  def enqueue_job(job)
    # Acquire lock to prevent duplicate enqueue
    lock_key = "job_enqueue_lock:#{job.id}"
    lock_acquired = @redis.set(lock_key, @scheduler_id, nx: true, ex: 60)

    return unless lock_acquired

    begin
      # Check dependencies
      if job.has_dependencies? && !dependencies_met?(job)
        job.update!(status: 'WAITING_DEPENDENCIES')
        return
      end

      # Publish to queue
      JobQueue.publish(
        job_id: job.id,
        name: job.name,
        payload: job.payload,
        timeout: job.timeout_seconds,
        attempt: job.attempt_number + 1
      )

      # Update status
      job.update!(status: 'QUEUED', queued_at: Time.current)

      Rails.logger.info("Enqueued job #{job.id}")
    ensure
      @redis.del(lock_key)
    end
  end

  def dependencies_met?(job)
    JobDependencyResolver.new.can_execute?(job)
  end
end
```

### Job Worker

```ruby
class JobWorker
  def initialize
    @worker_id = "worker_#{Socket.gethostname}_#{Process.pid}"
    @redis = Redis.new
    @running = true
  end

  def start
    # Register worker
    register_worker

    # Start heartbeat thread
    start_heartbeat

    # Process jobs
    process_jobs
  end

  def stop
    @running = false
    unregister_worker
  end

  private

  def process_jobs
    while @running
      begin
        # Consume job from queue
        message = JobQueue.consume(timeout: 5)

        next unless message

        job_data = JSON.parse(message.body)
        job = Job.find(job_data['job_id'])

        # Execute job
        JobExecutor.new(@redis, @worker_id).execute_with_lock(job)

        # Acknowledge message
        message.ack
      rescue => e
        Rails.logger.error("Worker error: #{e.message}")
        message&.nack
      end
    end
  end

  def register_worker
    @redis.sadd('workers:active', @worker_id)
  end

  def unregister_worker
    @redis.srem('workers:active', @worker_id)
  end

  def start_heartbeat
    Thread.new do
      while @running
        @redis.setex("worker:#{@worker_id}:heartbeat", 30, Time.current.to_i)
        sleep 10
      end
    end
  end
end
```

### Retry Logic with Exponential Backoff

```ruby
class JobRetryHandler
  def handle_failure(job, error)
    job.increment!(:attempt_number)

    if job.attempt_number >= job.max_attempts
      # Max attempts reached, move to dead letter queue
      job.update!(
        status: 'FAILED',
        failure_reason: error.message
      )

      DeadLetterQueue.publish(job.to_message)

      Rails.logger.error("Job #{job.id} failed after #{job.max_attempts} attempts")
    else
      # Calculate backoff delay
      delay = calculate_backoff(job.attempt_number)

      # Reschedule job
      job.update!(
        status: 'SCHEDULED',
        next_run_at: delay.seconds.from_now,
        failure_reason: error.message
      )

      Rails.logger.warn("Job #{job.id} failed, retrying in #{delay}s")
    end

    # Record execution
    JobExecution.create!(
      job_id: job.id,
      attempt_number: job.attempt_number,
      status: 'FAILED',
      started_at: job.started_at,
      completed_at: Time.current,
      worker_id: @worker_id,
      error_message: error.message
    )
  end

  private

  def calculate_backoff(attempt)
    # Exponential backoff: 2^attempt seconds
    # Attempt 1: 2s, Attempt 2: 4s, Attempt 3: 8s
    base_delay = 2 ** attempt

    # Add jitter to prevent thundering herd
    jitter = rand(0..base_delay * 0.1)

    base_delay + jitter
  end
end
```

### Cron Job Scheduler

```ruby
class CronJobScheduler
  def schedule_next_run(job)
    return unless job.schedule  # One-time job

    cron = Fugit::Cron.parse(job.schedule)
    next_run = cron.next_time(Time.current)

    # Create new job instance for next run
    Job.create!(
      name: job.name,
      schedule: job.schedule,
      payload: job.payload,
      status: 'SCHEDULED',
      next_run_at: next_run,
      priority: job.priority,
      timeout_seconds: job.timeout_seconds,
      max_attempts: job.max_attempts
    )

    # Record in recurring job history
    RecurringJobRun.create!(
      job_id: job.id,
      scheduled_at: next_run,
      status: 'SCHEDULED'
    )
  end
end
```

### Job Cancellation

```ruby
class JobCancellationService
  def cancel(job_id)
    job = Job.find(job_id)

    case job.status
    when 'SCHEDULED', 'QUEUED'
      # Easy case: job not started yet
      job.update!(status: 'CANCELLED', completed_at: Time.current)
    when 'RUNNING'
      # Hard case: job currently executing
      cancel_running_job(job)
    when 'COMPLETED', 'FAILED', 'CANCELLED'
      # Already finished
      raise JobAlreadyFinishedError
    end
  end

  private

  def cancel_running_job(job)
    # Set cancellation flag
    redis.setex("job_cancel:#{job.id}", 3600, '1')

    # Job executor should check this flag periodically
    job.update!(status: 'CANCELLING')

    # Wait for job to finish (with timeout)
    wait_for_cancellation(job, timeout: 30)
  end

  def wait_for_cancellation(job, timeout:)
    start_time = Time.current

    loop do
      job.reload

      if job.status == 'CANCELLED'
        return true
      elsif Time.current - start_time > timeout
        # Force kill (release lock)
        force_kill_job(job)
        return false
      end

      sleep 1
    end
  end

  def force_kill_job(job)
    lock_key = "job_execution:#{job.id}"
    redis.del(lock_key)

    job.update!(
      status: 'CANCELLED',
      completed_at: Time.current,
      failure_reason: 'Force killed'
    )
  end
end
```

## Scaling Strategy

### Horizontal Scaling

**Workers:**
- Auto-scale based on queue depth
- Minimum: 10 workers
- Maximum: 1000 workers
- Scale up: queue depth > 1000
- Scale down: queue depth < 100

**Schedulers:**
- 3 schedulers (leader election)
- Only leader actively polls
- Followers on standby

### Vertical Scaling

**PostgreSQL:**
- Instance type: r6g.2xlarge (64 GB RAM)
- Reason: Large job table, complex queries

### Partitioning Strategy

```ruby
# Partition jobs table by created_at
# Monthly partitions for historical data
# Keep last 12 months in hot storage
```

## High Availability Strategy

### Leader Election

```ruby
# Use Redis for leader election
# Automatic failover if leader dies
# Followers detect leader failure via TTL expiry
```

### Worker Redundancy

```ruby
# Multiple workers consume from same queue
# If worker dies, job requeued automatically
# Orphaned job detector recovers stuck jobs
```

## Observability & Monitoring

### Key Metrics

```ruby
class JobMetrics
  def self.record_execution(job, duration_ms, status)
    StatsD.increment('job.executed',
      tags: ["name:#{job.name}", "status:#{status}"])

    StatsD.histogram('job.duration', duration_ms,
      tags: ["name:#{job.name}"])

    StatsD.gauge('job.queue_depth',
      JobQueue.depth)
  end
end
```

### Alerting

```yaml
alerts:
  - name: HighJobFailureRate
    condition: job.failed / job.executed > 0.1
    duration: 10m
    severity: warning

  - name: JobQueueBacklog
    condition: job.queue_depth > 10000
    duration: 5m
    severity: critical

  - name: NoSchedulerLeader
    condition: scheduler.leader_count == 0
    duration: 1m
    severity: critical
```

## Testing Strategy

### Unit Tests

```ruby
RSpec.describe JobExecutor do
  it 'executes job exactly once' do
    job = create(:job, status: 'QUEUED')

    # Simulate concurrent execution attempts
    threads = 3.times.map do
      Thread.new { JobExecutor.new.execute_with_lock(job) }
    end

    threads.each(&:join)

    # Verify executed only once
    expect(JobExecution.where(job_id: job.id).count).to eq(1)
  end
end
```

## Trade-offs & Alternatives

### Chosen: PostgreSQL + Redis

**Pros:**
- Durable job storage
- Fast distributed locking
- Proven reliability

**Cons:**
- Two systems to manage
- Network overhead

**Alternative: Sidekiq/Resque**

**Pros:**
- Battle-tested
- Rich ecosystem

**Cons:**
- Less control
- Limited customization

**Decision:** Custom solution for exact requirements

---

### Cost Considerations

**Infrastructure:**
- PostgreSQL: $800/month
- Redis: $500/month
- Workers: $3000/month (30 instances)
- Message Queue: $200/month

**Total:** ~$4500/month for 100K jobs/minute
