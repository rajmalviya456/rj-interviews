# Real-Time Leaderboard System

## Problem Statement

Design a real-time leaderboard system for a multiplayer gaming platform that displays rankings of millions of players with sub-second update latency.

**Scale Requirements:**
- 100 million active players globally
- 10,000 score updates per second
- Leaderboard queries: 50,000 QPS
- Support multiple leaderboard types (global, regional, friends, time-based)
- Real-time updates (< 1 second latency)
- Historical leaderboards (daily, weekly, monthly, all-time)

**Business Constraints:**
- Accurate ranking (no ties unless scores are identical)
- Support pagination (top 100, rank 1000-1100, etc.)
- Show player's current rank even if not in top N
- Support score decay over time
- Handle score corrections/adjustments
- Prevent cheating/score manipulation

**Failure Expectations:**
- System must handle Redis failures gracefully
- No data loss of player scores
- Eventual consistency acceptable for non-critical leaderboards
- Strong consistency for prize-eligible leaderboards

**Edge Cases:**
- Simultaneous score updates for same player
- Mass score updates (e.g., end of game event)
- Leaderboard resets (daily/weekly)
- Player rank queries for players not in top N
- Tie-breaking logic
- Score rollbacks due to cheating detection

## Functional Requirements

- Update player scores in real-time
- Retrieve top N players
- Get player's current rank
- Get players around a specific rank
- Support multiple leaderboard types
- Reset leaderboards on schedule
- Archive historical leaderboards
- Support score increments and absolute updates
- Provide rank change indicators (↑↓)
- Support filtering (by region, level, etc.)

## Non-Functional Requirements

- **Availability:** 99.9%
- **Latency:**
  - Score update: P99 < 100ms
  - Rank query: P99 < 50ms
  - Top N query: P99 < 100ms
- **Throughput:** 10K score updates/sec, 50K queries/sec
- **Consistency:** Eventual consistency for most leaderboards, strong for prize-eligible
- **Scalability:** Support 100M+ players
- **Accuracy:** 100% accurate rankings

## Core Engineering Challenges

1. **High Write Throughput**
   - 10K score updates per second
   - Atomic rank recalculation
   - Concurrent updates to same player

2. **Efficient Rank Queries**
   - Finding rank of arbitrary player (not in top N)
   - Pagination at arbitrary positions
   - Counting players with higher scores

3. **Memory Efficiency**
   - 100M players × (player_id + score) = ~2GB minimum
   - Multiple leaderboards multiply memory requirements
   - Historical data retention

4. **Leaderboard Resets**
   - Atomic reset without downtime
   - Archiving old leaderboard
   - Zero data loss during reset

5. **Tie-Breaking**
   - Consistent tie-breaking logic
   - Secondary sort criteria (timestamp, player_id)

6. **Multi-Dimensional Leaderboards**
   - Global, regional, friends
   - Different time windows
   - Filtered leaderboards

## High-Level Design (HLD)

### System Architecture Overview

The real-time leaderboard system uses **Redis Sorted Sets** as the primary data structure with the following key components:

1. **API Layer** - Stateless servers handling score updates and rank queries
2. **Redis Cluster** - Sharded sorted sets for different leaderboard types
3. **Score Aggregator** - Batch processing for score updates
4. **Leaderboard Manager** - Handles resets, archiving, and maintenance
5. **PostgreSQL** - Persistent storage for historical data and audit trail
6. **Cache Layer** - CDN for frequently accessed leaderboard pages

### Architecture Diagram

```
                            Players (100M)
                                 │
                                 ▼
                          Load Balancer
                                 │
                ┌────────────────┼────────────────┐
                ▼                ▼                ▼
          API Servers      API Servers      API Servers
          (Stateless)      (Stateless)      (Stateless)
                │                │                │
                └────────────────┼────────────────┘
                                 │
                ┌────────────────┼────────────────┐
                ▼                ▼                ▼
          Redis Cluster    Redis Cluster    Redis Cluster
          (Shard 1)        (Shard 2)        (Shard 3)
          - Global LB      - Regional LB    - Friends LB
          - Daily LB       - Weekly LB      - Monthly LB
                │                │                │
                └────────────────┼────────────────┘
                                 │
                                 ▼
                          PostgreSQL
                          (Persistent Storage)
                          - Player Scores
                          - Historical Data
                                 │
                                 ▼
                          Data Warehouse
                          (Analytics)
```

### Component Responsibilities

**1. API Layer:**
- Accept score update requests
- Validate player_id and score
- Route to appropriate leaderboard (global, regional, friends)
- Handle rank queries with pagination
- Cache frequently accessed leaderboard pages
- Rate limiting per player

**2. Redis Cluster:**
- Store leaderboards as sorted sets (ZADD, ZRANK, ZRANGE)
- Atomic score updates
- Sub-millisecond rank queries
- Sharded by leaderboard type
- Persistence with AOF (Append-Only File)

**3. Score Aggregator:**
- Batch score updates for efficiency
- Deduplicate concurrent updates for same player
- Apply score decay formulas
- Detect and flag suspicious score patterns

**4. Leaderboard Manager:**
- Schedule leaderboard resets (daily, weekly, monthly)
- Archive old leaderboards to PostgreSQL
- Create new leaderboards atomically
- Manage leaderboard lifecycle

**5. PostgreSQL:**
- Persistent storage for all scores
- Historical leaderboard snapshots
- Player statistics and metadata
- Audit trail for score changes

**6. Cache Layer (CDN):**
- Cache top 100 leaderboard (1-minute TTL)
- Cache player rank (10-second TTL)
- Reduce load on Redis
- Geographic distribution

### Data Flow

```
1. Score Update
   Player → API → Validate score
   → Redis ZADD (leaderboard:global, score, player_id)
   → Async write to PostgreSQL
   → Return new rank

2. Get Top N
   Client → API → Check CDN cache
   → If miss: Redis ZREVRANGE (leaderboard:global, 0, N-1)
   → Cache result (1-minute TTL)
   → Return top N players with scores

3. Get Player Rank
   Client → API → Redis ZREVRANK (leaderboard:global, player_id)
   → Redis ZSCORE (leaderboard:global, player_id)
   → Return rank and score

4. Get Players Around Rank
   Client → API → Redis ZREVRANGE (leaderboard:global, rank-50, rank+50)
   → Return 100 players centered on rank

5. Leaderboard Reset (Daily)
   Cron Job → Leaderboard Manager
   → Archive current leaderboard to PostgreSQL
   → Rename Redis key (leaderboard:global → leaderboard:global:2024-01-15)
   → Create new empty leaderboard
   → Publish reset event
```

### Scalability Strategy

**Horizontal Scaling:**
- API Servers: Auto-scale based on QPS (10-50 instances)
- Redis: Cluster mode with 6-12 shards
- PostgreSQL: Read replicas for historical queries (3-5 replicas)

**Vertical Scaling:**
- API Servers: c6g.large (2 vCPU, 4 GB RAM)
- Redis: r6g.2xlarge (8 vCPU, 64 GB RAM) for large sorted sets
- PostgreSQL: r6g.xlarge (4 vCPU, 32 GB RAM)

**Partitioning:**
- Redis: Shard by leaderboard type (global, regional, friends)
- PostgreSQL: Partition scores table by date (monthly partitions)
- Leaderboards: Separate sorted sets per type/time window

**Caching:**
- Top 100 leaderboard: CDN cache (1-minute TTL)
- Player ranks: Local cache (10-second TTL)
- Leaderboard metadata: In-memory cache (5-minute TTL)

### Failure Handling

**Redis Failure:**
- Redis Sentinel for automatic failover (< 30s RTO)
- AOF persistence for zero data loss (RPO = 0)
- Fallback to PostgreSQL for read queries (degraded performance)
- Queue score updates during failover

**API Server Failure:**
- Load balancer health checks
- Auto-scaling replaces failed instances
- Stateless design allows instant failover

**PostgreSQL Failure:**
- Automatic failover to read replica
- Redis continues serving leaderboard queries
- Score updates queued for later persistence

**Leaderboard Reset Failure:**
- Atomic rename operation (RENAME command)
- Rollback on failure
- Retry with exponential backoff
- Alert operations team

## Low-Level Design (LLD)

### Class Diagram

```
┌─────────────────────────────┐
│   LeaderboardController     │
├─────────────────────────────┤
│ + update_score(params)      │
│ + get_top_n(n)              │
│ + get_player_rank(id)       │
│ + get_around_rank(rank)     │
└─────────────────────────────┘
            │
            │ uses
            ▼
┌─────────────────────────────┐
│   LeaderboardService        │
├─────────────────────────────┤
│ - redis: Redis              │
│ - db: Database              │
│ - cache: Cache              │
├─────────────────────────────┤
│ + add_score(player, score)  │
│ + get_rank(player_id)       │
│ + get_top(n)                │
│ + get_range(start, end)     │
└─────────────────────────────┘
            │
            │ uses
            ▼
┌─────────────────────────────┐
│   RedisSortedSet            │
├─────────────────────────────┤
│ - key: String               │
│ - redis: Redis              │
├─────────────────────────────┤
│ + zadd(member, score)       │
│ + zrank(member)             │
│ + zrevrank(member)          │
│ + zrange(start, stop)       │
│ + zrevrange(start, stop)    │
│ + zscore(member)            │
│ + zcard()                   │
└─────────────────────────────┘

┌─────────────────────────────┐
│   LeaderboardManager        │
├─────────────────────────────┤
│ + reset_daily()             │
│ + reset_weekly()            │
│ + archive_leaderboard()     │
│ - create_snapshot()         │
└─────────────────────────────┘

┌─────────────────────────────┐
│   ScoreAggregator           │
├─────────────────────────────┤
│ + batch_update(scores)      │
│ + apply_decay(player_id)    │
│ - deduplicate(scores)       │
└─────────────────────────────┘
```

### Database Schema Details

**Scores Table:**
```sql
CREATE TABLE scores (
    id BIGSERIAL PRIMARY KEY,
    player_id BIGINT NOT NULL,
    leaderboard_type VARCHAR(50) NOT NULL, -- global, regional, friends
    leaderboard_period VARCHAR(50) NOT NULL, -- daily, weekly, monthly, all_time
    score BIGINT NOT NULL,
    rank INTEGER,
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),

    CONSTRAINT positive_score CHECK (score >= 0)
) PARTITION BY RANGE (created_at);

-- Monthly partitions
CREATE TABLE scores_2024_01 PARTITION OF scores
    FOR VALUES FROM ('2024-01-01') TO ('2024-02-01');

CREATE INDEX idx_scores_player ON scores(player_id, created_at DESC);
CREATE INDEX idx_scores_leaderboard ON scores(leaderboard_type, leaderboard_period, score DESC);
CREATE UNIQUE INDEX idx_scores_unique ON scores(player_id, leaderboard_type, leaderboard_period, created_at DESC);
```

**Leaderboard Snapshots Table:**
```sql
CREATE TABLE leaderboard_snapshots (
    id BIGSERIAL PRIMARY KEY,
    leaderboard_type VARCHAR(50) NOT NULL,
    leaderboard_period VARCHAR(50) NOT NULL,
    snapshot_date DATE NOT NULL,
    top_players JSONB NOT NULL, -- Top 1000 players
    total_players INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT NOW(),

    UNIQUE(leaderboard_type, leaderboard_period, snapshot_date)
);

CREATE INDEX idx_snapshots_date ON leaderboard_snapshots(snapshot_date DESC);
CREATE INDEX idx_snapshots_type ON leaderboard_snapshots(leaderboard_type, leaderboard_period);
```

### API Endpoints

**Score Update API:**

```ruby
# Update player score
POST /api/v1/leaderboard/score
{
  "player_id": 12345,
  "score": 1500,
  "leaderboard_type": "global",  # global, regional, friends
  "game_id": "abc123"
}

Response: 200 OK
{
  "player_id": 12345,
  "score": 1500,
  "rank": 42,
  "rank_change": 5,  # Moved up 5 positions
  "percentile": 99.5
}

# Increment score (relative update)
POST /api/v1/leaderboard/score/increment
{
  "player_id": 12345,
  "score_delta": 100
}
```

**Leaderboard Query API:**

```ruby
# Get top N players
GET /api/v1/leaderboard/top?n=100&type=global&period=daily

Response: 200 OK
{
  "leaderboard_type": "global",
  "period": "daily",
  "total_players": 10000000,
  "players": [
    {
      "rank": 1,
      "player_id": 99999,
      "player_name": "ProGamer",
      "score": 15000,
      "rank_change": 0
    },
    ...
  ]
}

# Get player rank
GET /api/v1/leaderboard/rank/:player_id?type=global

Response: 200 OK
{
  "player_id": 12345,
  "rank": 42,
  "score": 1500,
  "total_players": 10000000,
  "percentile": 99.5
}

# Get players around rank
GET /api/v1/leaderboard/around/:rank?range=50

Response: 200 OK
{
  "center_rank": 1000,
  "players": [
    { "rank": 950, "player_id": 111, "score": 1200 },
    ...
    { "rank": 1050, "player_id": 222, "score": 1100 }
  ]
}
```

### Algorithms

**1. Score Update with Rank Calculation:**

```ruby
class LeaderboardService
  LEADERBOARD_KEY = "leaderboard:global:daily"

  def update_score(player_id, score)
    # Get old score and rank
    old_score = redis.zscore(LEADERBOARD_KEY, player_id)
    old_rank = redis.zrevrank(LEADERBOARD_KEY, player_id) if old_score

    # Update score in Redis sorted set
    redis.zadd(LEADERBOARD_KEY, score, player_id)

    # Get new rank
    new_rank = redis.zrevrank(LEADERBOARD_KEY, player_id)

    # Calculate rank change
    rank_change = old_rank ? (old_rank - new_rank) : 0

    # Async persist to PostgreSQL
    PersistScoreJob.perform_later(player_id, score, new_rank)

    {
      player_id: player_id,
      score: score,
      rank: new_rank + 1,  # Convert 0-indexed to 1-indexed
      rank_change: rank_change,
      percentile: calculate_percentile(new_rank)
    }
  end

  private

  def calculate_percentile(rank)
    total_players = redis.zcard(LEADERBOARD_KEY)
    ((total_players - rank) / total_players.to_f) * 100
  end
end
```

**2. Batch Score Updates:**

```ruby
class ScoreAggregator
  BATCH_SIZE = 1000
  BATCH_INTERVAL = 1  # second

  def initialize
    @score_queue = []
    @mutex = Mutex.new
  end

  def enqueue_score(player_id, score)
    @mutex.synchronize do
      @score_queue << { player_id: player_id, score: score }
    end
  end

  def process_batch
    loop do
      sleep BATCH_INTERVAL

      batch = @mutex.synchronize do
        @score_queue.shift(BATCH_SIZE)
      end

      next if batch.empty?

      # Deduplicate: Keep highest score per player
      deduplicated = batch.group_by { |s| s[:player_id] }
                          .transform_values { |scores| scores.max_by { |s| s[:score] } }

      # Batch update to Redis using pipeline
      redis.pipelined do
        deduplicated.each do |player_id, score_data|
          redis.zadd(LEADERBOARD_KEY, score_data[:score], player_id)
        end
      end
    end
  end
end
```

**3. Get Top N with Caching:**

```ruby
class LeaderboardService
  CACHE_TTL = 60  # 1 minute

  def get_top_n(n, leaderboard_type: 'global', period: 'daily')
    cache_key = "leaderboard:top:#{leaderboard_type}:#{period}:#{n}"

    # Check cache
    cached = Rails.cache.read(cache_key)
    return cached if cached

    # Fetch from Redis
    leaderboard_key = "leaderboard:#{leaderboard_type}:#{period}"

    # Get top N players with scores
    top_players = redis.zrevrange(leaderboard_key, 0, n - 1, with_scores: true)

    # Format response
    result = top_players.each_with_index.map do |(player_id, score), index|
      {
        rank: index + 1,
        player_id: player_id.to_i,
        score: score.to_i,
        player_name: get_player_name(player_id)  # From cache or DB
      }
    end

    # Cache result
    Rails.cache.write(cache_key, result, expires_in: CACHE_TTL)

    result
  end
end
```

**4. Leaderboard Reset with Archiving:**

```ruby
class LeaderboardManager
  def reset_daily_leaderboard
    leaderboard_key = "leaderboard:global:daily"
    archive_key = "leaderboard:global:daily:#{Date.yesterday}"

    # Step 1: Archive current leaderboard
    archive_leaderboard(leaderboard_key, archive_key)

    # Step 2: Persist top 1000 to PostgreSQL
    persist_snapshot(leaderboard_key, Date.yesterday)

    # Step 3: Rename current leaderboard to archive
    redis.rename(leaderboard_key, archive_key)

    # Step 4: Create new empty leaderboard
    # (Automatically created on first ZADD)

    # Step 5: Set expiry on archive (30 days)
    redis.expire(archive_key, 30.days.to_i)

    # Step 6: Publish reset event
    redis.publish('leaderboard:reset', { type: 'daily', date: Date.today }.to_json)
  end

  private

  def persist_snapshot(leaderboard_key, date)
    # Get top 1000 players
    top_players = redis.zrevrange(leaderboard_key, 0, 999, with_scores: true)
    total_players = redis.zcard(leaderboard_key)

    # Save to PostgreSQL
    LeaderboardSnapshot.create!(
      leaderboard_type: 'global',
      leaderboard_period: 'daily',
      snapshot_date: date,
      top_players: top_players.map { |p, s| { player_id: p, score: s } },
      total_players: total_players
    )
  end
end
```

**5. Tie-Breaking with Timestamp:**

```ruby
# Use composite score: (score * 1e10) + (MAX_TIMESTAMP - timestamp)
# This ensures higher scores rank first, and earlier timestamps break ties

class LeaderboardService
  MAX_TIMESTAMP = 9999999999  # Year 2286

  def add_score_with_tiebreaker(player_id, score, timestamp)
    # Composite score for tie-breaking
    composite_score = (score * 1e10) + (MAX_TIMESTAMP - timestamp.to_i)

    redis.zadd(LEADERBOARD_KEY, composite_score, player_id)
  end

  def get_actual_score(composite_score)
    (composite_score / 1e10).to_i
  end
end
```

**6. Friends Leaderboard:**

```ruby
class LeaderboardService
  def get_friends_leaderboard(player_id, limit: 100)
    # Get player's friends list
    friend_ids = get_friend_ids(player_id)
    friend_ids << player_id  # Include self

    # Get scores for all friends
    scores = redis.pipelined do
      friend_ids.each do |friend_id|
        redis.zscore(LEADERBOARD_KEY, friend_id)
      end
    end

    # Combine and sort
    friends_with_scores = friend_ids.zip(scores)
                                    .reject { |_, score| score.nil? }
                                    .sort_by { |_, score| -score }
                                    .take(limit)

    # Format response
    friends_with_scores.each_with_index.map do |(friend_id, score), index|
      {
        rank: index + 1,
        player_id: friend_id,
        score: score.to_i,
        is_current_player: friend_id == player_id
      }
    end
  end
end
```

### Sequence Diagrams

**Score Update Flow:**

```
Player   API    Redis   PostgreSQL
 │        │       │         │
 │─Score──>│       │         │
 │        │       │         │
 │        │─ZADD──>│         │
 │        │<─OK────│         │
 │        │       │         │
 │        │─ZREVRANK>│       │
 │        │<─Rank 42─│       │
 │        │       │         │
 │        │───────────Async──>│
 │        │       │  Persist │
 │        │       │         │
 │<─200 OK│       │         │
 │  rank=42       │         │
```

**Get Top N Flow:**

```
Client   API    Cache   Redis
 │        │       │       │
 │─Top 100>│       │       │
 │        │       │       │
 │        │─Check─>│       │
 │        │<─Miss──│       │
 │        │       │       │
 │        │───ZREVRANGE────>│
 │        │<──Top 100───────│
 │        │       │       │
 │        │─Cache─>│       │
 │        │       │       │
 │<─200 OK│       │       │
```

### Performance Optimizations

**1. Redis Pipelining:**
```ruby
# Get ranks for multiple players in one round-trip
def get_ranks_batch(player_ids)
  redis.pipelined do
    player_ids.each do |player_id|
      redis.zrevrank(LEADERBOARD_KEY, player_id)
    end
  end
end
```

**2. Lua Script for Atomic Operations:**
```ruby
# Atomic score update with rank calculation
UPDATE_AND_RANK_SCRIPT = <<~LUA
  local key = KEYS[1]
  local player_id = ARGV[1]
  local score = tonumber(ARGV[2])

  redis.call('ZADD', key, score, player_id)
  local rank = redis.call('ZREVRANK', key, player_id)
  local total = redis.call('ZCARD', key)

  return {rank, total}
LUA

def update_score_atomic(player_id, score)
  rank, total = redis.eval(
    UPDATE_AND_RANK_SCRIPT,
    keys: [LEADERBOARD_KEY],
    argv: [player_id, score]
  )

  { rank: rank + 1, total: total }
end
```

**3. CDN Caching:**
```ruby
# Cache top 100 at CDN edge
class LeaderboardController
  def top
    response.headers['Cache-Control'] = 'public, max-age=60'
    response.headers['Surrogate-Control'] = 'max-age=60'

    render json: leaderboard_service.get_top_n(100)
  end
end
```

**4. Read Replicas:**
```ruby
# Use Redis read replicas for queries
REDIS_MASTER = Redis.new(url: ENV['REDIS_MASTER_URL'])
REDIS_REPLICA = Redis.new(url: ENV['REDIS_REPLICA_URL'])

def get_top_n(n)
  # Read from replica
  REDIS_REPLICA.zrevrange(LEADERBOARD_KEY, 0, n - 1, with_scores: true)
end

def update_score(player_id, score)
  # Write to master
  REDIS_MASTER.zadd(LEADERBOARD_KEY, score, player_id)
end
```

**5. Compression for Large Leaderboards:**
```ruby
# Store only top 1M players in Redis, rest in PostgreSQL
MAX_REDIS_PLAYERS = 1_000_000

def prune_leaderboard
  total_players = redis.zcard(LEADERBOARD_KEY)

  if total_players > MAX_REDIS_PLAYERS
    # Remove bottom players
    redis.zremrangebyrank(LEADERBOARD_KEY, 0, total_players - MAX_REDIS_PLAYERS - 1)
  end
end
```

## Step-by-Step Request Flow

### Score Update Flow

1. **Player completes game, score submitted**
   ```
   POST /api/v1/leaderboard/score
   {
     "player_id": 12345,
     "score": 1500,
     "game_id": "abc123",
     "timestamp": "2024-01-15T10:30:00Z"
   }
   ```

2. **Validate score**
   ```ruby
   # Anti-cheat validation
   if score > MAX_POSSIBLE_SCORE
     raise InvalidScoreError
   end

   # Verify game completion
   game = Game.find(game_id)
   unless game.completed? && game.player_id == player_id
     raise UnauthorizedError
   end
   ```

3. **Update Redis sorted set (atomic)**
   ```ruby
   # ZADD is atomic and handles ranking automatically
   redis.zadd('leaderboard:global', score, player_id)
   redis.zadd('leaderboard:daily:2024-01-15', score, player_id)
   redis.zadd("leaderboard:region:#{player.region}", score, player_id)
   ```

4. **Persist to PostgreSQL (async)**
   ```ruby
   ScoreUpdateJob.perform_later(player_id, score, game_id)
   ```

5. **Publish event for real-time updates**
   ```ruby
   ActionCable.broadcast("leaderboard:global", {
     player_id: player_id,
     score: score,
     rank: new_rank
   })
   ```

### Rank Query Flow

1. **Get player's current rank**
   ```ruby
   # ZREVRANK returns rank (0-indexed)
   rank = redis.zrevrank('leaderboard:global', player_id)
   rank ? rank + 1 : nil  # Convert to 1-indexed
   ```

2. **Get top N players**
   ```ruby
   # ZREVRANGE with WITHSCORES
   top_players = redis.zrevrange('leaderboard:global', 0, 99, with_scores: true)
   # Returns: [[player_id, score], [player_id, score], ...]
   ```

3. **Get players around specific rank**
   ```ruby
   # Get players ranked 1000-1010
   players = redis.zrevrange('leaderboard:global', 999, 1009, with_scores: true)
   ```

4. **Get player's rank with context (players above/below)**
   ```ruby
   rank = redis.zrevrank('leaderboard:global', player_id)

   # Get 5 players above and below
   players_above = redis.zrevrange('leaderboard:global', rank - 5, rank - 1, with_scores: true)
   players_below = redis.zrevrange('leaderboard:global', rank + 1, rank + 5, with_scores: true)
   ```

## Data Model Design

### Redis Data Structures

**Sorted Sets (Primary Data Structure):**
```
Key: leaderboard:{type}:{identifier}
Type: SORTED SET
Score: player score
Member: player_id

Examples:
leaderboard:global → SORTED SET
leaderboard:daily:2024-01-15 → SORTED SET
leaderboard:region:us-east → SORTED SET
leaderboard:friends:12345 → SORTED SET
```

**Hash for Player Metadata:**
```
Key: player:{player_id}
Type: HASH
Fields:
  - username
  - level
  - region
  - last_score_update

Example:
HSET player:12345 username "ProGamer" level 50 region "us-east"
```

**Sorted Set for Historical Rankings:**
```
Key: leaderboard:archive:{date}
Type: SORTED SET
Score: player score
Member: player_id
TTL: 90 days
```

### PostgreSQL Schema

```sql
-- Player scores (source of truth)
CREATE TABLE player_scores (
    id BIGSERIAL PRIMARY KEY,
    player_id BIGINT NOT NULL,
    score BIGINT NOT NULL,
    game_id VARCHAR(255),
    leaderboard_type VARCHAR(50) NOT NULL,  -- global, daily, weekly
    created_at TIMESTAMP NOT NULL DEFAULT NOW(),

    INDEX idx_player_scores_player (player_id, created_at DESC),
    INDEX idx_player_scores_leaderboard (leaderboard_type, created_at DESC)
) PARTITION BY RANGE (created_at);

-- Monthly partitions
CREATE TABLE player_scores_2024_01 PARTITION OF player_scores
    FOR VALUES FROM ('2024-01-01') TO ('2024-02-01');

-- Leaderboard snapshots (for historical queries)
CREATE TABLE leaderboard_snapshots (
    id BIGSERIAL PRIMARY KEY,
    leaderboard_type VARCHAR(50) NOT NULL,
    snapshot_date DATE NOT NULL,
    player_id BIGINT NOT NULL,
    rank INTEGER NOT NULL,
    score BIGINT NOT NULL,
    created_at TIMESTAMP NOT NULL DEFAULT NOW(),

    UNIQUE(leaderboard_type, snapshot_date, player_id),
    INDEX idx_snapshots_type_date (leaderboard_type, snapshot_date, rank)
);

-- Player profiles
CREATE TABLE players (
    id BIGSERIAL PRIMARY KEY,
    username VARCHAR(255) NOT NULL UNIQUE,
    region VARCHAR(50) NOT NULL,
    level INTEGER DEFAULT 1,
    created_at TIMESTAMP NOT NULL DEFAULT NOW()
);
```

## Concurrency & Consistency Strategy

### Atomic Score Updates with Lua

```ruby
class LeaderboardService
  def update_score(player_id, new_score, leaderboard_key)
    lua_script = <<~LUA
      local leaderboard_key = KEYS[1]
      local player_id = ARGV[1]
      local new_score = tonumber(ARGV[2])

      -- Get current score
      local current_score = redis.call('ZSCORE', leaderboard_key, player_id)

      -- Only update if new score is higher
      if not current_score or new_score > tonumber(current_score) then
        redis.call('ZADD', leaderboard_key, new_score, player_id)

        -- Get new rank (0-indexed)
        local rank = redis.call('ZREVRANK', leaderboard_key, player_id)

        return {new_score, rank + 1}
      else
        local rank = redis.call('ZREVRANK', leaderboard_key, player_id)
        return {tonumber(current_score), rank + 1}
      end
    LUA

    result = redis.eval(
      lua_script,
      keys: [leaderboard_key],
      argv: [player_id, new_score]
    )

    score, rank = result
    { score: score, rank: rank }
  end
end
```

### Handling Concurrent Updates

```ruby
class LeaderboardService
  def increment_score(player_id, points, leaderboard_key)
    # ZINCRBY is atomic
    new_score = redis.zincrby(leaderboard_key, points, player_id)
    new_rank = redis.zrevrank(leaderboard_key, player_id) + 1

    { score: new_score.to_i, rank: new_rank }
  end
end
```

## Ruby Implementation Examples

### Leaderboard Service

```ruby
class LeaderboardService
  def initialize(redis)
    @redis = redis
  end

  # Update player score
  def update_score(player_id, score, leaderboard_type: 'global')
    leaderboard_key = "leaderboard:#{leaderboard_type}"

    # Update score (only if higher)
    result = update_score_if_higher(player_id, score, leaderboard_key)

    # Async: Persist to database
    ScoreUpdateJob.perform_later(player_id, score, leaderboard_type)

    # Async: Update related leaderboards
    update_related_leaderboards(player_id, score)

    result
  end

  # Get top N players
  def top_players(n, leaderboard_type: 'global')
    leaderboard_key = "leaderboard:#{leaderboard_type}"

    # Get top N with scores
    results = @redis.zrevrange(leaderboard_key, 0, n - 1, with_scores: true)

    # Enrich with player data
    results.map.with_index do |(player_id, score), index|
      player = get_player_data(player_id)
      {
        rank: index + 1,
        player_id: player_id.to_i,
        username: player['username'],
        score: score.to_i,
        level: player['level'].to_i
      }
    end
  end

  # Get player's rank
  def player_rank(player_id, leaderboard_type: 'global')
    leaderboard_key = "leaderboard:#{leaderboard_type}"

    rank = @redis.zrevrank(leaderboard_key, player_id)
    score = @redis.zscore(leaderboard_key, player_id)

    return nil unless rank

    {
      rank: rank + 1,
      score: score.to_i,
      total_players: @redis.zcard(leaderboard_key)
    }
  end

  # Get players around a specific rank
  def players_around_rank(rank, context: 5, leaderboard_type: 'global')
    leaderboard_key = "leaderboard:#{leaderboard_type}"

    start_rank = [rank - context - 1, 0].max
    end_rank = rank + context - 1

    results = @redis.zrevrange(leaderboard_key, start_rank, end_rank, with_scores: true)

    results.map.with_index do |(player_id, score), index|
      player = get_player_data(player_id)
      {
        rank: start_rank + index + 1,
        player_id: player_id.to_i,
        username: player['username'],
        score: score.to_i
      }
    end
  end

  # Get player's rank with context
  def player_rank_with_context(player_id, context: 5, leaderboard_type: 'global')
    rank_data = player_rank(player_id, leaderboard_type: leaderboard_type)
    return nil unless rank_data

    players = players_around_rank(rank_data[:rank], context: context, leaderboard_type: leaderboard_type)

    {
      player_rank: rank_data,
      surrounding_players: players
    }
  end

  private

  def update_score_if_higher(player_id, score, leaderboard_key)
    lua_script = <<~LUA
      local leaderboard_key = KEYS[1]
      local player_id = ARGV[1]
      local new_score = tonumber(ARGV[2])

      local current_score = redis.call('ZSCORE', leaderboard_key, player_id)

      if not current_score or new_score > tonumber(current_score) then
        redis.call('ZADD', leaderboard_key, new_score, player_id)
        local rank = redis.call('ZREVRANK', leaderboard_key, player_id)
        return {new_score, rank + 1, 1}  -- 1 = updated
      else
        local rank = redis.call('ZREVRANK', leaderboard_key, player_id)
        return {tonumber(current_score), rank + 1, 0}  -- 0 = not updated
      end
    LUA

    result = @redis.eval(lua_script, keys: [leaderboard_key], argv: [player_id, score])
    score, rank, updated = result

    {
      score: score.to_i,
      rank: rank,
      updated: updated == 1
    }
  end

  def get_player_data(player_id)
    @redis.hgetall("player:#{player_id}")
  end

  def update_related_leaderboards(player_id, score)
    player = Player.find(player_id)

    # Update daily leaderboard
    daily_key = "leaderboard:daily:#{Date.today}"
    @redis.zadd(daily_key, score, player_id)
    @redis.expire(daily_key, 7.days.to_i)

    # Update regional leaderboard
    regional_key = "leaderboard:region:#{player.region}"
    @redis.zadd(regional_key, score, player_id)

    # Update friends leaderboard
    player.friend_ids.each do |friend_id|
      friends_key = "leaderboard:friends:#{friend_id}"
      @redis.zadd(friends_key, score, player_id)
    end
  end
end
```

### Leaderboard Reset Job

```ruby
class LeaderboardResetJob < ApplicationJob
  # Runs daily at midnight
  def perform(leaderboard_type)
    leaderboard_key = "leaderboard:#{leaderboard_type}"
    archive_key = "leaderboard:archive:#{leaderboard_type}:#{Date.yesterday}"

    # Step 1: Archive current leaderboard
    archive_leaderboard(leaderboard_key, archive_key)

    # Step 2: Take snapshot to PostgreSQL
    snapshot_to_database(leaderboard_key, leaderboard_type)

    # Step 3: Reset leaderboard
    redis.del(leaderboard_key)

    Rails.logger.info("Reset leaderboard: #{leaderboard_type}")
  end

  private

  def archive_leaderboard(source_key, archive_key)
    # Copy to archive key
    redis.zunionstore(archive_key, [source_key])

    # Set TTL (90 days)
    redis.expire(archive_key, 90.days.to_i)
  end

  def snapshot_to_database(leaderboard_key, leaderboard_type)
    # Get all players and scores
    all_players = redis.zrevrange(leaderboard_key, 0, -1, with_scores: true)

    # Batch insert to database
    snapshot_date = Date.yesterday

    all_players.each_slice(1000).with_index do |batch, batch_index|
      records = batch.map.with_index do |(player_id, score), index|
        rank = batch_index * 1000 + index + 1
        {
          leaderboard_type: leaderboard_type,
          snapshot_date: snapshot_date,
          player_id: player_id.to_i,
          rank: rank,
          score: score.to_i,
          created_at: Time.current
        }
      end

      LeaderboardSnapshot.insert_all(records)
    end
  end
end
```

### Friends Leaderboard

```ruby
class FriendsLeaderboardService
  def initialize(redis, player_id)
    @redis = redis
    @player_id = player_id
    @leaderboard_key = "leaderboard:friends:#{player_id}"
  end

  # Build friends leaderboard on-demand
  def build_leaderboard
    player = Player.find(@player_id)
    friend_ids = player.friend_ids + [@player_id]  # Include self

    # Get scores from global leaderboard
    scores = @redis.zmget('leaderboard:global', *friend_ids)

    # Build friends leaderboard
    friend_ids.zip(scores).each do |friend_id, score|
      next unless score
      @redis.zadd(@leaderboard_key, score, friend_id)
    end

    # Set TTL (1 hour)
    @redis.expire(@leaderboard_key, 1.hour.to_i)
  end

  # Get friends leaderboard
  def top_friends(limit: 100)
    # Build if doesn't exist
    build_leaderboard unless @redis.exists?(@leaderboard_key)

    results = @redis.zrevrange(@leaderboard_key, 0, limit - 1, with_scores: true)

    results.map.with_index do |(friend_id, score), index|
      player = Player.find(friend_id)
      {
        rank: index + 1,
        player_id: friend_id.to_i,
        username: player.username,
        score: score.to_i
      }
    end
  end
end
```

### Percentile Rank

```ruby
class LeaderboardService
  # Get player's percentile rank
  def player_percentile(player_id, leaderboard_type: 'global')
    leaderboard_key = "leaderboard:#{leaderboard_type}"

    rank = @redis.zrevrank(leaderboard_key, player_id)
    return nil unless rank

    total_players = @redis.zcard(leaderboard_key)

    percentile = ((total_players - rank) / total_players.to_f) * 100

    {
      rank: rank + 1,
      total_players: total_players,
      percentile: percentile.round(2)
    }
  end
end
```

## Scaling Strategy

### Horizontal Scaling

**Redis Cluster:**
- Shard by leaderboard type
- Shard 1: Global leaderboards
- Shard 2: Regional leaderboards
- Shard 3: Friends leaderboards
- Each shard: 1 primary + 2 replicas

**API Servers:**
- Stateless, auto-scale based on request rate
- Minimum: 10 instances
- Maximum: 100 instances

### Memory Optimization

**Pruning Low-Ranked Players:**
```ruby
class LeaderboardPruningJob
  # Keep only top 10M players in Redis
  def perform
    leaderboard_key = 'leaderboard:global'

    total_players = redis.zcard(leaderboard_key)

    if total_players > 10_000_000
      # Remove bottom players
      players_to_remove = total_players - 10_000_000
      redis.zremrangebyrank(leaderboard_key, 0, players_to_remove - 1)
    end
  end
end
```

**Lazy Loading for Friends Leaderboards:**
- Don't pre-compute all friends leaderboards
- Build on-demand with 1-hour TTL
- Reduces memory by 90%

## High Availability Strategy

### Redis Sentinel for Failover

```ruby
# Configure Redis with Sentinel
redis = Redis.new(
  url: 'redis://sentinel-1:26379,sentinel-2:26379,sentinel-3:26379',
  sentinels: [
    { host: 'sentinel-1', port: 26379 },
    { host: 'sentinel-2', port: 26379 },
    { host: 'sentinel-3', port: 26379 }
  ],
  name: 'leaderboard-master',
  role: :master
)
```

### Fallback to PostgreSQL

```ruby
class LeaderboardService
  def top_players(n, leaderboard_type: 'global')
    # Try Redis first
    top_players_from_redis(n, leaderboard_type)
  rescue Redis::BaseError => e
    Rails.logger.error("Redis error: #{e.message}")
    # Fallback to PostgreSQL
    top_players_from_database(n, leaderboard_type)
  end

  private

  def top_players_from_database(n, leaderboard_type)
    # Query latest snapshot
    LeaderboardSnapshot
      .where(leaderboard_type: leaderboard_type, snapshot_date: Date.today)
      .order(rank: :asc)
      .limit(n)
      .map do |snapshot|
        {
          rank: snapshot.rank,
          player_id: snapshot.player_id,
          score: snapshot.score
        }
      end
  end
end
```

## Observability & Monitoring

### Key Metrics

```ruby
class LeaderboardMetrics
  def self.record_score_update(player_id, latency_ms)
    StatsD.increment('leaderboard.score_update')
    StatsD.histogram('leaderboard.update_latency', latency_ms)
  end

  def self.record_rank_query(player_id, latency_ms)
    StatsD.increment('leaderboard.rank_query')
    StatsD.histogram('leaderboard.query_latency', latency_ms)
  end

  def self.record_leaderboard_size(leaderboard_type, size)
    StatsD.gauge('leaderboard.size', size,
      tags: ["type:#{leaderboard_type}"])
  end
end
```

### Alerting

```yaml
alerts:
  - name: LeaderboardHighLatency
    condition: p99(leaderboard.query_latency) > 100ms
    duration: 5m
    severity: warning

  - name: LeaderboardRedisDown
    condition: leaderboard.redis_errors > 10
    duration: 1m
    severity: critical

  - name: LeaderboardMemoryHigh
    condition: redis_memory_usage > 80%
    duration: 5m
    severity: warning
```

## Testing Strategy

### Unit Tests

```ruby
RSpec.describe LeaderboardService do
  let(:redis) { MockRedis.new }
  let(:service) { described_class.new(redis) }

  describe '#update_score' do
    it 'updates player score and returns rank' do
      result = service.update_score(123, 1000)

      expect(result[:score]).to eq(1000)
      expect(result[:rank]).to eq(1)
    end

    it 'only updates if new score is higher' do
      service.update_score(123, 1000)
      result = service.update_score(123, 500)

      expect(result[:score]).to eq(1000)
      expect(result[:updated]).to be false
    end
  end

  describe '#top_players' do
    it 'returns top N players in order' do
      service.update_score(1, 1000)
      service.update_score(2, 2000)
      service.update_score(3, 1500)

      top = service.top_players(3)

      expect(top.map { |p| p[:player_id] }).to eq([2, 3, 1])
    end
  end
end
```

### Load Tests

```ruby
# Simulate 10K score updates/sec
require 'benchmark'

def load_test_score_updates
  service = LeaderboardService.new(redis)

  threads = 10.times.map do
    Thread.new do
      1000.times do |i|
        player_id = rand(1..100_000)
        score = rand(1..10_000)
        service.update_score(player_id, score)
      end
    end
  end

  threads.each(&:join)
end

Benchmark.bm do |x|
  x.report("10K updates:") { load_test_score_updates }
end
```

## Trade-offs & Alternatives

### Chosen: Redis Sorted Sets

**Pros:**
- O(log N) insert and rank query
- Built-in ranking
- Atomic operations
- Sub-millisecond latency

**Cons:**
- Memory-intensive
- Limited to single-server capacity
- Requires persistence strategy

**Alternative: PostgreSQL with Window Functions**

**Pros:**
- Durable storage
- Complex queries
- No memory limits

**Cons:**
- Slower (10-100ms vs <1ms)
- Doesn't scale to 10K writes/sec
- Requires materialized views

**Decision:** Redis for real-time, PostgreSQL for historical

---

### Cost Considerations

**Infrastructure:**
- Redis Cluster: $1500/month (3 shards × $500)
- PostgreSQL: $500/month
- API Servers: $2000/month

**Total:** ~$4000/month for 100M players
