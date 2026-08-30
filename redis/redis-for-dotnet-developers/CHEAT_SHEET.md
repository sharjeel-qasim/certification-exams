# ⚡ Redis for .NET Developers — Last-Minute Cram & Cheat Sheet

[![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)](https://redis.io/)
[![.NET](https://img.shields.io/badge/.NET_8%2F9-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)](https://dotnet.microsoft.com/)
[![Exam](https://img.shields.io/badge/Certification-Redis_for_.NET_Developers-red?style=for-the-badge)](#-high-frequency-exam-topics)

High-yield quick-reference cheat sheet for the **Redis Certified Developer for .NET** exam. Covers native data structures, Redis Stack modules (RedisJSON, RediSearch, TimeSeries), `StackExchange.Redis` C# client best practices, transactions, concurrency, persistence, and caching design patterns.

---

## 🔴 1. Redis Native Data Structures & CLI Commands

| Data Structure | Common Commands | Complexity | Exam Scenario / Use Case |
| :--- | :--- | :---: | :--- |
| **String** | `SET`, `GET`, `INCR`, `DECR`, `MSET`, `MGET`, `SETEX`, `EXPIRE` | \(O(1)\) | Page/API caching, distributed locks, session storage, counters |
| **Hash** | `HSET`, `HGET`, `HGETALL`, `HINCRBY`, `HDEL`, `HEXISTS`, `HMSET` | \(O(1)\) fields | Storing objects (e.g. `User:100` with `name`, `email`, `role`) without JSON serialization overhead |
| **List** | `LPUSH`, `RPUSH`, `LPOP`, `RPOP`, `LRANGE`, `LINDEX`, `LLEN`, `BRPOP` | \(O(1)\) push/pop | Message queues, FIFO/LIFO buffers, latest activity feeds, blocking consumer queues (`BRPOP`) |
| **Set** | `SADD`, `SMEMBERS`, `SISMEMBER`, `SREM`, `SCARD`, `SINTER`, `SUNION`, `SDIFF` | \(O(1)\) add/lookup | Unique tags, friend lists, intersection queries (common interests), deduplication |
| **Sorted Set (ZSet)** | `ZADD`, `ZRANGE`, `ZREVRANGE`, `ZRANGEBYSCORE`, `ZINCRBY`, `ZSCORE`, `ZCARD` | \(O(\log N)\) | Real-time leaderboards, rate limiters (sliding window), priority queues with floating-point scores |
| **Stream** | `XADD`, `XREAD`, `XRANGE`, `XREADGROUP`, `XACK`, `XPENDING`, `XGROUP CREATE` | \(O(1)\) append | Append-only event sourcing, distributed Kafka-like event streaming, multi-consumer group fanout |
| **HyperLogLog** | `PFADD`, `PFCOUNT`, `PFMERGE` | \(O(1)\) | Unique visitor / cardinality counting with **fixed 12 KB memory** (~0.81% standard error) |
| **Bitmap** | `SETBIT`, `GETBIT`, `BITCOUNT`, `BITOP` (`AND`, `OR`, `XOR`, `NOT`) | \(O(1)\) bit | Daily active user (DAU) tracking, user flags/permissions mapped to integer bit offsets |
| **Geospatial** | `GEOADD`, `GEODIST`, `GEOPOS`, `GEOSEARCH`, `GEORADIUS` | \(O(N + \log M)\) | Location-based queries, finding nearby drivers/stores within a radius |

---

## 🔴 2. Redis Stack Modules

### 1. RedisJSON (`JSON.*`)
- Manipulates JSON documents natively in-memory without deserializing the whole document.
- **Key Commands**:
  - `JSON.SET key path value` (e.g. `JSON.SET doc:1 $ '{"name":"Alice","age":30,"tags":["c#"]}'`)
  - `JSON.GET key [path]` (e.g. `JSON.GET doc:1 $.name`)
  - `JSON.NUMINCRBY key path number` (atomically increments numeric values inside JSON)
  - `JSON.ARRAPPEND key path value` (appends items to a JSON array)
- **JSONPath Expressions**:
  - `$` = Root object
  - `..` = Recursive descent
  - `$.users[?(@.age > 21)]` = Filter predicate

### 2. RediSearch (`FT.*`)
- Real-time indexing, full-text search, and secondary indexing over Hashes and JSON documents.
- **Schema Creation**:
  ```text
  FT.CREATE idx:users ON JSON PREFIX 1 user: SCHEMA $.name AS name TEXT $.age AS age NUMERIC $.role AS role TAG
  ```
- **Field Types**:
  - `TEXT`: Tokenized, stemmed full-text search with phonetic matching.
  - `TAG`: Exact-match identifiers (e.g. status `active`, categories, GUIDs). Comma-separated strings.
  - `NUMERIC`: Range filtering (`@age:[21 65]`).
  - `GEO`: Coordinates (`@location:[lon lat radius km]`).
  - `VECTOR`: Vector similarity search (k-NN, HNSW, Flat) for AI embeddings.

### 3. Redis TimeSeries (`TS.*`)
- High-throughput ingestion of time-series data with automatic downsampling and retention.
- **Key Commands**: `TS.CREATE`, `TS.ADD`, `TS.RANGE`, `TS.MRANGE`, `TS.CREATERULE` (for compaction rules: `avg`, `min`, `max`, `sum`, `count`).

---

## 🔴 3. `StackExchange.Redis` Best Practices in C# (.NET)

### ⚙️ Lifecycle & Connection Management
```csharp
// MUST be registered as a SINGLETON in DI (never create per-request)
builder.Services.AddSingleton<IConnectionMultiplexer>(sp =>
{
    var config = ConfigurationOptions.Parse("localhost:6379");
    config.AbortOnConnectFail = false; // CRITICAL: Prevents app startup crash if Redis is recovering
    config.ConnectTimeout = 5000;
    config.SyncTimeout = 5000;
    config.ConnectRetry = 3;
    config.KeepAlive = 60;
    return ConnectionMultiplexer.Connect(config);
});
```

### ⚡ Database Access (`IDatabase` vs `IServer`)
- **`IDatabase db = muxer.GetDatabase(dbNumber);`**
  - Extremely cheap struct allocation (zero network overhead).
  - Default database is `0`. Note: Redis Cluster only supports database `0`.
- **`IServer server = muxer.GetServer("localhost:6379");`**
  - Used for administrative commands: `server.Keys()`, `server.FlushDatabase()`, `server.Info()`.
  - In production, **never use raw `KEYS *`** (blocks single-threaded event loop). `IServer.Keys()` in `StackExchange.Redis` automatically uses non-blocking **`SCAN`**.

### 🔒 Transactions & Optimistic Concurrency (WATCH / MULTI / EXEC)
```csharp
var tran = db.CreateTransaction();

// Add optimistic concurrency conditions (WATCH)
tran.AddCondition(Condition.StringEqual("account:balance", "100"));

// Queue commands (MULTI)
_ = tran.StringSetAsync("account:balance", "50");
_ = tran.ListRightPushAsync("account:history", "debit:50");

// Commit transaction (EXEC)
bool committed = await tran.ExecuteAsync();
if (!committed)
{
    // Concurrency conflict occurred (watched key was modified by another client)
}
```

### 📡 Pub/Sub vs Interactive Connection
- `muxer.GetSubscriber()` establishes a **dedicated socket connection** because Redis pub/sub connections cannot execute standard data commands while subscribed to channels.

---

## 🔴 4. Caching Patterns & Eviction Policies

| Caching Pattern | Read Flow | Write Flow | Pros & Cons |
| :--- | :--- | :--- | :--- |
| **Cache-Aside (Lazy Loading)** | App reads cache ➔ on miss, reads DB ➔ writes to cache | App updates DB ➔ **invalidates (deletes) cache entry** | Most resilient; cache only contains requested data; write ordering prevents race conditions |
| **Write-Through** | App reads cache ➔ on miss, reads DB | App writes to cache ➔ Cache updates DB synchronously | Data in cache is never stale; higher write latency |
| **Write-Behind (Write-Back)** | App reads cache | App writes to cache ➔ Cache writes asynchronously to DB in batches | Highest write throughput; potential data loss if cache crashes before flush |

### 🧹 Memory Eviction Policies (`maxmemory-policy`)
- **`allkeys-lru`**: Evicts Least Recently Used keys out of **all keys** (Best general-purpose cache policy).
- **`volatile-lru`**: Evicts LRU keys among keys with an **expiration (`TTL`) set**.
- **`allkeys-lfu`**: Evicts Least Frequently Used keys (evicts keys with lowest access frequency counter).
- **`volatile-lfu`**: Evicts LFU keys among keys with an expiration set.
- **`volatile-ttl`**: Evicts keys with the shortest remaining Time-To-Live.
- **`noeviction`**: Returns Out-Of-Memory (`OOM`) errors on write commands when memory limit is reached (default).

---

## 🔴 5. Persistence, High Availability & Clustering

| Feature | Mechanism | Trade-offs & High-Yield Exam Facts |
| :--- | :--- | :--- |
| **RDB (Snapshot)** | `BGSAVE` forks child process to write point-in-time binary snapshot (`dump.rdb`). | Fast recovery, compact disk footprint, but potential data loss of writes since last snapshot. |
| **AOF (Append-Only File)** | Logs every write operation to `appendonly.aof` (`appendfsync everysec` default). `BGREWRITEAOF` compacts. | Maximum durability (minimal data loss), but larger file size and slower startup replay than RDB. |
| **Replication** | Asynchronous master-to-replica replication. | Read scaling and redundancy; asynchronous nature means slight replication lag. |
| **Redis Sentinel** | External monitoring daemons that monitor primary and replica instances. | Performs **automatic failover** when the primary node fails and reconfigures replicas. |
| **Redis Cluster** | Horizontal sharding across **16,384 hash slots** (`CRC16(key) % 16384`). | Auto-sharding across master nodes. Use **hash tags** (e.g. `{user:100}:profile` and `{user:100}:orders`) to guarantee multi-key operations land on the same hash slot. |

---

## 🔴 6. High-Frequency Exam Trap Alerts 🚨

> [!WARNING]
> - **Trap 1:** Never instantiate `ConnectionMultiplexer` per request or inside a `using` block. It is thread-safe and designed as a long-lived Singleton.
> - **Trap 2:** `IServer.Keys()` does **NOT** block the server like CLI `KEYS *` does — it uses `SCAN` in batches under the hood.
> - **Trap 3:** Multi-key operations (`MGET`, Transactions, Lua scripts) in Redis Cluster fail with `CROSSSLOT` error unless all keys use matching `{hash_tag}` curly brackets.
> - **Trap 4:** In Cache-Aside write operations, always **update the database first, then delete (invalidate) the cache key** (do not update cache first).
> - **Trap 5:** Setting `AbortOnConnectFail = false` is critical in cloud environments so your .NET app boots successfully even if Redis is reconnecting.
