# Redis for .NET Developers — Certification Exam Preparation Guide

[![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)](https://redis.io/)
[![.NET](https://img.shields.io/badge/.NET-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)](https://dotnet.microsoft.com/)
[![StackExchange.Redis](https://img.shields.io/badge/StackExchange.Redis-v2.x-blue?style=for-the-badge)](https://stackexchange.github.io/StackExchange.Redis/)
[![Questions](https://img.shields.io/badge/Questions-65%20Verified-success?style=for-the-badge)](#table-of-contents)

Comprehensive study guide and question bank for the **Redis for .NET Developers** certification. This guide covers core Redis architectural concepts, the `StackExchange.Redis` and `NRedisStack` client libraries, advanced data structures, caching patterns, concurrency, transactions, persistence, and production operations.

> [!NOTE]
> **Study Format**: In accordance with high-retention learning practices, each question displays **only the verified correct answer(s)** alongside in-depth architectural and code-level explanations. Incorrect distractors have been omitted so you focus strictly on correct patterns and behaviors.

---

## Table of Contents

- [Domain 1: Redis Fundamentals, Architecture & RESP Protocol (Q1 – Q5)](#domain-1-redis-fundamentals-architecture--resp-protocol)
- [Domain 2: StackExchange.Redis Connection & Multiplexing (Q6 – Q10)](#domain-2-stackexchangeredis-connection--multiplexing)
- [Domain 3: Hashes & Field Operations (Q11 – Q15)](#domain-3-hashes--field-operations)
- [Domain 4: RedisJSON, Hierarchies & JSONPath (Q16 – Q20)](#domain-4-redisjson-hierarchies--jsonpath)
- [Domain 5: Caching Strategies & The Cache-Aside Pattern (Q21 – Q25)](#domain-5-caching-strategies--the-cache-aside-pattern)
- [Domain 6: Query Result Caching & Stale-While-Revalidate (Q26 – Q30)](#domain-6-query-result-caching--stale-while-revalidate)
- [Domain 7: Key Lifecycles, Expiration (TTL) & Persistence (Q31 – Q35)](#domain-7-key-lifecycles-expiration-ttl--persistence)
- [Domain 8: Transactions, Batches & Concurrency Patterns (Q36 – Q40)](#domain-8-transactions-batches--concurrency-patterns)
- [Domain 9: Keyspace Inspections, Memory & Namespace Design (Q41 – Q43)](#domain-9-keyspace-inspections-memory--namespace-design)
- [Domain 10: Lists & Capped Event Feeds (Q44 – Q48)](#domain-10-lists--capped-event-feeds)
- [Domain 11: Sets & Server-Side Set Operations (Q49 – Q53)](#domain-11-sets--server-side-set-operations)
- [Domain 12: Sorted Sets & Real-Time Leaderboards (Q54 – Q58)](#domain-12-sorted-sets--real-time-leaderboards)
- [Domain 13: Advanced JSONPath Filters & Merge Patching (Q59 – Q61)](#domain-13-advanced-jsonpath-filters--merge-patching)
- [Domain 14: Production Operations, UNLINK & Bulk Processing (Q62 – Q65)](#domain-14-production-operations-unlink--bulk-processing)

---

## Domain 1: Redis Fundamentals, Architecture & RESP Protocol

### Question 1
**Which of the following are accurate statements about Redis?**

#### ✅ Correct Answers
1. **Redis supports configurable persistence mechanisms that allow data to survive process restarts when enabled.**
2. **Redis stores data primarily in main memory (RAM), which is why it achieves lower latency than disk-based databases for read and write operations.**

#### 💡 Explanation
- **RAM Residency & Microsecond Latency**: Redis is designed from the ground up as an in-memory data store where all active datasets reside in RAM.
- **Configurable Persistence**: Durability is opt-in and configurable via RDB (point-in-time snapshots) and AOF (append-only logs).
- **Behavior at Memory Limits**: When Redis hits `maxmemory` under the default `noeviction` policy, it rejects incoming *write* commands with an OOM error while continuing to serve *read* commands normally.
- **Concurrency Model**: Redis processes database commands sequentially on a single-threaded event loop, avoiding locking overhead on data access.
- **Server-Side Data Structures**: Hashes, Lists, Sets, and Sorted Sets are native, server-side data types executed inside Redis, not client-side abstractions.

---

### Question 2
**You're inspecting the raw traffic between the client and server on an application using Redis. Which of the following are true about RESP (Redis Serialization Protocol)?**

#### ✅ Correct Answers
1. **Clients send commands to the Redis server as RESP arrays of bulk strings. For example, `SET mykey myvalue` is transmitted as an array of three bulk strings: `SET`, `mykey`, and `myvalue`.**
2. **RESP responses are type-prefixed — the first byte of each response indicates its wire type, such as `+` for simple strings, `-` for errors, and `:` for integers. This allows parsers to determine how to read each response from the byte stream.**

#### 💡 Explanation
- **Wire Framing**: RESP is a human-readable, binary-safe protocol. Client commands are transmitted as arrays of bulk strings formatted as `*<arg_count>\r\n$<len>\r\n<arg>\r\n...`.
- **Type Identifiers**:
  - `+` Simple String (e.g. `+OK\r\n`)
  - `-` Error (e.g. `-ERR unknown command\r\n`)
  - `:` Integer (e.g. `:1000\r\n`)
  - `$` Bulk String (e.g. `$6\r\nfoobar\r\n`)
  - `*` Array (e.g. `*2\r\n...`)
- **Transport Security**: RESP is unencrypted plain text by default and can be inspected using tools like `tcpdump` or Wireshark. Production TLS encryption is configured at the transport layer.

---

### Question 3
**Which statement most accurately describes Redis transactions?**

#### ✅ Correct Answer
**Redis transactions queue commands until `EXEC`, then execute them sequentially without interleaving from other clients, but Redis does not support rollback.**

#### 💡 Explanation
- Initiated with `MULTI`, commands are queued on the server and executed sequentially upon receiving `EXEC`.
- Redis guarantees isolation and sequential execution without command interleaving from other connections.
- **No Rollback**: If a command produces a runtime error during execution (e.g., executing a list command on a string key), subsequent commands still execute and prior commands are not reverted.

---

### Question 4
**Which of the following is NOT an example of an atomic operation in Redis?**

#### ✅ Correct Answer
**Executing a series of commands in a pipeline.**

#### 💡 Explanation
- **Individual Command Atomicity**: Every individual Redis command (e.g. `LPUSH`, `UNLINK`, `INCR`, `HSET`) executes atomically on the single-threaded engine.
- **Pipelining**: Batches network round-trips by writing multiple commands to the socket at once. Redis executes each command in the pipeline individually; commands from other clients can interleave between pipelined commands.
- For multi-command atomicity, use Redis transactions (`MULTI`/`EXEC`) or server-side Lua scripts.

---

### Question 5
**Which of the following are valid Redis key names under Redis's default key-size limit?**

#### ✅ Correct Answers
1. **The raw bytes of a PDF file, approximately 120 KB in size**
2. **`""` (an empty string)**
3. **A key made of the letter `"a"` repeated until the key is 512 MB long**
4. **The "winking face" emoji**

#### 💡 Explanation
- Redis keys are binary-safe byte sequences up to a maximum size of **512 MB**.
- Binary files, empty strings, Unicode characters, and emojis are all legal key names.
- Payloads exceeding 512 MB (such as a 1 GB payload) violate the key limit.

---

## Domain 2: StackExchange.Redis Connection & Multiplexing

### Question 6
**Your operations team monitors the Redis server and notices that your .NET application is maintaining 2 physical TCP connections, even though you only created a single `ConnectionMultiplexer` instance. What is the explanation for this?**

#### ✅ Correct Answer
**The `ConnectionMultiplexer` creates one connection for interactive commands and a separate dedicated connection for pub/sub subscriptions.**

#### 💡 Explanation
- `StackExchange.Redis` shares a single primary TCP connection across all threads for interactive commands (`GET`, `SET`, `HSET`, etc.).
- When Pub/Sub subscriptions are established, Redis protocol requires the socket to enter subscription mode, where it can only process subscription commands. `ConnectionMultiplexer` automatically provisions a dedicated second TCP connection for Pub/Sub.
- `IDatabase` objects obtained via `GetDatabase()` are lightweight, stateless structures that do not open additional sockets.

---

### Question 7
**Under load, 50 concurrent requests each issue Redis commands at the same time through a shared `ConnectionMultiplexer`. You're concerned about commands "stepping on each other" over the shared connection. How does the `ConnectionMultiplexer` handle this?**

#### ✅ Correct Answer
**It sends commands from all threads over a shared connection without waiting for each response before sending the next. The library tracks which response belongs to which caller and dispatches results back to the correct thread as they arrive.**

#### 💡 Explanation
- `StackExchange.Redis` implements **multiplexing** and pipelining over a single connection.
- Commands from multiple concurrent threads are queued and written to the socket continuously.
- Each command is mapped to a pending completion token; as responses stream back in FIFO order, the multiplexer routes the result to the awaiting `Task`.

---

### Question 8
**How should `StackExchange.Redis` handle connection failures when the Redis server might be unavailable at application startup?**

#### ✅ Correct Answer
Add `abortConnect=false` to the connection string:
```text
"redis-server:6379,abortConnect=false"
```
**This tells the `ConnectionMultiplexer` not to throw an exception if the initial connection attempt fails. Instead, it continues retrying in the background until the Redis server becomes available.**

#### 💡 Explanation
- By default, `abortConnect=true` throws an exception immediately if the server cannot be reached during initialization.
- Setting `abortConnect=false` enables non-blocking background connection recovery, which is essential in cloud environments (e.g. Kubernetes, container start order) where Redis may take a few seconds to become ready.

---

### Question 9
**Your .NET application uses a shared `ConnectionMultiplexer` singleton. During a planned Redis server restart, the server goes offline for approximately 10 seconds. What happens to Redis commands issued by your application during this window?**

#### ✅ Correct Answer
**The `ConnectionMultiplexer` reconnects automatically in the background. Commands issued while Redis is unavailable may fail with timeout or connection exceptions; the application should handle those failures and retry only when safe.**

#### 💡 Explanation
- `ConnectionMultiplexer` manages auto-reconnection internally without requiring manual disposal or re-instantiation.
- In-flight commands during the outage fail with transient exceptions.
- Applications should implement resilience policies (e.g., Polly retry with exponential backoff or fallback paths) rather than creating new multiplexers.

---

### Question 10
**After a deployment, you need to run the `INFO` command from your .NET application to check memory usage on the Redis server. How do you access server-level commands?**

#### ✅ Correct Answer
**Server commands like `INFO` are accessed through `IServer`, obtained via `redis.GetServer("host", port)`. This interface exposes methods like `Info()`, `FlushDatabase()`, and `Keys()` that are intentionally absent from `IDatabase`.**

#### 💡 Explanation
- `StackExchange.Redis` separates data keyspace operations (`IDatabase`) from server/infrastructure commands (`IServer`).
- Server administration methods (`Info()`, `ClientList()`, `FlushDatabase()`, `Keys()`) target specific nodes via `IServer`.
- Note: Administrative commands like `FlushDatabase` and `Keys` require `allowAdmin=true` in the connection string, though `Info()` is always accessible.

---

## Domain 3: Hashes & Field Operations

### Question 11
**Your team is deciding how to cache product records. One developer proposes storing each product as a serialized JSON string like `'{"name":"Widget","price":9.99,"stock":150}'`. Another proposes using a Hash. The application frequently updates stock counts without touching other fields. What is the strongest argument for choosing a Hash over a serialized String in this case?**

#### ✅ Correct Answer
**A Hash allows updating the `stock` field directly without deserializing and rewriting the entire record.**

#### 💡 Explanation
- **Granular Updates**: With a Redis Hash, `HSET` or `HINCRBY` updates only the `stock` field in a single round-trip.
- **Reduced Network & CPU Overhead**: A serialized JSON string requires fetching the full string, deserializing the JSON object, modifying the property, serializing the JSON, and writing the entire string back to Redis.

---

### Question 12
**You cache a product for the first time, then immediately update its stock:**
```csharp
db.HashSet("product:42", new HashEntry[] {
    new("name", "Widget"),
    new("price", "9.99"),
    new("category", "gadgets"),
    new("stock", "150")
});

bool result = db.HashSet("product:42", "stock", "125");
```
**What is the value of `result` and why?**

#### ✅ Correct Answer
**`false` — when setting a single field, `HashSet` returns `true` if the field is new and `false` if the field already existed and was updated. Since `stock` already existed, the return is `false`.**

#### 💡 Explanation
- The Redis `HSET` command returns `1` if a new field was created, and `0` if an existing field was updated.
- `StackExchange.Redis` maps `1` to `true` (novelty) and `0` to `false`. The update is applied in both cases.

---

### Question 13
**After a flash sale ends, a cleanup routine removes the discount field from all product Hashes using `HDEL`. For one product, `discount` was the only field in the Hash. A developer on your team assumes the key still exists afterward and schedules a separate `UNLINK` job to remove it later. What actually happens?**

#### ✅ Correct Answer
**Redis automatically deletes the key when its last field is removed. There is no such thing as an empty Hash in Redis. The scheduled `UNLINK` job is unnecessary.**

#### 💡 Explanation
- Redis collections (Hashes, Sets, Sorted Sets, Lists) do not exist in an empty state.
- When the final element/field is removed via `HDEL`, `SREM`, `LPOP`, or `ZREM`, Redis immediately deletes the key from the keyspace.

---

### Question 14
**You're building a product page that displays only the item's name and price. The product is cached as a Hash with six fields: name, price, category, stock, weight, and supplier. Which call fetches exactly the fields you need in a single round trip, without retrieving unnecessary data?**

#### ✅ Correct Answer
```csharp
db.HashGet("product:42", new RedisValue[] { "name", "price" });
```

#### 💡 Explanation
- Passing an array of field names to `db.HashGet()` translates to the Redis `HMGET` command.
- It returns an array of `RedisValue` for only the requested fields in a single round trip.

---

### Question 15
**A supplier import job refreshes name, price, and stock on every run, but the `firstSeenAt` field in each product Hash should be written only the first time the product appears. Multiple workers may process the same product at the same time. Which approach is best?**

#### ✅ Correct Answer
**Use `HSETNX product:42 firstSeenAt <timestamp>` for that field, and use `HSET` for mutable fields like `name`, `price`, and `stock`.**

#### 💡 Explanation
- `HSETNX` (Hash Set if Not Exists) sets a hash field only if it does not yet exist.
- It is evaluated atomically on the server, eliminating race conditions across multiple concurrent workers.

---

## Domain 4: RedisJSON, Hierarchies & JSONPath

### Question 16
**Your team has been caching flat product records as Hashes. A new requirement arrives: each product now includes a nested `dimensions` object with `width`, `height`, and `weight` fields, as well as an array of `tags`. A team member suggests migrating from Hashes to JSON. What is the strongest reason to consider this change for this data model?**

#### ✅ Correct Answer
**JSON allows you to read and update nested paths like `$.dimensions.weight` directly, whereas a Hash would require you to flatten the structure or serialize the nested data into a single field.**

#### 💡 Explanation
- Hashes support only flat key-value pairs. Storing nested objects in hashes requires artificial delimiter schemes or embedding serialized blobs.
- **RedisJSON** provides native document support, allowing direct manipulation of nested properties and arrays using JSONPath syntax.

---

### Question 17
**You store a product as a Redis JSON document with nested fields and an array of tags. Which statement best explains why the application must handle RedisJSON path results carefully?**

#### ✅ Correct Answer
**Paths using `$` can return arrays of matches, even when the path currently matches one value.**

#### 💡 Explanation
- JSONPath expressions starting with `$` are multi-match queries.
- RedisJSON returns results wrapped in an array (e.g. `["value"]`), so client code must extract the element rather than assuming a bare scalar return.

---

### Question 18
**A supplier notifies you that the weight for product 42 has changed. The product document includes a nested `dimensions` object with `width`, `height`, and `weight` fields. You need to update only `weight` without replacing the rest of the document. Which call accomplishes this?**

#### ✅ Correct Answer
```csharp
json.Set("product:42", "$.dimensions.weight", 0.6);
```

#### 💡 Explanation
- `JSON.SET` targeting a specific JSONPath (`$.dimensions.weight`) updates only the targeted property in-place.
- Using root path `"$"` would overwrite the entire document.

---

### Question 19
**Your team is running a seasonal promotion where certain product tags need to be removed when the sale ends. You review the following cleanup code. The product had tags: `["gadget", "sale"]`. After this runs, you retrieve the full product. What happened to the document?**
```csharp
var json = db.JSON();
var removed = json.Del("product:42", "$.tags");
Console.WriteLine(removed);
var product = json.Get("product:42", path: "$");
```

#### ✅ Correct Answer
**The `tags` field was removed from the document entirely — the product still exists but no longer has a `tags` property.**

#### 💡 Explanation
- `JSON.DEL` on path `$.tags` deletes the property itself from the JSON document.
- The document remains intact with all other fields preserved.

---

### Question 20
**After running both Hashes and JSON documents in production for several weeks, your team is establishing guidelines for when to use each. Which of the following is a valid guideline?**

#### ✅ Correct Answer
**Use JSON when the data has nested structures or arrays that need to be queried or updated by path; use Hashes when the data is a flat set of field-value pairs with no nesting.**

#### 💡 Explanation
- **Hashes**: Optimum performance and lower memory overhead for flat, dictionary-like key-value structures.
- **RedisJSON**: Optimum for complex, nested, hierarchical documents and array manipulations.

---

## Domain 5: Caching Strategies & The Cache-Aside Pattern

### Question 21
**Your team is implementing cache-aside for product lookups. A request comes in for a product that is not currently in Redis. Which sequence of steps correctly describes the cache-aside pattern for handling this cache miss?**

#### ✅ Correct Answer
**The application reads from Redis and gets a miss, queries the database, writes the result to Redis, and returns it to the caller.**

#### 💡 Explanation
- **Cache-Aside Flow**:
  1. Check Redis cache.
  2. If missing, fetch from the database (source of truth).
  3. Write data to Redis (typically with a TTL).
  4. Return data to client.

---

### Question 22
**When a product's price is updated in the database, the cached copy in Redis becomes stale. You're reviewing two approaches your team proposed:**

**Approach A:**
```csharp
public async Task UpdatePriceAsync(IDatabase db, int productId, string newPrice)
{
    await _repository.UpdateProductPriceAsync(productId, newPrice);
    await db.HashSetAsync($"product:{productId}", "price", newPrice);
}
```

**Approach B:**
```csharp
public async Task UpdatePriceAsync(IDatabase db, int productId, string newPrice)
{
    await _repository.UpdateProductPriceAsync(productId, newPrice);
    await db.KeyDeleteAsync($"product:{productId}");
}
```

**Which approach is more consistent with the cache-aside pattern, and why?**

#### ✅ Correct Answer
**Approach B, because cache-aside treats the database as the source of truth. Deleting the key forces the next read to repopulate from the database, avoiding write-path inconsistency.**

#### 💡 Explanation
- Invalidate (delete) rather than update.
- Mutating the cache directly on writes introduces race conditions where concurrent updates can leave the cache out of sync with the database. Deleting the key ensures subsequent reads fetch fresh, authoritative data.

---

### Question 23
**Your team is configuring Redis with `maxmemory` for a cache-aside layer. Some cached keys have TTLs and some do not. Which statement correctly describes how `allkeys-lru`, `volatile-lru`, and `noeviction` differ when Redis runs out of memory?**

#### ✅ Correct Answer
**`allkeys-lru` can evict any key based on recent use, `volatile-lru` can evict only keys that have an expiration set, and `noeviction` rejects writes that would exceed the memory limit.**

#### 💡 Explanation
- **`allkeys-lru`**: Evicts least recently used keys across the entire database.
- **`volatile-lru`**: Evicts least recently used keys only among keys configured with a TTL expiration.
- **`noeviction`**: Returns an error on writes when memory limit is reached; serves reads.

---

### Question 24
**Your Redis instance is configured with `maxmemory` and the `allkeys-lru` eviction policy. During a traffic spike, Redis starts evicting cached product keys to stay within the memory limit. How does this affect your cache-aside implementation?**

#### ✅ Correct Answer
**The application continues to function correctly — evicted keys appear as cache misses, and the cache-aside logic repopulates them from the database on the next read.**

#### 💡 Explanation
- Cache-aside is inherently eviction-tolerant.
- An evicted key is indistinguishable from a cold cache entry and is repopulated seamlessly from the primary database.

---

### Question 25
**You're load testing your cache-aside implementation and notice that immediately after a product update, some requests return stale data. Here's the relevant code:**
```csharp
public async Task UpdatePriceAsync(IDatabase db, int productId, string newPrice)
{
    await db.KeyDeleteAsync($"product:{productId}");
    await _repository.UpdateProductPriceAsync(productId, newPrice);
}

public async Task<Product> GetProductAsync(IDatabase db, int productId)
{
    var cached = await db.HashGetAllAsync($"product:{productId}");
    if (cached.Length == 0)
    {
        var product = await _repository.GetProductAsync(productId);
        await db.HashSetAsync($"product:{productId}", ToHashEntries(product));
        return product;
    }
    return ToProduct(cached);
}
```
**What is causing the stale data?**

#### ✅ Correct Answer
**The cache is deleted *before* the database is updated. A concurrent `GetProductAsync` call between `KeyDeleteAsync` and the database write can read the old price from the database and re-cache it.**

#### 💡 Explanation
- Order of execution is critical:
  1. Write updates to the primary database first.
  2. Invalidate / delete the cache key afterward.
- Deleting the key prior to database commit allows concurrent reads to cache stale database data that persists until TTL expiration.

---

## Domain 6: Query Result Caching & Stale-While-Revalidate

### Question 26
**Your team has been caching individual product records as Hashes. Now the product listing page, which returns filtered results like "all gadgets under $20 sorted by price," is generating a heavy database load. You need to cache these full result sets. Why is a String more appropriate than a Hash for caching a query result?**

#### ✅ Correct Answer
**A String is more appropriate because a query result is a pre-computed response with no need to read or update individual fields, so serializing it into a single value is simpler than mapping it to Hash fields.**

#### 💡 Explanation
- Query result sets represent read-only, aggregate payloads.
- Storing them as serialized JSON strings into Redis String keys minimizes serialization overhead and simplifies cache reads.

---

### Question 27
**Your team caches many listing-page query results with a 5-minute TTL (`EX: 300`). Product managers report that price changes can leave some listing pages stale for up to 5 minutes. A teammate proposes lowering the TTL to 15 seconds. What is the main tradeoff across the query cache?**

#### ✅ Correct Answer
**The cache hit rate will drop. More query results will expire before reuse, causing more reads to fall through to the database.**

#### 💡 Explanation
- Reducing TTL trades cache freshness for database hit rate.
- Lower TTLs mean keys expire rapidly, causing increased database load on repeated queries.

---

### Question 28
**You're implementing async query caching for the product listing page. Your team has agreed on the key schema `query:{category}:{sort}:{page}`. You need to write a method that checks the cache first, falls through to the database on a miss, caches the result, and returns it. Which implementation is correct?**

#### ✅ Correct Answer
```csharp
public async Task<List<Product>> GetProductsAsync(IDatabase db, string category, string sort, int page)
{
    var key = $"query:{category}:{sort}:{page}";
    var cached = await db.StringGetAsync(key);
    if (!cached.IsNull) return JsonSerializer.Deserialize<List<Product>>(cached);

    var results = await _repository.GetProductsAsync(category, sort, page);
    await db.StringSetAsync(key, JsonSerializer.Serialize(results), TimeSpan.FromSeconds(300));
    return results;
}
```

#### 💡 Explanation
- Reads from cache using `StringGetAsync`.
- Verifies `!cached.IsNull` and deserializes JSON on hit.
- Queries repository, serializes result, and saves with a TTL (`TimeSpan.FromSeconds(300)`) on miss.

---

### Question 29
**During a flash sale, one listing query is requested hundreds of times per second. The cached result can be up to 60 seconds stale, but the team wants to avoid a database spike when the normal TTL is reached while keeping response latency low. Which query-caching strategy best fits this situation?**

#### ✅ Correct Answer
**Use stale-while-revalidate with soft and hard TTLs. Serve the cached result briefly while one worker refreshes it.**

#### 💡 Explanation
- **Stale-While-Revalidate (SWR)**:
  - If soft TTL has expired, immediately return the cached data to incoming callers without blocking.
  - Asynchronously trigger a background refresh to fetch fresh data from the database and update Redis.
  - Prevents cache stampedes on hot query keys.

---

### Question 30
**Your team is investigating two patterns of unexpected key removal in Redis. In the first, a product key is consistently gone after the same amount of time regardless of how frequently it is accessed. In the second, product keys disappear only during high write volume, Redis memory usage is at its configured limit, and the server's eviction counter is increasing. What is the most likely explanation for each scenario?**

#### ✅ Correct Answer
**The first is TTL-based expiration. Redis removed the key after its time-to-live elapsed, regardless of access patterns. The second is memory-based eviction. Redis hit its `maxmemory` limit and began removing keys as new writes arrived.**

#### 💡 Explanation
- **TTL Expiration**: Governed by time elapsed since key creation or expiration configuration, independent of access frequency.
- **Memory Eviction**: Triggered when memory exceeds `maxmemory`, causing Redis to evict keys according to its eviction policy.

---

## Domain 7: Key Lifecycles, Expiration (TTL) & Persistence

### Question 31
**You're debugging a caching issue and need to check when a specific product key is set to expire. You run `EXPIRETIME product:42` in the Redis CLI. Under which conditions would this command return `-1`?**

#### ✅ Correct Answer
**The key `product:42` exists but has no expiration set — it will persist until explicitly deleted or evicted.**

#### 💡 Explanation
- `EXPIRETIME` / `TTL` return codes:
  - `> 0`: Unix timestamp (`EXPIRETIME`) or seconds remaining (`TTL`).
  - `-1`: Key exists, but has no TTL set (persistent).
  - `-2`: Key does not exist.

---

### Question 32
**Your team cached products with a 5-minute TTL using `await db.StringSetAsync(key, data, TimeSpan.FromSeconds(300))`. Later, a new feature was added that updates the cached stock count whenever inventory changes:**
```csharp
public async Task UpdateCachedStockAsync(IDatabase db, int productId, int newStock)
{
    var key = $"product:{productId}";
    var cached = await db.StringGetAsync(key);
    if (!cached.IsNull)
    {
        var product = JsonSerializer.Deserialize<Product>(cached);
        product.Stock = newStock;
        await db.StringSetAsync(key, JsonSerializer.Serialize(product));
    }
}
```
**After deploying this feature, the ops team notices that some product keys are never expiring. What is the root cause?**

#### ✅ Correct Answer
**The `StringSetAsync` call in the update method overwrites the key without specifying a TTL. That discards the existing expiration, so the key persists until deleted or evicted.**

#### 💡 Explanation
- Calling `SET` (`StringSetAsync`) without an expiration or `keepTtl: true` clears any previously set TTL and converts the key into a permanent key.

---

### Question 33
**You have a product cached as a Hash with a 5-minute TTL:**
```csharp
db.HashSet("product:42", new HashEntry[] {
    new("name", "Widget"),
    new("price", "9.99"),
    new("stock", "150")
});
db.KeyExpire("product:42", TimeSpan.FromSeconds(300));

// Later:
db.HashSet("product:42", "stock", "125");
```
**What happens to the TTL on `product:42` after the update call?**

#### ✅ Correct Answer
**The TTL is unaffected — `HashSet` updates a field within the Hash without replacing the key itself, so the existing expiration continues counting down from where it was.**

#### 💡 Explanation
- Key expiration in Redis belongs to the root key, not individual hash fields.
- Sub-field mutations via `HSET` or `HDEL` do not overwrite the key object or alter its expiration schedule.

---

### Question 34
**Your team is evaluating persistence for a Redis product cache that uses cache-aside in front of a relational database. Redis is not the source of truth, and losing the most recent few minutes of cached entries after a crash is acceptable. The main goal is to avoid a completely cold cache after restart while keeping normal cache writes lightweight and restart loading fast. Which persistence strategy best fits this priority?**

#### ✅ Correct Answer
**Enable RDB snapshots at regular intervals so Redis can restart from a recent point-in-time cache state.**

#### 💡 Explanation
- RDB snapshots create compact binary dumps via background fork (`BGSAVE`).
- Provides fast startup recovery times and zero I/O overhead on main-thread write commands, perfect for caching layers where minor data loss on crash is acceptable.

---

### Question 35
**When a customer views a product page, your application needs to perform three Redis operations:**
1. Fetch the cached product data
2. Increment the page view counter
3. Check if the product is in the user's wishlist set.
**None of these operations depend on each other's results. A team member suggests wrapping them in a transaction using `MULTI/EXEC`. Another suggests using a batch. Which approach is more appropriate and why?**

#### ✅ Correct Answer
**A batch is more appropriate because the three operations are independent reads and writes with no need for atomicity. A batch groups them for efficiency without adding transactional guarantees that are not needed here.**

#### 💡 Explanation
- Batches pipeline commands over the network into a single round-trip without imposing transactional locking overhead on the server.
- Transactions are reserved for multi-step atomic operations where isolation is required.

---

## Domain 8: Transactions, Batches & Concurrency Patterns

### Question 36
**When a customer adds a product to their cart, your application needs to atomically decrement the stock count and add the product to the customer's cart Set. You review the following implementation:**
```csharp
public async Task AddToCartAsync(IDatabase db, string productId, string customerId)
{
    var tran = db.CreateTransaction();
    var stockTask = tran.HashIncrementAsync($"product:{productId}", "stock", -1);
    var cartTask = tran.SetAddAsync($"cart:{customerId}", productId);
    await tran.ExecuteAsync();
    Console.WriteLine($"Stock: {await stockTask}, Cart added: {await cartTask}");
}
```
**The product's stock is currently 10 and the customer's cart is empty. What values are printed for Stock and Cart added?**

#### ✅ Correct Answer
**Stock is 9 and Cart added is true. `HashIncrementAsync` returns the new value after increment, and `SetAddAsync` returns true because the member was new to the Set.**

#### 💡 Explanation
- In `StackExchange.Redis`, transaction task results complete once `tran.ExecuteAsync()` returns.
- `HINCRBY` returns the updated numeric value (`10 - 1 = 9`).
- `SADD` returns `1` (`true`) when the member is newly added to the set.

---

### Question 37
**Your team implements a last-item purchase check using a read-then-write pattern:**
```csharp
public async Task AddToCartAsync(IDatabase db, string productId, string customerId)
{
    var stockValue = await db.HashGetAsync($"product:{productId}", "stock");
    var stock = int.Parse(stockValue!);
    if (stock > 0)
    {
        await db.HashSetAsync($"product:{productId}", "stock", stock - 1);
        await db.SetAddAsync($"cart:{customerId}", productId);
    }
    else
    {
        throw new Exception("Out of stock");
    }
}
```
**During load testing with stock set to 1, two customers call this function simultaneously. Both succeed in adding the product to their cart, but only one item was available. What causes this, and what is the correct fix?**

#### ✅ Correct Answer
**Both requests read `stock = 1` before either writes. Each writes `0`, so both pass the check. The fix is to use one atomic server-side decrement such as `HashIncrementAsync(..., -1)`, then reject or compensate if the result is negative.**

#### 💡 Explanation
- Read-then-write creates a classic race condition.
- Atomic server-side decrement via `HashIncrementAsync` ensures only one request receives a valid stock balance, while concurrent callers receive negative numbers and are rejected.

---

### Question 38
**A Redis `INFO keyspace` report includes this line: `db0:keys=25,expires=11,avg_ttl=285000`. What does `expires=11` mean?**

#### ✅ Correct Answer
**11 keys have an expiration set.**

#### 💡 Explanation
- `keys=25`: Total number of keys in database 0.
- `expires=11`: Number of keys with a configured TTL.
- `avg_ttl=285000`: Average remaining TTL in milliseconds for expiring keys.

---

### Question 39
**A production Redis database has millions of keys. Your team needs to find keys matching `product:*` without blocking Redis. Which statement about `SCAN 0 MATCH product:* COUNT 1000` is correct?**

#### ✅ Correct Answer
**It is one step in a cursor scan. The caller must continue until the cursor returns to 0.**

#### 💡 Explanation
- `SCAN` is an incremental cursor-based iterator.
- `COUNT` is a hint for the amount of work per iteration, not a return limit. The client must iterate until the returned cursor is `0`.

---

### Question 40
**You run `TTL product:45`, and Redis returns `-1`. What does that mean?**

#### ✅ Correct Answer
**The key exists but has no expiration set.**

#### 💡 Explanation
- `TTL` return values:
  - `-1`: Key exists with no expiration.
  - `-2`: Key does not exist.
  - `>= 0`: Seconds until expiration.

---

## Domain 9: Keyspace Inspections, Memory & Namespace Design

### Question 41
**An app verifies a generated list of cache keys by running `EXISTS` and comparing the integer result to the list length. The generated list can contain duplicate key names. What is the main risk with this approach?**

#### ✅ Correct Answer
**A repeated existing key can be counted more than once, so the check can pass even when a distinct required key is missing.**

#### 💡 Explanation
- `EXISTS` with multiple arguments counts matching arguments, not distinct keys.
- If `keyA` is passed twice and exists, `EXISTS keyA keyA` returns `2`.

---

### Question 42
**A large product catalog is stored as a Redis Hash with many fields. A reviewer wants an exact RAM measurement for the full aggregate value, including Redis overhead. Which statement about `MEMORY USAGE product:catalog` is correct?**

#### ✅ Correct Answer
**It reports memory in bytes, but aggregate values may use sampling unless `SAMPLES 0` is specified.**

#### 💡 Explanation
- `MEMORY USAGE` samples elements by default for large composite structures to avoid blocking the main thread.
- Passing `SAMPLES 0` forces Redis to inspect every element for an exact byte count.

---

### Question 43
**Your team is designing the key namespace for the food delivery platform. Which key naming approach provides the best organization for debugging and operational monitoring?**

#### ✅ Correct Answer
**Use a consistent hierarchical namespace with colon separators that starts with the data type / domain entity:**
```text
menu:rest:5
orders:recent:rest:5
trending:dishes
customers:unique:2025-03-25
```

#### 💡 Explanation
- Colon-separated namespaces (`entity:id:attribute`) provide deterministic hierarchy, enabling efficient prefix pattern matching with `SCAN` and clean organization in Redis management tooling.

---

## Domain 10: Lists & Capped Event Feeds

### Question 44
**Your team is implementing the recent orders feed using a Redis List: `LPUSH` on each completed order, `LTRIM` to cap at 50, and `LRANGE 0 49` to retrieve. A teammate argues you should switch to a Sorted Set because it would make the ordering explicit by storing each order's completion timestamp as the score. Which of the following are valid reasons to keep the List?**

#### ✅ Correct Answers
1. **Orders arrive in the correct order naturally, so no scoring mechanism is needed to maintain the feed's sequence.**
2. **`LPUSH` and `LTRIM` together provide a simple and natural pattern for maintaining a capped recent-orders feed.**
3. **The feed does not require ranking, range queries by score, or weighted ordering, so none of the extra capabilities a Sorted Set adds are needed here.**

#### 💡 Explanation
- Lists naturally maintain chronological insertion order when prepending with `LPUSH`.
- The `LPUSH` + `LTRIM` pattern is the standard, high-performance approach for capped event feeds.

---

### Question 45
**You're reviewing the implementation for adding a completed order to a restaurant's recent orders feed. What does the `await db.ListTrimAsync(key, 0, 49)` call accomplish?**
```csharp
public async Task AddCompletedOrderAsync(IDatabase db, int restaurantId, Order orderData)
{
    var key = $"orders:recent:{restaurantId}";
    await db.ListLeftPushAsync(key, JsonSerializer.Serialize(orderData));
    await db.ListTrimAsync(key, 0, 49);
}
```

#### ✅ Correct Answer
**It keeps elements at indices 0 through 49 (the 50 most recent orders) and removes everything beyond that, ensuring the list never grows past 50 elements.**

#### 💡 Explanation
- `LTRIM` keeps the specified inclusive index range (`0` to `49` = 50 elements) and discards all remaining elements.

---

### Question 46
**Your team's dashboard component fetches the recent orders feed for display. A new restaurant was just onboarded and hasn't received any orders yet. What does this method return when called for that restaurant?**
```csharp
public List<Order> GetRecentOrders(IDatabase db, int restaurantId)
{
    var key = $"orders:recent:{restaurantId}";
    var orders = db.ListRange(key, 0, 49);
    return orders.Select(o => JsonSerializer.Deserialize<Order>(o)).ToList();
}
```

#### ✅ Correct Answer
**It returns an empty `List<Order>` because `ListRange` returns an empty `RedisValue[]` when the key doesn't exist, and `Select` over an empty array produces an empty list.**

#### 💡 Explanation
- In Redis, calling `LRANGE` on a non-existent key returns an empty array rather than null or an error.

---

### Question 47
**Three orders complete in quick succession for a restaurant. Your application runs:**
```csharp
db.ListLeftPush("orders:recent:5", JsonSerializer.Serialize(new { id = "A", item = "Pizza" }));
db.ListLeftPush("orders:recent:5", JsonSerializer.Serialize(new { id = "B", item = "Burger" }));
db.ListLeftPush("orders:recent:5", JsonSerializer.Serialize(new { id = "C", item = "Sushi" }));
var feed = db.ListRange("orders:recent:5", 0, 2);
```
**What is the order of elements in `feed`?**

#### ✅ Correct Answer
```json
[C-Sushi, B-Burger, A-Pizza]
```

#### 💡 Explanation
- `LPUSH` prepends elements to the head of the list.
- Order of insertion: A, then B, then C -> List order: `[C, B, A]`.
- `LRANGE 0 2` reads from index 0 upward, returning `C-Sushi`, `B-Burger`, `A-Pizza`.

---

### Question 48
**After deploying the recent orders feed, the ops team notices that restaurant dashboards occasionally show 51 or 52 orders instead of 50. You review the code:**
```csharp
public async Task AddCompletedOrderAsync(IDatabase db, int restaurantId, Order orderData)
{
    var key = $"orders:recent:{restaurantId}";
    var length = await db.ListLeftPushAsync(key, JsonSerializer.Serialize(orderData));
    if (length > 50)
    {
        await db.ListTrimAsync(key, 0, 49);
    }
}
```
**The conditional trim appears correct. What is the most likely cause?**

#### ✅ Correct Answer
**Two concurrent requests can both `ListLeftPushAsync` before either `ListTrimAsync` runs, creating a window where the list temporarily exceeds 50 entries and a dashboard read during that window sees the oversized list.**

#### 💡 Explanation
- The push and trim operations are separate round-trips.
- Under high concurrency, multiple pushes can occur before trims execute, causing temporary size increases visible to concurrent readers.

---

## Domain 11: Sets & Server-Side Set Operations

### Question 49
**Your team is tracking unique customers who ordered from each restaurant on a given day. Each time an order completes, the customer ID is added via `SADD`. The daily unique count is retrieved via `SCARD`. Which of the following are good reasons a Redis Set fits this use case?**

#### ✅ Correct Answers
1. **Because duplicate customer IDs are stored only once, `SCARD` can return the Set's cardinality in $O(1)$ without scanning members.**
2. **Sets natively support union and intersection operations, so comparing unique customers across restaurants or across days can be done directly in Redis without pulling data into the application.**
3. **Adding the same customer ID multiple times does not create duplicates, so uniqueness is enforced without application-side duplicate checks.**

#### 💡 Explanation
- Sets maintain distinct elements automatically with $O(1)$ cardinality lookups (`SCARD`) and server-side set algebra (`SINTER`, `SUNION`, `SDIFF`).

---

### Question 50
**Your team implements the daily unique customer tracker:**
```csharp
public void TrackCustomerOrder(IDatabase db, int customerId)
{
    var today = DateTime.UtcNow.ToString("yyyy-MM-dd");
    var key = $"customers:unique:{today}";
    bool added = db.SetAdd(key, customerId.ToString());
    Console.WriteLine(added);
}
```
**Customer `cust:42` places three orders throughout the day. What does `added` equal on each of the three calls?**

#### ✅ Correct Answer
**`true` the first time a customer orders that day, and `false` on subsequent orders from the same customer, because `SetAdd` returns whether the member was newly added to the Set.**

#### 💡 Explanation
- `SADD` returns `1` if the element was newly added, and `0` if it already existed in the set.
- `StackExchange.Redis` surfaces this as `bool`.

---

### Question 51
**The marketing team wants to identify customers who ordered from two different restaurants on the same day for a cross-promotion campaign. You have `customers:unique:rest:5:2025-03-25` and `customers:unique:rest:7:2025-03-25`. Which Redis command finds these customers most efficiently?**

#### ✅ Correct Answer
```text
SINTER customers:unique:rest:5:2025-03-25 customers:unique:rest:7:2025-03-25
```

#### 💡 Explanation
- `SINTER` computes the intersection directly on the server in a single command, returning only common members without round-trip network overhead.

---

### Question 52
**At midnight, your application needs to clean up customer tracking sets from 7 days ago. You retrieve all customer IDs from the old set before deleting it to generate a weekly summary report:**
```csharp
public async Task<string[]> ArchiveAndCleanupAsync(IDatabase db, string dateKey)
{
    var key = $"customers:unique:{dateKey}";
    var members = await db.SetMembersAsync(key);
    await db.KeyDeleteAsync(key);
    return members.Select(m => m.ToString()).ToArray();
}
```
**What is the issue with this code and what is the best fix?**

#### ✅ Correct Answer
**The code has a race condition. Another process might add a customer between `SetMembersAsync` and `KeyDeleteAsync`. Use `RENAME` to atomically move the key to an archive namespace, then read from there.**

#### 💡 Explanation
- Calling `SMEMBERS` followed by `DEL` leaves a window where items added between commands are lost.
- `RENAME` atomically moves the key away from active writers, allowing safe reading and deletion.

---

### Question 53
**Your analytics team needs an exact weekly unique customer count every Monday. You have daily Sets from `customers:unique:2025-03-24` through `customers:unique:2025-03-30`. You want Redis to compute the weekly union without returning all customer IDs to the application. Which approach is best?**

#### ✅ Correct Answer
**`SUNIONSTORE customers:unique:2025-W13 <7 daily keys>`, then use its integer reply.**

#### 💡 Explanation
- `SUNIONSTORE` computes the union server-side, stores it in a destination key, and returns the cardinality directly as an integer reply, preventing high network data transfer.

---

## Domain 12: Sorted Sets & Real-Time Leaderboards

### Question 54
**Your team is implementing a "trending dishes" feature that shows the most-ordered dishes across all restaurants in the past hour. Each time a dish is ordered, you update a Sorted Set. What should the score represent to make the trending calculation accurate?**

#### ✅ Correct Answer
**The order count. Increment the score by 1 each time the dish is ordered. Higher scores mean more orders.**

#### 💡 Explanation
- Trending leaderboards track frequency.
- The score should represent the cumulative order count, updated via `ZINCRBY`.

---

### Question 55
**Your team initializes the trending dishes Sorted Set, then processes incoming orders:**
```csharp
db.SortedSetAdd("trending:dishes", new SortedSetEntry[] {
    new("Pizza", 5),
    new("Burger", 3),
    new("Sushi", 8)
});

bool result = db.SortedSetAdd("trending:dishes", "Sushi", 12);
```
**What does `result` equal, and what is Sushi's score after the second call?**

#### ✅ Correct Answer
**`result` is `false` and Sushi's score is `12`. `SortedSetAdd` returns `true` when a member is new and `false` when an existing member's score is updated. The score is still updated.**

#### 💡 Explanation
- `ZADD` returns `0` (`false`) when updating an existing member's score, but the score is updated to `12`.

---

### Question 56
**You need to display the top 3 trending dishes with their order counts. The Sorted Set `trending:dishes` currently contains: Pizza (25), Burger (18), Sushi (42), Tacos (31), Salad (12). Which call retrieves the top 3 dishes with their scores, ordered from highest to lowest score?**

#### ✅ Correct Answer
```csharp
SortedSetEntry[] top3 = db.SortedSetRangeByRankWithScores("trending:dishes", 0, 2, Order.Descending);
```

#### 💡 Explanation
- `SortedSetRangeByRankWithScores` with `Order.Descending` fetches members sorted by highest score first (`WITHSCORES`), with 0-indexed range `0, 2` returning the top 3 elements.

---

### Question 57
**Each time a dish is ordered, the trending score needs to increment by 1. You review the code:**
```csharp
public double RecordDishOrder(IDatabase db, string dishName)
{
    double newScore = db.SortedSetIncrement("trending:dishes", dishName, 1);
    return newScore;
}
```
**The dish "Ramen" has never been ordered before — it doesn't exist in the Sorted Set. What happens when this method is called for Ramen?**

#### ✅ Correct Answer
**The call creates Ramen as a new member with a score of 1.0 and returns 1.0. `SortedSetIncrement` treats a non-existent member as having a score of 0 before applying the increment.**

#### 💡 Explanation
- `ZINCRBY` automatically initializes missing members with a score of `0` before adding the increment.

---

### Question 58
**Your team uses `ZRANK` to show each dish's ranking position on the trending page. The Sorted Set contains: Salad (12), Burger (18), Pizza (25), Tacos (31), Sushi (42). You run `ZRANK trending:dishes Pizza`. What does it return, and why?**

#### ✅ Correct Answer
**`2` — `ZRANK` is 0-based and orders from lowest to highest score.**

#### 💡 Explanation
- Ascending scores: Salad (0), Burger (1), Pizza (2), Tacos (3), Sushi (4).
- For descending rank, use `ZREVRANK`.

---

## Domain 13: Advanced JSONPath Filters & Merge Patching

### Question 59
**Your team stores each restaurant's menu as a JSON document:**
```csharp
var json = db.JSON();
json.Set("menu:rest:5", "$", new {
    restaurant = "Sakura Sushi",
    categories = new[] {
        new {
            name = "Appetizers",
            items = new[] {
                new { dish = "Edamame", price = 5.99 },
                new { dish = "Gyoza", price = 7.50 }
            }
        },
        new {
            name = "Entrees",
            items = new[] {
                new { dish = "Salmon Roll", price = 14.99 }
            }
        }
    }
});
```
**You need to retrieve the prices of all items across all categories. Which call accomplishes this?**

#### ✅ Correct Answer
```csharp
var prices = json.Get("menu:rest:5", path: "$.categories[*].items[*].price");
```

#### 💡 Explanation
- The `[*]` wildcard navigates every element in the `categories` and `items` arrays, collecting all matching prices.

---

### Question 60
**A restaurant stores its menu as this JSON document:**
```csharp
var json = db.JSON();
json.Set("menu:rest:5", "$", new {
    restaurant = "Sakura Sushi",
    categories = new[] {
        new {
            name = "Appetizers",
            items = new[] {
                new { dish = "Edamame", price = 5.99, available = true },
                new { dish = "Gyoza", price = 7.50, available = false }
            }
        },
        new {
            name = "Entrees",
            items = new[] {
                new { dish = "Salmon Roll", price = 14.99, available = true }
            }
        }
    }
});
```
**The restaurant updates Edamame from $5.99 to $6.99. Category and item order may change over time, but dish names are unique within the menu. Which approach updates only Edamame's price without replacing the entire document?**

#### ✅ Correct Answer
```csharp
json.Set("menu:rest:5", "$.categories[*].items[?(@.dish==\"Edamame\")].price", 6.99);
```

#### 💡 Explanation
- The JSONPath filter `[?(@.dish=="Edamame")]` targets the specific object regardless of its array index.

---

### Question 61
**A restaurant needs to update its menu document in one call: change the phone number, add a new website field, and remove the fax field. Which `JSON.MERGE` call achieves all three changes?**

#### ✅ Correct Answer
```csharp
json.Merge("menu:rest:5", "$", "{\"phone\":\"555-0200\",\"website\":\"sakurasushi.com\",\"fax\":null}");
```

#### 💡 Explanation
- `JSON.MERGE` follows RFC 7386 JSON Merge Patch semantics:
  - Updates/adds non-null fields (`phone`, `website`).
  - Removes fields set to `null` (`"fax": null`).

---

## Domain 14: Production Operations, UNLINK & Bulk Processing

### Question 62
**After a production server crash, the team discovers that the last 3 minutes of orders were lost. Restaurant dashboards showed orders that are no longer in Redis. The current persistence configuration uses RDB snapshots every 5 minutes. What change would minimize data loss for this real-time orders use case?**

#### ✅ Correct Answer
**Switch to AOF with `appendfsync everysec`. This writes operations to the append-only log every second, limiting data loss to approximately one second rather than up to 5 minutes.**

#### 💡 Explanation
- AOF with `appendfsync everysec` bounds potential data loss to at most 1 second of write operations while maintaining high throughput.

---

### Question 63
**Your operations team needs to audit all restaurant menu keys to verify a migration completed successfully. The production Redis instance has 50 million keys across all data types. Which approach safely retrieves all `menu:rest:*` keys without impacting production traffic?**

#### ✅ Correct Answer
```text
SCAN 0 MATCH menu:rest:* COUNT 1000  (in an iterative loop)
```

#### 💡 Explanation
- `SCAN` is non-blocking and iterates incrementally.
- Running `KEYS` on 50 million keys would block the single-threaded server for seconds or minutes.

---

### Question 64
**At the end of each day, your cleanup job needs to delete the trending dishes Sorted Set, which contains approximately 100,000 members. You want to minimize impact on concurrent operations. Which approach is best?**

#### ✅ Correct Answer
```text
UNLINK trending:dishes:2025-03-25
```

#### 💡 Explanation
- `UNLINK` immediately removes the key from the keyspace in $O(1)$ and reclaims memory asynchronously on a background thread.
- `DEL` blocks the main thread while deallocating 100,000 members.

---

### Question 65
**Your cleanup routine receives 500 exact Redis key names to remove from a standalone Redis database. The deletes do not need transaction semantics. Which `StackExchange.Redis` implementation is the most appropriate async approach?**
```csharp
public async Task<long> CleanupOldKeysAsync(IDatabase db, string[] keysToDelete)
{
    // Implementation here
}
```

#### ✅ Correct Answer
```csharp
var redisKeys = keysToDelete.Select(k => (RedisKey)k).ToArray();
return await db.KeyDeleteAsync(redisKeys);
```

#### 💡 Explanation
- Passing an array of `RedisKey` to `KeyDeleteAsync` generates a single variadic `DEL key1 key2 ...` command in one network round trip.
- Calling `KeyDeleteAsync` individually inside a loop generates 500 separate round trips.
