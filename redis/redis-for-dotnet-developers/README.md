# Redis for .NET Developers — Practice Question Bank

[![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)](https://redis.io/)
[![.NET](https://img.shields.io/badge/.NET-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)](https://dotnet.microsoft.com/)
[![StackExchange.Redis](https://img.shields.io/badge/StackExchange.Redis-v2.x-blue?style=for-the-badge)](https://stackexchange.github.io/StackExchange.Redis/)
[![Questions](https://img.shields.io/badge/Questions-65%20MCQs-success?style=for-the-badge)](#table-of-contents)
[![Cheat Sheet](https://img.shields.io/badge/Study_Guide-Cheat_Sheet-orange?style=for-the-badge)](CHEAT_SHEET.md)

Comprehensive Multiple Choice Practice Question Bank for the **Redis for .NET Developers** certification. Curated and verified with accurate answer keys and clear technical explanations for each question.

> [!TIP]
> Preparing for the exam? Review the [Redis for .NET Developers Last-Minute Cram Sheet](CHEAT_SHEET.md) for native data structures, `StackExchange.Redis` C# patterns, RedisJSON/RediSearch, eviction policies, and high-frequency exam traps.

---

## Table of Contents

- [Questions 1 – 10: Redis Architecture, RESP & Connections](#questions-1--10-redis-architecture-resp--connections)
- [Questions 11 – 20: Hashes, RedisJSON & Data Modeling](#questions-11--20-hashes-redisjson--data-modeling)
- [Questions 21 – 30: Cache-Aside Patterns, Eviction & Query Caching](#questions-21--30-cache-aside-patterns-eviction--query-caching)
- [Questions 31 – 40: TTL, Persistence, Transactions & Concurrency](#questions-31--40-ttl-persistence-transactions--concurrency)
- [Questions 41 – 50: Keyspace Management, Lists & Sets](#questions-41--50-keyspace-management-lists--sets)
- [Questions 51 – 60: Set Operations, Sorted Sets & JSONPath Filters](#questions-51--60-set-operations-sorted-sets--jsonpath-filters)
- [Questions 61 – 65: JSON Merge Patching & Production Operations](#questions-61--65-json-merge-patching--production-operations)

---

## Questions 1 – 10: Redis Architecture, RESP & Connections

### Question 1
Which of the following are accurate statements about Redis?

*Choose 2 answers*

- **A.** Redis supports configurable persistence mechanisms that allow data to survive process restarts when enabled.
- **B.** When Redis reaches its configured memory limit, it rejects all incoming commands — including reads — until memory is freed by expiring keys or by an administrator manually deleting data.
- **C.** Redis stores data primarily in main memory (RAM), which is why it achieves lower latency than disk-based databases for read and write operations.
- **D.** Redis uses multiple threads to execute commands in parallel, which is how a single instance can handle hundreds of thousands of operations per second.
- **E.** Redis data structures like Hashes and Sorted Sets are client-side abstractions — the client library converts them into plain Strings before sending them to the server, which stores everything in a single flat key-value format.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** A, C

> **Why:** With `noeviction`, Redis rejects *writes* at the memory limit but keeps serving reads, so B is wrong. Command execution is single-threaded (D is wrong), and Hashes and Sorted Sets are real server-side types, not client shims (E is wrong). Persistence being configurable and opt-in, and RAM residency being the latency story, are the two accurate statements.

</details>

---

### Question 2
You're inspecting the raw traffic between the client and server on an application using Redis. Which of the following are true about RESP (Redis Serialization Protocol)?

*Choose 2 answers*

- **A.** Each Redis client library uses its own proprietary wire format to communicate with the server, and RESP is only used internally within the server to serialize data to disk.
- **B.** RESP traffic cannot be inspected with standard networking tools. Because the protocol uses a compact encoding, you need a specialized Redis protocol analyzer to read or send raw commands to the server.
- **C.** RESP encrypts all traffic between the client and server by default, so no additional TLS configuration is needed to secure Redis connections in production.
- **D.** Clients send commands to the Redis server as RESP arrays of bulk strings. For example, `SET mykey myvalue` is transmitted as an array of three bulk strings: `SET`, `mykey`, and `myvalue`.
- **E.** RESP responses are type-prefixed — the first byte of each response indicates its wire type, such as `+` for simple strings, `-` for errors, and `:` for integers. This allows parsers to determine how to read each response from the byte stream.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** D, E

> **Why:** RESP is the standard wire protocol shared by all Redis clients (A is wrong) and is human-readable plain text that can be inspected with ordinary tools like `tcpdump` (B is wrong). Commands go out as arrays of bulk strings, and every reply carries a one-byte type prefix (`+` simple string, `-` error, `:` integer, `$` bulk string, `*` array). It is unencrypted by default — TLS is configured separately (C is wrong).

</details>

---

### Question 3
Which statement most accurately describes Redis transactions?

- **A.** Redis transactions block all other clients as soon as `MULTI` is issued, and no other commands on the server can run until `EXEC` or `DISCARD`.
- **B.** Redis transactions queue commands until `EXEC`, then execute them sequentially without interleaving from other clients, but Redis does not support rollback.
- **C.** Redis transactions provide SQL-style rollback, so if any command fails during execution, all earlier commands in the transaction are automatically undone.
- **D.** Redis transactions execute each command immediately when it is issued after `MULTI`, and `EXEC` only asks Redis to return the buffered results.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `MULTI` queues commands and `EXEC` runs them sequentially as one isolated unit without other clients interleaving. Redis does not block other clients while commands are merely queued after `MULTI` (A is wrong), does not support SQL-style rollback if a command fails at execution time (C is wrong), and does not execute queued commands until `EXEC` is called (D is wrong).

</details>

---

### Question 4
Which of the following is NOT an example of an atomic operation in Redis?

- **A.** Appending to a list
- **B.** Deleting a key using `UNLINK`
- **C.** Executing a series of commands in a pipeline
- **D.** Incrementing a numeric counter

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** Every individual Redis command — such as appending to a list (`RPUSH`, A), asynchronously unlinking a key (`UNLINK`, B), or incrementing a counter (`INCR`, D) — executes atomically on the single-threaded command loop. A pipeline (C) only batches network round trips; other clients' commands can still interleave between the pipelined commands, so the batch as a whole is not atomic.

</details>

---

### Question 5
Which of the following are valid Redis key names under Redis's default key-size limit?

*Choose 4 answers*

- **A.** The raw bytes of a PDF file, approximately 120 KB in size
- **B.** `""` (an empty string)
- **C.** A key made of the letter `"a"` repeated until the key is 512 MB long
- **D.** The "winking face" emoji
- **E.** The raw bytes of a compressed dump of Wikipedia, approximately 1 GB in size

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** A, B, C, D

> **Why:** Keys are binary-safe byte strings capped at 512 MB, so raw PDF bytes, an empty string, and an emoji are all legal key names; 1 GB exceeds the 512 MB cap (E is wrong). Option C sits exactly on the 512 MB boundary — the exam counts it as valid.

</details>

---

### Question 6
Your operations team monitors the Redis server and notices that your .NET application is maintaining 2 physical TCP connections, even though you only created a single `ConnectionMultiplexer` instance. What is the explanation for this?

- **A.** The `ConnectionMultiplexer` creates one connection for interactive commands and a separate dedicated connection for pub/sub subscriptions.
- **B.** The second connection is a standby replica that remains idle until the primary connection fails. The `ConnectionMultiplexer` maintains it for automatic failover and will promote it if the first connection drops.
- **C.** `GetDatabase()` opens a new TCP connection each time it is called. The two connections likely correspond to two `GetDatabase()` calls somewhere in the application.
- **D.** The `ConnectionMultiplexer` opens one connection for reading and a separate connection for writing to avoid contention between inbound and outbound traffic on a single socket.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** `StackExchange.Redis` opens a second physical connection for pub/sub, because a subscriber connection cannot interleave ordinary commands. It is not a standby failover socket (B is wrong), `GetDatabase()` returns a lightweight handle over the existing multiplexer rather than opening new TCP sockets (C is wrong), and reads and writes share the same interactive connection rather than splitting across sockets (D is wrong).

</details>

---

### Question 7
Under load, 50 concurrent requests each issue Redis commands at the same time through a shared `ConnectionMultiplexer`. You're concerned about commands "stepping on each other" over the shared connection. How does the `ConnectionMultiplexer` handle this?

- **A.** It assigns each calling thread a temporary dedicated connection from an internal pool, ensuring complete isolation between concurrent requests. Connections are returned to the pool after each command completes.
- **B.** It opens a new TCP connection for each concurrent command to guarantee isolation, then closes the connection once the response is received. Under 50 concurrent requests, 50 separate connections are active simultaneously.
- **C.** It queues all commands into a single FIFO buffer and processes them one at a time, waiting for each response before sending the next command. This guarantees correctness but limits throughput to one in-flight command at a time regardless of how many threads are active.
- **D.** It sends commands from all threads over a shared connection without waiting for each response before sending the next. The library tracks which response belongs to which caller and dispatches results back to the correct thread as they arrive.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** This is what multiplexing means: commands from many threads share one socket, are pipelined without waiting for prior replies, and the library correlates each incoming FIFO reply back to the awaiting `Task`. It does not check out pooled connections per thread (A is wrong), does not open a new TCP connection per command (B is wrong), and does not block on each response before writing the next command (C is wrong).

</details>

---

### Question 8
*Scenario:* Connection handling when the Redis server might be temporarily unavailable at startup.

- **A.** Add the following to the connection string:
  ```text
  "redis-server:6379,connectTimeout=0"
  ```
  Setting the timeout to zero tells the `ConnectionMultiplexer` to wait indefinitely for the Redis server to become available rather than timing out.
- **B.** Add the following to the connection string:
  ```text
  "redis-server:6379,abortConnect=false"
  ```
  This tells the `ConnectionMultiplexer` not to throw an exception if the initial connection attempt fails. Instead, it continues retrying in the background until the Redis server becomes available.
- **C.** Replace the connection call with:
  ```csharp
  var redis = await ConnectionMultiplexer.ConnectAsync("redis-server:6379");
  ```
  The asynchronous version automatically retries failed connections indefinitely, while the synchronous Connect method fails immediately if the server is unreachable.
- **D.** Wrap the connection attempt in retry logic such as:
  ```csharp
  try
  {
      var redis = ConnectionMultiplexer.Connect("redis-server:6379");
  }
  catch
  {
      Thread.Sleep(5000);
  }
  ```
  The `ConnectionMultiplexer` has no built-in mechanism for handling an unavailable server at startup, so retry logic must be implemented manually.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** In `StackExchange.Redis`, setting `abortConnect=false` in the connection string instructs the `ConnectionMultiplexer` not to throw an exception at startup if the Redis server is temporarily unreachable, and to automatically continue retrying connections in the background until available. Setting `connectTimeout=0` does not wait indefinitely (A is wrong), `ConnectAsync` still throws when `abortConnect` defaults to `true` (C is wrong), and manual `try/catch` with `Thread.Sleep` is an anti-pattern when built-in background connection retry exists (D is wrong).

</details>

---

### Question 9
Your .NET application uses a shared `ConnectionMultiplexer` singleton. During a planned Redis server restart, the server goes offline for approximately 10 seconds. What happens to Redis commands issued by your application during this window?

- **A.** Commands continue to succeed during the outage because the `ConnectionMultiplexer` serves all read commands from a local in-memory replica that it maintains automatically. Only write commands fail during the disconnection window.
- **B.** Commands issued during the outage are silently discarded — no exceptions are thrown and no results are returned. The application must poll `ConnectionMultiplexer.IsConnected` after each command to detect whether the result is valid.
- **C.** The `ConnectionMultiplexer` permanently enters a faulted state after the connection drops. The application must catch the disconnection event and create a new `ConnectionMultiplexer` instance to restore Redis functionality.
- **D.** The `ConnectionMultiplexer` reconnects automatically in the background. Commands issued while Redis is unavailable may fail with timeout or connection exceptions; the application should handle those failures and retry only when safe.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** The multiplexer reconnects on its own, so no new instance is needed — but commands issued during the outage fail with connection or timeout exceptions rather than queuing silently. Treat them as ordinary transient faults and retry only where a retry is safe. The multiplexer does not maintain a local in-memory replica (A is wrong), does not silently discard commands without throwing (B is wrong), and does not permanently fault on disconnect (C is wrong).

</details>

---

### Question 10
After a deployment, you need to run the `INFO` command from your .NET application to check memory usage on the Redis server. How do you access server-level commands?

- **A.** Server commands like `INFO` are accessed through `IServer`, obtained via `redis.GetServer("host", port)`. This interface exposes methods like `Info()`, `FlushDatabase()`, and `Keys()` that are intentionally absent from `IDatabase`.
- **B.** Server commands are available on `IDatabase` but require the `AllowAdmin` flag to be set in the connection string before they appear.
- **C.** Server commands are accessed by casting `IDatabase` to `IServer` — they implement the same underlying interface, but the server methods are explicitly hidden and only accessible through the cast.
- **D.** Server commands like `INFO` are not supported in `StackExchange.Redis`. You must use `db.Execute("INFO")` to send raw command strings, and parse the response manually.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Server-wide commands (`INFO`, `CONFIG`, `CLIENT LIST`, `SLOWLOG`) live on `IServer`, obtained from `GetServer`; `IDatabase` deliberately exposes only keyspace commands. Note: some `IServer` methods such as `FlushDatabase` and `Keys` additionally require `allowAdmin=true` in the connection string, though `INFO` does not. Setting `allowAdmin=true` does not add server methods to `IDatabase` (B is wrong), `IDatabase` cannot be cast to `IServer` (C is wrong), and `IServer.Info()` is natively supported without raw `db.Execute("INFO")` calls (D is wrong).

</details>

---

## Questions 11 – 20: Hashes, RedisJSON & Data Modeling

### Question 11
Your team is deciding how to cache product records. One developer proposes storing each product as a serialized JSON string like `'{"name":"Widget","price":9.99,"stock":150}'`. Another proposes using a Hash. The application frequently updates stock counts without touching other fields. What is the strongest argument for choosing a Hash over a serialized String in this case?

- **A.** Hashes use less memory than Strings for all data sizes.
- **B.** A Hash automatically coerces numeric values, so stock can be incremented without type conversion.
- **C.** Hashes enforce type constraints on field values, so storing stock as a number prevents accidental non-numeric assignments, unlike a serialized String, which stores the entire record as untyped text.
- **D.** A Hash allows updating the stock field directly without deserializing and rewriting the entire record.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** A Hash lets you `HSET` or `HINCRBY` one field in place; a serialized String forces a read, deserialize, modify, serialize, write cycle for any change. Hashes are not universally smaller than Strings for all data sizes (A is wrong), store field values as byte strings that are parsed as numbers only when commands like `HINCRBY` run (B is wrong), and do not enforce schema or type constraints (C is wrong).

</details>

---

### Question 12
You cache a product for the first time, then immediately update its stock:

```csharp
db.HashSet("product:42", new HashEntry[] {
    new("name", "Widget"),
    new("price", "9.99"),
    new("category", "gadgets"),
    new("stock", "150")
});

bool result = db.HashSet("product:42", "stock", "125");
```

- **A.** `false` — `HashSet` returns false because no `When` parameter was specified. Without `When.Always`, `StackExchange.Redis` defaults to a conditional write that skips existing fields and signals the no-op with false.
- **B.** `true` — `HashSet` always returns true when the operation completes without error, regardless of whether the field was new or already existed.
- **C.** `true` — `HashSet` returns true because the stock value was successfully changed from "150" to "125".
- **D.** `false` — when setting a single field, `HashSet` returns true if the field is new and false if the field already existed and was updated. Since stock already existed, the return is false.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** Single-field `HSET` returns `1` only when the field is newly created. Updating an existing field returns `0`, which `StackExchange.Redis` surfaces as `false`. The write happens either way — the return value reports novelty, not success. `StackExchange.Redis` defaults to `When.Always` so the update is not skipped (A is wrong), and `HashSet` does not return `true` when overwriting an existing field (B and C are wrong).

</details>

---

### Question 13
After a flash sale ends, a cleanup routine removes the discount field from all product Hashes using `HDEL`. For one product, discount was the only field in the Hash. A developer on your team assumes the key still exists afterward and schedules a separate `UNLINK` job to remove it later. What actually happens?

- **A.** Redis keeps the key as a zero-length Hash until the next background cleanup cycle removes it, so the scheduled `UNLINK` job is still needed to reclaim the key immediately.
- **B.** Redis automatically deletes the key when its last field is removed. There is no such thing as an empty Hash in Redis. The scheduled `UNLINK` job is unnecessary.
- **C.** `HDEL` on the last remaining field returns an error, signaling that `DEL` must be used instead to remove the final field.
- **D.** The key persists as an empty Hash until explicitly deleted with `DEL`. `HDEL` only removes fields, not the key itself.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Redis has no empty collections. Removing the last field with `HDEL` immediately deletes the key itself, so the scheduled `UNLINK` has nothing to clean up. Redis never keeps zero-length Hashes around (A and D are wrong), and `HDEL` removes the final field cleanly without returning an error (C is wrong).

</details>

---

### Question 14
You're building a product page that displays only the item's name and price. The product is cached as a Hash with six fields: name, price, category, stock, weight, and supplier. Which call fetches exactly the fields you need in a single round trip, without retrieving unnecessary data?

- **A.** `db.HashScan("product:42", "name|price");`
- **B.** `db.HashGet("product:42", new RedisValue[] { "name", "price" });`
- **C.** `db.HashGetAll("product:42");`
- **D.** `db.StringGet(new RedisKey[] { "product:42:name", "product:42:price" });`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `HashGet` with an array of fields maps to `HMGET`: one round trip, only the requested fields. `HSCAN` iterates fields with a glob pattern rather than selecting exact fields in one call (A is wrong), `HGETALL` pulls all six fields unnecessarily (C is wrong), and `StringGet` queries standalone String keys rather than fields inside the `product:42` Hash (D is wrong).

</details>

---

### Question 15
A supplier import job refreshes name, price, and stock on every run, but the `firstSeenAt` field in each product Hash should be written only the first time the product appears. Multiple workers may process the same product at the same time. Which approach is best?

- **A.** Use `HSETNX product:42 firstSeenAt <timestamp>` for that field, and use `HSET` for mutable fields like name, price, and stock.
- **B.** Run `HEXISTS product:42 firstSeenAt`, then call `HSET product:42 firstSeenAt <timestamp>` if the field is missing, because Redis serializes commands.
- **C.** Use `HSET product:42 firstSeenAt <timestamp>`, because `HSET` refuses to overwrite existing fields.
- **D.** Store `firstSeenAt` in a separate key with `SETNX`, because Hash fields cannot be conditionally set.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** `HSETNX` sets a hash field only if it does not already exist, atomically on the server. The `HEXISTS`-then-`HSET` sequence in B has a race window between the two commands where concurrent workers can overwrite each other, standard `HSET` always overwrites existing fields (C is wrong), and `HSETNX` provides native conditional field writes on Hashes so a separate String key is unnecessary (D is wrong).

</details>

---

### Question 16
Your team has been caching flat product records as Hashes. A new requirement arrives: each product now includes a nested dimensions object with width, height, and weight fields, as well as an array of tags. A team member suggests migrating from Hashes to JSON. What is the strongest reason to consider this change for this data model?

- **A.** JSON compresses documents internally, so nested structures use significantly less memory than equivalent Hash representations.
- **B.** JSON supports TTL on individual paths within a document, allowing dimensions to expire separately from the rest of the product.
- **C.** JSON allows you to read and update nested paths like `$.dimensions.weight` directly, whereas a Hash would require you to flatten the structure or serialize the nested data into a single field.
- **D.** JSON automatically indexes all paths for searching, eliminating the need for key naming conventions.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** Once the data nests, a Hash forces you either to flatten paths into field names or to bury a JSON blob inside one field. RedisJSON reads and writes nested paths in place. RedisJSON stores documents as a parsed binary tree rather than compressing them below Hash memory usage (A is wrong), TTLs apply only to the top-level Redis key rather than individual JSON paths (B is wrong), and secondary indexing requires explicitly defining an index with RediSearch (`FT.CREATE`) rather than happening automatically (D is wrong).

</details>

---

### Question 17
You store a product as a Redis JSON document with nested fields and an array of tags. Which statement best explains why the application must handle RedisJSON path results carefully?

- **A.** RedisJSON automatically flattens nested objects, so paths like `$.dimensions.weight` are rewritten as `dimensions.weight`.
- **B.** `JSON.GET` always returns plain strings, so the application must parse every number manually.
- **C.** Paths using `$` can return arrays of matches, even when the path currently matches one value.
- **D.** `JSON.GET` can only read top-level fields unless the document was indexed first.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** A JSONPath beginning with `$` is a multi-match expression, so RedisJSON wraps results in an array even when exactly one node matches. Code that assumes a scalar will break the first time it does. RedisJSON preserves nested document hierarchy rather than flattening paths (A is wrong), preserves JSON data types in responses rather than converting numbers to strings (B is wrong), and reads any nested path via `JSON.GET` without requiring an index (D is wrong).

</details>

---

### Question 18
A supplier notifies you that the weight for product 42 has changed. The product document includes a nested dimensions object with width, height, and weight fields. You need to update only weight without replacing the rest of the document. Which call accomplishes this?

- **A.** `json.Set("product:42", "$.dimensions.weight", 0.6)`
- **B.** `json.Set("product:42", "$", new { dimensions = new { weight = 0.6 } })`
- **C.** `json.Set("product:42", "$.weight", 0.6)`
- **D.** `json.Set("product:42", "$.dimensions", 0.6)`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** `JSON.SET` with a specific path writes just that node. Passing `"$"` (B) replaces the entire root document, `$.weight` (C) targets a top-level `weight` field instead of the nested one, and `$.dimensions` (D) overwrites the entire `dimensions` object with a scalar number.

</details>

---

### Question 19
Your team is running a seasonal promotion where certain product tags need to be removed when the sale ends. You review the following cleanup code. The product had tags: `["gadget", "sale"]`. After this runs, you retrieve the full product. What happened to the document?

```csharp
var json = db.JSON();
var removed = json.Del("product:42", "$.tags");
Console.WriteLine(removed);
var product = json.Get("product:42", path: "$");
```

- **A.** The contents of tags were emptied to `[]`, but the field itself remains on the document.
- **B.** The command failed silently because `JSON.DEL` cannot remove root-level fields, only nested paths.
- **C.** The tags field was removed from the document entirely — the product still exists but no longer has a tags property.
- **D.** The entire `product:42` key was deleted because removing tags left an incomplete document.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** `JSON.DEL` on `$.tags` removes the property itself, not just its contents — the document remains, minus that field. It does not leave an empty array `[]` behind (A is wrong), works on any path including root-level fields (B is wrong), and only deletes the entire key if the root path `"$"` is deleted (D is wrong).

</details>

---

### Question 20
After running both Hashes and JSON documents in production for several weeks, your team is establishing guidelines for when to use each. Which of the following is a valid guideline?

- **A.** Use Hashes only when the record has fewer than 10 fields, since Hashes become less memory-efficient than JSON beyond that threshold.
- **B.** Use JSON for data that requires TTL and Hashes for data that should persist indefinitely, since Hashes do not support key expiration.
- **C.** Use JSON for read-heavy workloads and Hashes for write-heavy workloads, since Hashes are always faster for write operations.
- **D.** Use JSON when the data has nested structures or arrays that need to be queried or updated by path; use Hashes when the data is a flat set of field-value pairs with no nesting.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** The deciding factor is data shape and access pattern: nested structures or arrays addressed by path favour JSON; flat field-value records favour Hashes. Hashes remain memory-efficient well beyond 10 fields (A is wrong), both Hashes and JSON keys support standard Redis key expiration (B is wrong), and choosing between them is driven by document structure rather than a blanket read-vs-write split (C is wrong).

</details>

---

## Questions 21 – 30: Cache-Aside Patterns, Eviction & Query Caching

### Question 21
Your team is implementing cache-aside for product lookups. A request comes in for a product that is not currently in Redis. Which sequence of steps correctly describes the cache-aside pattern for handling this cache miss?

- **A.** The application queries the database, returns the result to the caller, and Redis asynchronously fetches and caches the record in the background.
- **B.** Redis automatically queries the database when a key is missing, caches the result, and returns it to the application.
- **C.** The application writes the product to Redis, then reads it back from Redis, then returns it to the caller.
- **D.** The application reads from Redis and gets a miss, queries the database, writes the result to Redis, and returns it to the caller.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** Cache-aside puts the application in control: read cache, on a miss read the database, write the result back to the cache, return it. Redis never talks to your database on its own (A and B are wrong), and on a miss the application must query the database first and does not need a redundant read-back from Redis after caching (C is wrong).

</details>

---

### Question 22
When a product's price is updated in the database, the cached copy in Redis becomes stale. You're reviewing two approaches your team proposed:

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

Which approach is more consistent with the cache-aside pattern, and why?

- **A.** Approach A, because deleting the key in Approach B creates a window where the product is completely unavailable to users until another request triggers the cache-aside read path and repopulates it.
- **B.** Approach B, because cache-aside treats the database as the source of truth. Deleting the key forces the next read to repopulate from the database, avoiding write-path inconsistency.
- **C.** Approach A, because updating the cache directly avoids a subsequent cache miss and keeps the cache warm at all times. This reduces latency for the next read and ensures users always see the latest price immediately.
- **D.** Neither. Cache-aside requires the database to notify Redis directly when data changes through an event-driven push, so the application should not be involved in invalidation at all.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Invalidate rather than update. Writing the cache on the write path creates ordering races between concurrent database writes and cache writes (C is wrong); deleting the key lets the next read repopulate from the source of truth. Deleting the key does not make the product unavailable — it merely causes one cache miss on the next read (A is wrong), and in cache-aside the application itself manages cache invalidation rather than relying on database push notifications (D is wrong).

</details>

---

### Question 23
Your team is configuring Redis with `maxmemory` for a cache-aside layer. Some cached keys have TTLs and some do not. Which statement correctly describes how `allkeys-lru`, `volatile-lru`, and `noeviction` differ when Redis runs out of memory?

- **A.** `allkeys-lru` can evict any key based on recent use, `volatile-lru` can evict only keys that have an expiration set, and `noeviction` rejects writes that would exceed the memory limit.
- **B.** `allkeys-lru` evicts the least recently used keys only among keys that have an expiration set, `volatile-lru` also evicts only among keys that have an expiration set, and `noeviction` rejects both reads and writes once memory is exhausted.
- **C.** `allkeys-lru` evicts the largest keys first, `volatile-lru` evicts the least recently used expiring keys, and `noeviction` disables expiration so keys stay until deleted.
- **D.** `allkeys-lru` and `volatile-lru` both evict from the full keyspace, but `volatile-lru` gives priority to keys with shorter TTLs. `noeviction` keeps accepting writes by spilling older values to disk.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** The `volatile-*` policies consider only keys carrying a TTL, the `allkeys-*` policies consider the whole keyspace, and `noeviction` turns memory pressure into write errors while reads continue to work. B is wrong because `allkeys-lru` evicts across all keys and `noeviction` still allows reads; C is wrong because `allkeys-lru` tracks recency of use rather than key size and `noeviction` does not disable TTL expiration; D is wrong because `volatile-lru` ignores persistent keys and `noeviction` rejects writes instead of spilling to disk.

</details>

---

### Question 24
Your Redis instance is configured with `maxmemory` and the `allkeys-lru` eviction policy. During a traffic spike, Redis starts evicting cached product keys to stay within the memory limit. How does this affect your cache-aside implementation?

- **A.** The application will begin throwing errors because it attempts to read keys that were evicted mid-request.
- **B.** Evicted keys are moved to a secondary storage tier by Redis and are still accessible, but with higher latency.
- **C.** The application continues to function correctly — evicted keys appear as cache misses, and the cache-aside logic repopulates them from the database on the next read.
- **D.** The application must be updated to listen for eviction events and preemptively repopulate the cache, otherwise users will see empty product records.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** Cache-aside is eviction-tolerant by design: an evicted key is indistinguishable from a key that was never cached, and the miss path rebuilds it. Evicted keys return a normal cache miss rather than throwing errors (A is wrong), Redis deletes evicted keys from memory rather than moving them to a secondary storage tier (B is wrong), and the read path lazily repopulates misses without needing eviction event listeners (D is wrong).

</details>

---

### Question 25
You're load testing your cache-aside implementation and notice that immediately after a product update, some requests return stale data. Here's the relevant code:

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

What is causing the stale data?

- **A.** `HashSetAsync` silently fails when called immediately after `KeyDeleteAsync` on the same key, leaving the cache permanently empty.
- **B.** The cache is deleted *before* the database is updated. A concurrent `GetProductAsync` call between `KeyDeleteAsync` and the database write can read the old price from the database and re-cache it.
- **C.** `HashGetAllAsync` caches results internally in the `ConnectionMultiplexer`, so even after the key is deleted from Redis, the client returns the previously retrieved `HashEntry[]` array.
- **D.** `KeyDeleteAsync` and `UpdateProductPriceAsync` run on different threads due to the `ConnectionMultiplexer`'s multiplexed I/O. The database update may complete before the Redis delete because the multiplexer reorders commands for throughput optimization.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Order matters. Deleting before the database write leaves a window in which a concurrent read repopulates the cache from the not-yet-updated database, and that stale value then survives until its TTL. Update the database first, then invalidate. `HashSetAsync` works normally after `KeyDeleteAsync` (A is wrong), `ConnectionMultiplexer` does not cache query responses client-side (C is wrong), and `await` sequentially orders `KeyDeleteAsync` before `UpdateProductPriceAsync` (D is wrong).

</details>

---

### Question 26
Your team has been caching individual product records as Hashes. Now the product listing page, which returns filtered results like "all gadgets under $20 sorted by price," is generating a heavy database load. You need to cache these full result sets. Why is a String more appropriate than a Hash for caching a query result?

- **A.** A String is more appropriate because Hashes are intended for single-record caching, while Strings are the standard choice for caching any response that contains multiple records.
- **B.** A String is more appropriate because a query result is a pre-computed response with no need to read or update individual fields, so serializing it into a single value is simpler than mapping it to Hash fields.
- **C.** A Hash is actually the better choice here because each product in the result set maps naturally to a Hash field, and `HGETALL` retrieves them all at once as one complete response.
- **D.** A Hash is required whenever a cached value contains multiple products, because Redis Strings can only store a single scalar value and cannot hold serialized arrays or nested objects.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** A query result is an opaque blob you read whole and replace whole. Hash fields only pay off when you address individual fields, which never happens here. The choice is driven by access pattern rather than a rigid single-vs-multiple record rule (A is wrong), mapping a sorted list of products into unordered Hash fields loses ordering and adds unnecessary complexity (C is wrong), and Redis Strings can store any serialized JSON array or binary payload up to 512 MB (D is wrong).

</details>

---

### Question 27
Your team caches many listing-page query results with a 5-minute TTL (`EX: 300`). Product managers report that price changes can leave some listing pages stale for up to 5 minutes. A teammate proposes lowering the TTL to 15 seconds. What is the main tradeoff across the query cache?

- **A.** The application will need to handle more cache invalidation events, because shorter TTLs trigger more expiration notifications that the client must process and respond to.
- **B.** A 15-second TTL will cause Redis to consume more CPU on expiration processing, which will degrade the latency of all other Redis commands running on the same instance.
- **C.** The cache hit rate will drop. More query results will expire before reuse, causing more reads to fall through to the database.
- **D.** Shorter TTLs will cause cache stampedes for most query keys, because every expired entry forces multiple requests to hit the database at the same time.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** A shorter TTL trades freshness for hit rate: more cached results expire before they are reused, so more requests fall through to the database. Clients do not need to listen to expiration events for standard cache-aside (A is wrong), Redis handles TTL expiration with negligible CPU overhead (B is wrong), and stampedes only occur on high-concurrency hot keys rather than most query keys (D is wrong).

</details>

---

### Question 28
You're implementing async query caching for the product listing page. Your team has agreed on the key schema `query:{category}:{sort}:{page}`. You need to write a method that checks the cache first, falls through to the database on a miss, caches the result, and returns it. Which implementation is correct?

- **A.**
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
- **B.**
  ```csharp
  public async Task<List<Product>> GetProductsAsync(IDatabase db, string category, string sort, int page)
  {
      var key = $"query:{category}:{sort}:{page}";
      var results = await _repository.GetProductsAsync(category, sort, page);
      await db.StringSetAsync(key, JsonSerializer.Serialize(results), TimeSpan.FromSeconds(300));
      return results;
  }
  ```
- **C.**
  ```csharp
  public async Task<List<Product>> GetProductsAsync(IDatabase db, string category, string sort, int page)
  {
      var key = $"query:{category}:{sort}:{page}";
      var cached = await db.StringGetAsync(key);
      if (!cached.IsNull) return JsonSerializer.Deserialize<List<Product>>(cached);
      var results = await _repository.GetProductsAsync(category, sort, page);
      await db.StringSetAsync(key, results, TimeSpan.FromSeconds(300));
      return results;
  }
  ```
- **D.**
  ```csharp
  public async Task<List<Product>> GetProductsAsync(IDatabase db, string category, string sort, int page)
  {
      var key = $"query:{category}:{sort}:{page}";
      var cached = await db.StringGetAsync(key);
      if (!cached.IsNull) return (List<Product>)cached;
      var results = await _repository.GetProductsAsync(category, sort, page);
      await db.StringSetAsync(key, JsonSerializer.Serialize(results), TimeSpan.FromSeconds(300));
      return results;
  }
  ```

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** The correct implementation checks the cache first, deserializes on a hit, and serializes with a TTL on the miss path. B never reads the cache, C passes an un-serialized `List<Product>` to `StringSetAsync`, and D attempts an invalid cast from `RedisValue` directly to `List<Product>`.

</details>

---

### Question 29
During a flash sale, one listing query is requested hundreds of times per second. The cached result can be up to 60 seconds stale, but the team wants to avoid a database spike when the normal TTL is reached while keeping response latency low. Which query-caching strategy best fits this situation?

- **A.** Extend the fixed TTL to several hours during the sale so the key is unlikely to expire while traffic is high.
- **B.** Use stale-while-revalidate with soft and hard TTLs. Serve the cached result briefly while one worker refreshes it.
- **C.** Use a miss-time Redis lock. When the key expires, one request rebuilds while the remaining requests wait until the fresh value is written.
- **D.** Apply TTL jitter to query cache keys so many listing results are less likely to expire at the same instant.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Stale-while-revalidate serves the existing value — which is allowed to be up to 60 seconds stale — while a single worker refreshes it in the background. No request waits, and only one request reaches the database. Extending the TTL to several hours violates the 60-second staleness bound (A is wrong), a miss-time lock makes waiting requests spike latency (C is wrong), and TTL jitter spreads expiration across many keys rather than protecting one hot key (D is wrong).

</details>

---

### Question 30
Your team is investigating two patterns of unexpected key removal in Redis. In the first, a product key is consistently gone after the same amount of time regardless of how frequently it is accessed. In the second, product keys disappear only during high write volume, Redis memory usage is at its configured limit, and the server's eviction counter is increasing. What is the most likely explanation for each scenario?

- **A.** The first is TTL-based expiration. The second is caused by memory-based eviction, but only keys that already have a TTL set are at risk. Redis never evicts persistent keys when memory is exhausted.
- **B.** The first is TTL-based expiration. Redis removed the key after its time-to-live elapsed, regardless of access patterns. The second is memory-based eviction. Redis hit its maxmemory limit and began removing keys as new writes arrived.
- **C.** The first is memory-based eviction using volatile-ttl, which removes the key closest to its expiration deadline. The second is TTL-based expiration where short, randomized TTLs are causing keys to expire unpredictably under load.
- **D.** Both are TTL-based expiration. The second scenario occurs because Redis uses lazy expiration, deferring deletion of expired keys until they are accessed, so keys appear to vanish unpredictably rather than at a fixed time.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** A fixed lifetime regardless of access is TTL expiry. Removal that tracks write volume with a rising eviction counter at the memory limit is maxmemory eviction. They are independent mechanisms: `allkeys-*` eviction can remove persistent keys that have no TTL at all (A is wrong), predictable fixed-duration removal is TTL expiry rather than `volatile-ttl` eviction (C is wrong), and an increasing eviction counter at `maxmemory` indicates memory eviction rather than lazy TTL expiration (D is wrong).

</details>

---

## Questions 31 – 40: TTL, Persistence, Transactions & Concurrency

### Question 31
You're debugging a caching issue and need to check when a specific product key is set to expire. You run `EXPIRETIME product:42` in the Redis CLI. Under which conditions would this command return `-1`?

- **A.** The key `product:42` exists but has no expiration set — it will persist until explicitly deleted or evicted.
- **B.** The key `product:42` was created with `SETNX` and the `EXPIRETIME` command is not compatible with keys created using conditional set operations.
- **C.** The key `product:42` has an expiration set, but it has less than 1 second remaining before it expires.
- **D.** The key `product:42` does not exist in the database at all.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** `EXPIRETIME` returns the absolute Unix expiry timestamp, `-1` when the key exists but has no expiry, and `-2` when the key does not exist (D is wrong). Keys created with `SETNX` work normally with `EXPIRETIME` (B is wrong), and a key with less than 1 second remaining still returns its positive Unix expiration timestamp (C is wrong).

</details>

---

### Question 32
Your team cached products with a 5-minute TTL using `await db.StringSetAsync(key, data, TimeSpan.FromSeconds(300))`. Later, a new feature was added that updates the cached stock count whenever inventory changes:

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

After deploying this feature, the ops team notices that some product keys are never expiring. What is the root cause?

- **A.** The `StringSetAsync` call in the update method overwrites the key without specifying a TTL. That discards the existing expiration, so the key persists until deleted or evicted.
- **B.** `JsonSerializer.Deserialize` and `JsonSerializer.Serialize` corrupt the TTL metadata embedded in the serialized value, so Redis can no longer determine when the key should expire.
- **C.** The `if (!cached.IsNull)` check prevents the method from running when the key does not exist, but it also prevents the method from restoring the TTL on keys that have already expired and been recreated by another process.
- **D.** Calling `db.StringGetAsync` on a key resets its TTL to infinite, because Redis treats any read as a signal that the key is still in active use.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** `SET` replaces the key and drops its TTL unless you pass `KEEPTTL` or re-specify the expiry. The update path here silently converts every product it touches into a permanent key. TTL is stored in Redis keyspace metadata rather than inside the JSON payload (B is wrong), the `!cached.IsNull` check merely guards against cache misses (C is wrong), and `StringGetAsync` reads never alter or reset a key's TTL (D is wrong).

</details>

---

### Question 33
You have a product cached as a Hash with a 5-minute TTL:

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

What happens to the TTL on `product:42` after the update call?

- **A.** The TTL is unaffected — `HashSet` updates a field within the Hash without replacing the key itself, so the existing expiration continues counting down from where it was.
- **B.** The TTL is preserved only if the updated field already had its own field-level expiration set. Without a field-level TTL, the hash key loses its expiration after `HashSet` is called.
- **C.** The TTL is removed entirely because `HashSet` overwrites the key, and any overwrite discards the existing expiration — similar to how `StringSet` behaves on a String key.
- **D.** The TTL is reset to 300 seconds because any write operation on a key automatically refreshes its expiration.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** `HSET` writes a field inside an existing key. The TTL belongs to the key, not the field, so it keeps counting down. Preserving the key's TTL does not depend on field-level expiration (B is wrong), `HSET` does not replace the key or clear its TTL like `SET` does (C is wrong), and writing to a key does not automatically refresh its TTL back to 300 seconds (D is wrong).

</details>

---

### Question 34
Your team is evaluating persistence for a Redis product cache that uses cache-aside in front of a relational database. Redis is not the source of truth, and losing the most recent few minutes of cached entries after a crash is acceptable. The main goal is to avoid a completely cold cache after restart while keeping normal cache writes lightweight and restart loading fast. Which persistence strategy best fits this priority?

- **A.** Enable AOF with `appendfsync always` so each cache write is synced immediately, prioritizing the lowest possible data loss.
- **B.** Enable RDB snapshots at regular intervals so Redis can restart from a recent point-in-time cache state.
- **C.** Disable persistence and require the application to pre-fetch the full product catalog before accepting traffic.
- **D.** Enable AOF with `appendfsync everysec` so Redis replays recent cache writes and prioritizes lower data loss.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** RDB gives cheap writes and fast restart loading from a compact point-in-time snapshot, which is the right trade when Redis is not the source of truth and losing the last few minutes is acceptable. AOF with `always` (A) or `everysec` (D) adds write overhead and slower startup log replay for durability guarantees a cache does not need, while disabling persistence and pre-fetching the entire catalog (C) delays startup and overloads the database.

</details>

---

### Question 35
When a customer views a product page, your application needs to perform three Redis operations:
1. Fetch the cached product data
2. Increment the page view counter
3. Check if the product is in the user's wishlist set.

None of these operations depend on each other's results. A team member suggests wrapping them in a transaction using `MULTI/EXEC`. Another suggests using a batch. Which approach is more appropriate and why?

- **A.** A transaction is more appropriate because it ensures all three operations execute on the server without any other client's commands interleaving between them, which prevents data corruption when multiple users view the same product simultaneously.
- **B.** A transaction is more appropriate because batches can only group write operations. Since one of the three operations is a read, a batch would fail and a transaction is required.
- **C.** A batch is more appropriate because the three operations are independent reads and writes with no need for atomicity. A batch groups them for efficiency without adding transactional guarantees that are not needed here.
- **D.** Neither is appropriate because `StackExchange.Redis` already multiplexes concurrent callers efficiently, so explicitly batching independent operations from one caller does not improve throughput.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** Reach for a transaction only when you need atomicity or isolation. These three operations are independent, so a batch — which pipelines them into one round trip without `MULTI`/`EXEC` overhead — is the cheaper correct tool (A is wrong). Batches support both reads and writes (B is wrong), and batching multiple independent calls from a single caller still reduces latency compared to awaiting three sequential round trips (D is wrong).

</details>

---

### Question 36
When a customer adds a product to their cart, your application needs to atomically decrement the stock count and add the product to the customer's cart Set. You review the following implementation:

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

The product's stock is currently 10 and the customer's cart is empty. What values are printed for Stock and Cart added?

- **A.** Stock is 9 and Cart added is true. `HashIncrementAsync` returns the new value after increment, and `SetAddAsync` returns true because the member was new to the Set.
- **B.** Stock is "OK" and Cart added is "OK". Both commands return status strings indicating success.
- **C.** Both are null because transaction results are not available until a separate `GetResults()` call.
- **D.** Stock is -1 and Cart added is 1. The results reflect the delta applied, not the post-operation state.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Inside a `StackExchange.Redis` transaction the Tasks complete once `ExecuteAsync` returns. `HINCRBY` returns the value after the increment (`9`), and `SADD` returns `true` for a member that was not already present. Neither command returns `"OK"` status strings (B is wrong), transaction Tasks populate automatically upon `ExecuteAsync()` without a `GetResults()` call (C is wrong), and `HashIncrementAsync` returns the post-increment value (`9`) while `SetAddAsync` returns a `bool` (`true`) rather than deltas (D is wrong).

</details>

---

### Question 37
Your team implements a last-item purchase check using a read-then-write pattern:

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

During load testing with stock set to 1, two customers call this function simultaneously. Both succeed in adding the product to their cart, but only one item was available. What causes this, and what is the correct fix?

- **A.** Both requests read `stock = 1` before either writes. Each writes 0, so both pass the check. The fix is to use one atomic server-side decrement such as `HashIncrementAsync(..., -1)`, then reject or compensate if the result is negative.
- **B.** `int.Parse` introduces a timing delay between the read and write. The fix is to compare stock as a string instead of converting it to an integer before the conditional check.
- **C.** The client may reorder `SetAddAsync` ahead of `HashSetAsync` for throughput. The fix is to wrap both commands in a transaction without conditions, which guarantees only one request can complete successfully.
- **D.** `HashGetAsync` returns a stale cached value from the client library, so both requests see 1 after the first write. The fix is to disable client-side caching on the read so each request sees the latest server value.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** A textbook check-then-act race: both callers read `stock = 1` before either writes, so both pass the guard. `HINCRBY` with `-1` performs the read and the write in one atomic server-side step, so exactly one caller drives the value below zero and can be rejected or compensated. The race stems from separate network round trips rather than `int.Parse` CPU overhead (B is wrong), an unconditional `MULTI`/`EXEC` transaction after reading `stock = 1` still lets both callers write `0` (C is wrong), and `StackExchange.Redis` does not cache `HashGetAsync` responses locally (D is wrong).

</details>

---

### Question 38
A Redis `INFO keyspace` report includes this line: `db0:keys=25,expires=11,avg_ttl=285000`. What does `expires=11` mean?

- **A.** 11 keys are permanent and will not expire.
- **B.** 11 keys were evicted because Redis ran out of memory.
- **C.** 11 keys have already expired but have not been deleted yet.
- **D.** 11 keys have an expiration set.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** In `INFO keyspace`, `keys` is the total number of keys in the database (`25`) and `expires` is how many of those currently carry a TTL (`11`). That means `14` keys (`25 - 11`) are permanent without an expiration (A is wrong), evicted keys are tracked separately under `evicted_keys` in `INFO stats` (B is wrong), and `expires` counts active keys with a scheduled TTL rather than already-expired keys awaiting deletion (C is wrong).

</details>

---

### Question 39
A production Redis database has millions of keys. Your team needs to find keys matching `product:*` without blocking Redis. Which statement about `SCAN 0 MATCH product:* COUNT 1000` is correct?

- **A.** It returns all matching keys in one call because the cursor starts at 0.
- **B.** It returns exactly 1000 matching keys unless fewer than 1000 exist.
- **C.** It is one step in a cursor scan. The caller must continue until the cursor returns to 0.
- **D.** It is equivalent to `KEYS product:*`, but safer because it only checks keys with the `product:` prefix.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** `SCAN` is a cursor-based iterator, not a one-shot query. Starting at cursor `0` only initiates the first iteration rather than returning all matches in one call (A is wrong), `COUNT 1000` is a hint about how many hash slots to inspect per call rather than a guarantee of 1000 returned matches (B is wrong), and `SCAN` still walks the full keyspace hash table incrementally rather than only inspecting keys with the `product:` prefix (D is wrong).

</details>

---

### Question 40
You run `TTL product:45`, and Redis returns `-1`. What does that mean?

- **A.** The key has less than one second before it expires.
- **B.** Redis could not determine the key's TTL.
- **C.** The key does not exist.
- **D.** The key exists but has no expiration set.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** `TTL` returns `-1` for "key exists, no expiry" and `-2` for "key does not exist" (C is wrong). A key with less than one second remaining returns `0` in whole seconds (A is wrong), and Redis always knows a key's expiration state (B is wrong).

</details>

---

## Questions 41 – 50: Keyspace Management, Lists & Sets

### Question 41
An app verifies a generated list of cache keys by running `EXISTS` and comparing the integer result to the list length. The generated list can contain duplicate key names. What is the main risk with this approach?

- **A.** With multiple arguments, `EXISTS` returns only 0 or 1, so comparing it to the list length is invalid.
- **B.** A repeated existing key can be counted more than once, so the check can pass even when a distinct required key is missing.
- **C.** Redis treats duplicate key arguments as a syntax error and returns no count.
- **D.** Redis removes duplicate names before counting, so the check can fail even when all required keys exist.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `EXISTS` with multiple arguments counts each existing key occurrence rather than distinct keys. A key listed twice contributes `2` to the total, which can make the count match the list length even though a different, genuinely required key is missing. Variadic `EXISTS` returns the integer count of hits rather than just `0` or `1` (A is wrong), duplicate key arguments are valid syntax (C is wrong), and Redis does not deduplicate arguments before counting (D is wrong).

</details>

---

### Question 42
A large product catalog is stored as a Redis Hash with many fields. A reviewer wants an exact RAM measurement for the full aggregate value, including Redis overhead. Which statement about `MEMORY USAGE product:catalog` is correct?

- **A.** It reports the RDB serialized payload size, so it should match `DUMP product:catalog`.
- **B.** It reports memory in bytes, but aggregate values may use sampling unless `SAMPLES 0` is specified.
- **C.** It reports nil for Hashes because memory usage can only be measured for Strings.
- **D.** It reports only field values and excludes Redis object overhead.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `MEMORY USAGE` reports RAM consumption in bytes including Redis object overhead, but for aggregate types it samples a subset of nested elements by default (`5` samples). Passing `SAMPLES 0` forces an exact traversal of every element. It measures live in-memory allocation rather than the compressed `DUMP` payload size (A is wrong), works on all data types including Hashes (C is wrong), and includes Redis object and pointer overhead rather than only raw field values (D is wrong).

</details>

---

### Question 43
Your team is designing the key namespace for the food delivery platform. Which key naming approach provides the best organization for debugging and operational monitoring?

- **A.** Use a consistent hierarchical namespace with colon separators that starts with the data type: `menu:rest:5`, `orders:recent:rest:5`, `trending:dishes`, `customers:unique:2025-03-25`
- **B.** Use a consistent hierarchical namespace with colon separators, but use human-readable restaurant names as the primary segment: `menu:sakura-sushi`, `orders:recent:sakura-sushi`, `trending:dishes`, `customers:unique:2025-03-25`
- **C.** Use a consistent hierarchical namespace with colon separators, entity first: `rest:5:menu`, `rest:5:orders:recent`, `dishes:trending`, `customers:unique:2025-03-25`
- **D.** Prefix every key with the application and environment, but vary the remaining segment order by feature: `fooddelivery:prod:menu:rest:5`, `fooddelivery:prod:5:recent:orders`, `fooddelivery:prod:dishes:trending`, `fooddelivery:prod:2025-03-25:customers:unique`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** This is a convention question rather than a hard technical rule. Redis's own guidance favours a consistent colon-delimited hierarchy starting with the feature/collection prefix (`menu:rest:5`, `orders:recent:rest:5`), which makes prefix scanning (`SCAN 0 MATCH menu:*`) predictable. Using mutable display names like `sakura-sushi` instead of stable IDs breaks keys if a restaurant rebrands (B is wrong), entity-first prefixes scatter keys of the same feature across different restaurant IDs when scanning by feature (C is less suited for feature-level monitoring here), and varying segment order by feature makes prefix scans unreliable (D is wrong).

</details>

---

### Question 44
Your team is implementing the recent orders feed using a Redis List: `LPUSH` on each completed order, `LTRIM` to cap at 50, and `LRANGE 0 49` to retrieve. A teammate argues you should switch to a Sorted Set because it would make the ordering explicit by storing each order's completion timestamp as the score. Which of the following are valid reasons to keep the List?

*Choose 3 answers*

- **A.** Orders arrive in the correct order naturally, so no scoring mechanism is needed to maintain the feed's sequence.
- **B.** `LPUSH` and `LTRIM` together provide a simple and natural pattern for maintaining a capped recent-orders feed.
- **C.** The feed does not require ranking, range queries by score, or weighted ordering, so none of the extra capabilities a Sorted Set adds are needed here.
- **D.** Lists generally use less memory than Sorted Sets for simple feeds, so memory efficiency should be the main reason to prefer them here.
- **E.** A Sorted Set would require the application to guarantee that no two orders share the same timestamp, since duplicate scores corrupt the feed's ordering.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** A, B, C

> **Why:** The List already encodes arrival order, and `LPUSH` plus `LTRIM` is the idiomatic capped-feed pattern. D and E are wrong on the facts: memory is not the deciding factor at 50 elements (D is wrong), and duplicate scores do not corrupt a Sorted Set — ties simply break lexicographically by member string (E is wrong).

</details>

---

### Question 45
You're reviewing the implementation for adding a completed order to a restaurant's recent orders feed. What does the `await db.ListTrimAsync(key, 0, 49)` call accomplish?

```csharp
public async Task AddCompletedOrderAsync(IDatabase db, int restaurantId, Order orderData)
{
    var key = $"orders:recent:{restaurantId}";
    await db.ListLeftPushAsync(key, JsonSerializer.Serialize(orderData));
    await db.ListTrimAsync(key, 0, 49);
}
```

- **A.** It removes the first 49 elements from the list, keeping only elements from index 50 onward.
- **B.** It sets a maximum capacity of 49 on the list. Any future `ListLeftPushAsync` calls will silently fail once the list reaches this capacity.
- **C.** It removes elements at indices 0 through 49, clearing the first 50 entries.
- **D.** It keeps elements at indices 0 through 49 (the 50 most recent orders) and removes everything beyond that, ensuring the list never grows past 50 elements.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** `LTRIM` keeps the given inclusive index range (`0` through `49`, which is 50 elements) and discards everything outside it. The range specifies which elements to *retain* rather than which elements to delete (A and C are wrong), and `LTRIM` is an immediate one-off trim operation rather than a persistent capacity setting on the key (B is wrong).

</details>

---

### Question 46
Your team's dashboard component fetches the recent orders feed for display. A new restaurant was just onboarded and hasn't received any orders yet. What does this method return when called for that restaurant?

```csharp
public List<Order> GetRecentOrders(IDatabase db, int restaurantId)
{
    var key = $"orders:recent:{restaurantId}";
    var orders = db.ListRange(key, 0, 49);
    return orders.Select(o => JsonSerializer.Deserialize<Order>(o)).ToList();
}
```

- **A.** It returns null because `ListRange` returns null for keys that don't exist, and the `.Select()` call will throw a `NullReferenceException`.
- **B.** It throws a `KeyNotFoundException` because `StackExchange.Redis` raises standard .NET collection exceptions when a Redis key is not found.
- **C.** It returns an empty `List<Order>` because `ListRange` returns an empty `RedisValue[]` when the key doesn't exist, and `Select` over an empty array produces an empty list.
- **D.** It throws a `RedisServerException` because the key doesn't exist yet and `ListRange` cannot operate on a missing key.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** In Redis, a missing key behaves like an empty collection, so `LRANGE` returns an empty array (`RedisValue[0]`). `Select` over an empty array yields an empty `List<Order>` — `ListRange` does not return `null` (A is wrong) and does not throw `KeyNotFoundException` (B is wrong) or `RedisServerException` (D is wrong) on a missing key.

</details>

---

### Question 47
Three orders complete in quick succession for a restaurant. Your application runs:

```csharp
db.ListLeftPush("orders:recent:5", JsonSerializer.Serialize(new { id = "A", item = "Pizza" }));
db.ListLeftPush("orders:recent:5", JsonSerializer.Serialize(new { id = "B", item = "Burger" }));
db.ListLeftPush("orders:recent:5", JsonSerializer.Serialize(new { id = "C", item = "Sushi" }));
var feed = db.ListRange("orders:recent:5", 0, 2);
```

What is the order of elements in `feed`?

- **A.** `[A-Pizza]`
- **B.** `[C-Sushi, B-Burger, A-Pizza]`
- **C.** `[C-Sushi, B-Burger]`
- **D.** `[A-Pizza, B-Burger, C-Sushi]`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `LPUSH` prepends each element to the head (left) of the list, so the newest order (`C-Sushi`) lands at index `0` and `LRANGE 0 2` reads newest-first: `C`, then `B`, then `A`. Because `LRANGE` stop indices are inclusive (`0` through `2`), it returns three elements rather than one or two (A and C are wrong), and `LPUSH` reverses insertion order rather than appending FIFO like `RPUSH` (D is wrong).

</details>

---

### Question 48
After deploying the recent orders feed, the ops team notices that restaurant dashboards occasionally show 51 or 52 orders instead of 50. You review the code:

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

The conditional trim appears correct. What is the most likely cause?

- **A.** `ListLeftPushAsync` returns the list length before the insertion, so the `length > 50` check is off by one and the trim does not run at the correct time.
- **B.** Two concurrent requests can both `ListLeftPushAsync` before either `ListTrimAsync` runs, creating a window where the list temporarily exceeds 50 entries and a dashboard read during that window sees the oversized list.
- **C.** `ListTrimAsync` returns before Redis trims the list, so the dashboard reads the list before the trim finishes on the server.
- **D.** `ListTrimAsync` removes one element per call, so a single trim only brings a list of 51 down to 50, but if two pushes arrive before the trim runs, the second push is never trimmed.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** The push and the trim are two separate network round trips. Two concurrent writers can both push before either trims, and a dashboard read landing in that window sees a list above its cap. `LPUSH` returns the length *after* insertion (A is wrong), `LTRIM` executes synchronously on the server before returning (C is wrong), and `LTRIM 0 49` removes *all* elements past index 49 in a single call rather than just one element (D is wrong).

</details>

---

### Question 49
Your team is tracking unique customers who ordered from each restaurant on a given day. Each time an order completes, the customer ID is added via `SADD`. The daily unique count is retrieved via `SCARD`. Which of the following are good reasons a Redis Set fits this use case?

*Choose 3 answers*

- **A.** Because duplicate customer IDs are stored only once, `SCARD` can return the Set's cardinality in $O(1)$ without scanning members.
- **B.** Sets automatically expire individual members after a configurable TTL, so yesterday's customers are removed without manual cleanup.
- **C.** Sets natively support union and intersection operations, so comparing unique customers across restaurants or across days can be done directly in Redis without pulling data into the application.
- **D.** Adding the same customer ID multiple times does not create duplicates, so uniqueness is enforced without application-side duplicate checks.
- **E.** Sets maintain insertion order, so customers can be retrieved in the order they first placed an order that day.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** A, C, D

> **Why:** A Set gives $O(1)$ cardinality via `SCARD`, native union and intersection, and idempotent adds. B is false — Redis Sets do not support per-member TTLs (expiration applies to the whole key) — and E is false, since Sets are unordered collections.

</details>

---

### Question 50
Your team implements the daily unique customer tracker:

```csharp
public void TrackCustomerOrder(IDatabase db, int customerId)
{
    var today = DateTime.UtcNow.ToString("yyyy-MM-dd");
    var key = $"customers:unique:{today}";
    bool added = db.SetAdd(key, customerId.ToString());
    Console.WriteLine(added);
}
```

Customer `cust:42` places three orders throughout the day. What does `added` equal on each of the three calls?

- **A.** `true` every time, because `SetAdd` returns true when the operation completes successfully, regardless of whether the member was already in the Set.
- **B.** `true` if the key already existed, false if this is the first member being added to a new Set.
- **C.** `true` the first time a customer orders that day, and `false` on subsequent orders from the same customer, because `SetAdd` returns whether the member was newly added to the Set.
- **D.** The current size of the Set after the addition, allowing you to track how many unique customers have ordered so far.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** `SADD` returns the number of members newly added, which `StackExchange.Redis` surfaces as a `bool`: `true` the first time that customer orders, `false` on repeats. It does not return `true` for duplicate additions (A is wrong), does not report whether the Set key previously existed (B is wrong), and returns a `bool` rather than the Set's total cardinality (which requires `SetLength` / `SCARD`, so D is wrong).

</details>

---

## Questions 51 – 60: Set Operations, Sorted Sets & JSONPath Filters

### Question 51
The marketing team wants to identify customers who ordered from two different restaurants on the same day for a cross-promotion campaign. You have `customers:unique:rest:5:2025-03-25` and `customers:unique:rest:7:2025-03-25`. Which Redis command finds these customers most efficiently?

- **A.** `SMEMBERS customers:unique:rest:5:2025-03-25` followed by `SISMEMBER` for each customer in the second set
- **B.** `SINTER customers:unique:rest:5:2025-03-25 customers:unique:rest:7:2025-03-25`
- **C.** `SUNION customers:unique:rest:5:2025-03-25 customers:unique:rest:7:2025-03-25`
- **D.** `SDIFF customers:unique:rest:5:2025-03-25 customers:unique:rest:7:2025-03-25`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `SINTER` computes the intersection on the server in one command. The `SMEMBERS`-then-`SISMEMBER` loop in A pulls an entire set across the wire and issues one round trip per customer, `SUNION` (C) returns customers who ordered from *either* restaurant, and `SDIFF` (D) returns customers who ordered from restaurant 5 but *not* restaurant 7.

</details>

---

### Question 52
At midnight, your application needs to clean up customer tracking sets from 7 days ago. You retrieve all customer IDs from the old set before deleting it to generate a weekly summary report:

```csharp
public async Task<string[]> ArchiveAndCleanupAsync(IDatabase db, string dateKey)
{
    var key = $"customers:unique:{dateKey}";
    var members = await db.SetMembersAsync(key);
    await db.KeyDeleteAsync(key);
    return members.Select(m => m.ToString()).ToArray();
}
```

- **A.** Replace the two commands with `SPOP` with a count parameter to atomically retrieve and remove all members in a single command.
- **B.** The code has a race condition. Another process might add a customer between `SetMembersAsync` and `KeyDeleteAsync`. Use `RENAME` to atomically move the key to an archive namespace, then read from there.
- **C.** Use `SSCAN` instead of `SMEMBERS` because `SMEMBERS` blocks the server for large sets. Then delete in a separate operation.
- **D.** Use `SMEMBERS` followed by `DEL` as shown. This is the correct approach since you need the full member list before deletion.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `SMEMBERS` and `DEL` are two separate commands, so any member added between them is silently lost (D is wrong). `RENAME` moves the key atomically into an archive namespace, after which you can read and delete it at leisure with no race. `SPOP` with a count also removes atomically, but you would either need `SCARD` first to learn the count (reintroducing a race) or guess an upper bound (A is less clean), and `SSCAN` followed by `DEL` still leaves a race window between reading and deleting (C is wrong).

</details>

---

### Question 53
Your analytics team needs an exact weekly unique customer count every Monday. You have daily Sets from `customers:unique:2025-03-24` through `customers:unique:2025-03-30`. You want Redis to compute the weekly union without returning all customer IDs to the application. Which approach is best?

- **A.** `SCARD` on each daily key, then sum the seven daily cardinalities.
- **B.** `SUNIONSTORE customers:unique:2025-W13 <7 daily keys>`, then use its integer reply.
- **C.** `SUNION` across the 7 daily keys, then count returned customers in the application.
- **D.** `SINTER` across the 7 daily keys, then count customers who appear every day.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `SUNIONSTORE` computes the union server-side and returns the cardinality of the stored result, so no customer IDs cross the network. Summing seven daily `SCARD`s (A) double-counts anyone who ordered on more than one day, `SUNION` (C) transfers all unique customer IDs to the application, and `SINTER` (D) counts only customers who ordered on *every single day* of the week.

</details>

---

### Question 54
Your team is implementing a "trending dishes" feature that shows the most-ordered dishes across all restaurants in the past hour. Each time a dish is ordered, you update a Sorted Set. What should the score represent to make the trending calculation accurate?

- **A.** The order's Unix timestamp. The most recently ordered dishes will have the highest scores and appear at the top.
- **B.** The order count. Increment the score by 1 each time the dish is ordered. Higher scores mean more orders.
- **C.** The dish's price. More expensive dishes are ranked higher to maximize revenue visibility.
- **D.** The dish's average rating. This allows the highest-rated dishes to rise to the top as customers leave feedback.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Trending means order frequency, so the score must accumulate order counts via `ZINCRBY` by `1` per order. A Unix timestamp score ranks by recency of the last order instead (A is wrong), while price (C) and average rating (D) rank by cost or review quality rather than popularity.

</details>

---

### Question 55
Your team initializes the trending dishes Sorted Set, then processes incoming orders:

```csharp
db.SortedSetAdd("trending:dishes", new SortedSetEntry[] {
    new("Pizza", 5),
    new("Burger", 3),
    new("Sushi", 8)
});

bool result = db.SortedSetAdd("trending:dishes", "Sushi", 12);
```

What does `result` equal, and what is Sushi's score after the second call?

- **A.** `result` is true and Sushi's score is 12. `SortedSetAdd` returns true because the score changed, treating it as a new entry.
- **B.** `result` is false and Sushi's score is 8. `SortedSetAdd` ignores the call entirely because Sushi is already a member.
- **C.** `result` is false and Sushi's score is 12. `SortedSetAdd` returns true when a member is new and false when an existing member's score is updated. The score is still updated.
- **D.** `result` is true and Sushi's score is 20. `SortedSetAdd` automatically adds the new score to the existing score.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** `ZADD`'s default integer reply counts newly added members, so re-adding an existing member returns `0` (`false`, so A is wrong) — yet its score is still overwritten to `12` (B is wrong). `ZADD` replaces the score rather than adding to it, which is what `ZINCRBY` (`SortedSetIncrement`) does (D is wrong).

</details>

---

### Question 56
You need to display the top 3 trending dishes with their order counts. The Sorted Set `trending:dishes` currently contains: Pizza (25), Burger (18), Sushi (42), Tacos (31), Salad (12). Which call retrieves the top 3 dishes with their scores, ordered from highest to lowest score?

- **A.**
  ```csharp
  SortedSetEntry[] top3 = db.SortedSetRangeByRankWithScores("trending:dishes", 0, 2);
  ```
- **B.**
  ```csharp
  RedisValue[] top3 = db.SortedSetRangeByRank("trending:dishes", 0, 2);
  ```
- **C.**
  ```csharp
  RedisValue[] top3 = db.SortedSetRangeByRank("trending:dishes", 0, 2, Order.Descending);
  ```
- **D.**
  ```csharp
  SortedSetEntry[] top3 = db.SortedSetRangeByRankWithScores("trending:dishes", 0, 2, Order.Descending);
  ```

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** Two things are needed: scores in the result (`SortedSetRangeByRankWithScores`) and descending order (`Order.Descending`). Rank ranges are 0-based and inclusive, so `0` to `2` returns three members. Option A defaults to `Order.Ascending` (lowest 3 dishes), Option B omits both scores and descending order, and Option C orders descending but returns only member names (`RedisValue[]`) without scores.

</details>

---

### Question 57
Each time a dish is ordered, the trending score needs to increment by 1. You review the code:

```csharp
public double RecordDishOrder(IDatabase db, string dishName)
{
    double newScore = db.SortedSetIncrement("trending:dishes", dishName, 1);
    return newScore;
}
```

The dish Ramen has never been ordered before — it doesn't exist in the Sorted Set. What happens when this method is called for Ramen?

- **A.** The call throws a `RedisServerException` because `SortedSetIncrement` requires the member to already exist before its score can be incremented.
- **B.** The call creates Ramen as a new member with a score of 1.0 and returns 1.0. `SortedSetIncrement` treats a non-existent member as having a score of 0 before applying the increment.
- **C.** The call creates Ramen as a new member with a score of 0.0 and returns 0.0. The increment is applied on the next call.
- **D.** The call adds Ramen but returns `Double.NaN` because the member didn't previously exist. The score is set internally but isn't returned until the next `SortedSetScore` call.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `ZINCRBY` treats a missing member as having score `0`, creates it, applies the increment immediately, and returns the resulting score (`1.0`). It does not throw an exception on missing members (A is wrong), does not initialize at `0.0` without applying the increment (C is wrong), and never returns `Double.NaN` (D is wrong).

</details>

---

### Question 58
Your team uses `ZRANK` to show each dish's ranking position on the trending page. The Sorted Set contains: Salad (12), Burger (18), Pizza (25), Tacos (31), Sushi (42). You run `ZRANK trending:dishes Pizza`. What does it return, and why?

- **A.** 2 — `ZRANK` is 0-based and orders from lowest to highest score.
- **B.** 3 — `ZRANK` is 1-based and orders from highest to lowest score.
- **C.** 2 — `ZRANK` is 0-based and orders from highest to lowest score.
- **D.** 25 — `ZRANK` returns the member's score, not its positional rank.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** `ZRANK` is 0-based and ranks ascending by score (lowest to highest). With Salad at `0` and Burger at `1`, Pizza is at rank `2`. Redis ranks are 0-based rather than 1-based (B is wrong), descending rank requires `ZREVRANK` (although Pizza happens to be `2` from either end in a 5-element set, C's explanation of `ZRANK`'s ordering is wrong), and `ZSCORE` returns the score `25` rather than `ZRANK` (D is wrong).

</details>

---

### Question 59
Your team stores each restaurant's menu as a JSON document:

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

You need to retrieve the prices of all items across all categories. Which call accomplishes this?

- **A.**
  ```csharp
  var prices = json.Get("menu:rest:5", path: "$.categories.items.price");
  ```
- **B.**
  ```csharp
  var prices = json.Get("menu:rest:5", path: "$.categories[*].items[*].price");
  ```
- **C.**
  ```csharp
  var prices = json.Get("menu:rest:5", path: "$.price");
  ```
- **D.**
  ```csharp
  var prices = json.Get("menu:rest:5", path: "$.categories[0].items[0].price");
  ```

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `[*]` is the array wildcard that walks every element of an array, so `$.categories[*].items[*].price` collects prices across all categories and items. A dotted path without `[*]` does not descend into JSON arrays (A is wrong), `$.price` only checks for a top-level `price` property (C is wrong), and `[0]` indices retrieve only the first item of the first category (D is wrong).

</details>

---

### Question 60
A restaurant stores its menu as this JSON document:

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

The restaurant updates Edamame from $5.99 to $6.99. Category and item order may change over time, but dish names are unique within the menu. Which approach updates only Edamame's price without replacing the entire document?

- **A.**
  ```csharp
  json.Set("menu:rest:5", "$",
      new { categories = new[] { new { items = new[] { new { dish = "Edamame", price = 6.99 } } } } });
  ```
- **B.**
  ```csharp
  json.Set("menu:rest:5", "categories.items.price", 6.99);
  ```
- **C.**
  ```csharp
  json.Set("menu:rest:5", "$.categories[0].items[0].price", 6.99);
  ```
- **D.**
  ```csharp
  json.Set("menu:rest:5", "$.categories[*].items[?(@.dish==\"Edamame\")].price", 6.99);
  ```

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** A JSONPath filter expression `[?(@.dish=="Edamame")]` selects by content rather than array position, so the update still targets Edamame even if categories or items are reordered. Option A overwrites the root `"$"` and wipes out the rest of the menu, Option B fails to traverse the arrays or filter for Edamame, and Option C uses hard-coded `[0]` indices that break when array order changes.

</details>

---

## Questions 61 – 65: JSON Merge Patching & Production Operations

### Question 61
A restaurant needs to update its menu document in one call: change the phone number, add a new website field, and remove the fax field. Which `JSON.MERGE` call achieves all three changes?

- **A.**
  ```csharp
  json.Merge("menu:rest:5", "$", "{\"phone\":\"555-0200\",\"website\":\"sakurasushi.com\"}");
  json.Del("menu:rest:5", "$.fax");
  ```
- **B.**
  ```csharp
  json.Merge("menu:rest:5", "$", "{\"phone\":\"555-0200\",\"website\":\"sakurasushi.com\",\"fax\":null}");
  ```
- **C.**
  ```csharp
  json.Set("menu:rest:5", "$", "{\"phone\":\"555-0200\",\"website\":\"sakurasushi.com\",\"fax\":null}");
  ```
- **D.**
  ```csharp
  json.Merge("menu:rest:5", "$", "{\"phone\":\"555-0200\",\"website\":\"sakurasushi.com\",\"fax\":\"\"}");
  ```

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `JSON.MERGE` follows RFC 7386 JSON Merge Patch semantics: supplied non-null fields are updated or added, and a `null` value deletes that property. Option A uses two separate commands instead of one call, Option C uses `JSON.SET` at `"$"` which overwrites the entire document with only those three properties (leaving `"fax": null` intact), and Option D sets `fax` to an empty string `""` rather than removing it.

</details>

---

### Question 62
After a production server crash, the team discovers that the last 3 minutes of orders were lost. Restaurant dashboards showed orders that are no longer in Redis. The current persistence configuration uses RDB snapshots every 5 minutes. What change would minimize data loss for this real-time orders use case?

- **A.** Disable persistence entirely and rely on the application to replay orders from the primary database on Redis restart.
- **B.** Increase RDB snapshot frequency to every 60 seconds. This reduces the maximum data loss window while keeping the simpler snapshot-based recovery.
- **C.** Switch to AOF with `appendfsync everysec`. This writes operations to the append-only log every second, limiting data loss to approximately one second rather than up to 5 minutes.
- **D.** Enable AOF with `appendfsync always` so that every write is immediately persisted to disk, guaranteeing zero data loss.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** AOF with `appendfsync everysec` bounds the loss window to roughly one second while keeping write throughput high. Disabling persistence (A) requires slow application-side replay on restart, 60-second RDB snapshots (B) still risk up to a full minute of lost orders, and D's claim of "guaranteeing zero data loss" is an overstatement — `appendfsync always` severely degrades write throughput and still cannot guarantee zero loss under catastrophic storage failure.

</details>

---

### Question 63
Your operations team needs to audit all restaurant menu keys to verify a migration completed successfully. The production Redis instance has 50 million keys across all data types. Which approach safely retrieves all `menu:rest:*` keys without impacting production traffic?

- **A.**
  ```text
  OBJECT FREQ menu:rest:*
  ```
- **B.**
  ```text
  SCAN 0 MATCH menu:rest:* COUNT 1000  (in an iterative loop)
  ```
- **C.**
  ```text
  DBSIZE followed by RANDOMKEY in a loop
  ```
- **D.**
  ```text
  KEYS menu:rest:*
  ```

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `SCAN` iterates the keyspace in small non-blocking chunks so production traffic can interleave between calls. `OBJECT FREQ` inspects the LFU frequency counter of a single key rather than matching patterns (A is wrong), `RANDOMKEY` samples keys randomly with replacement and cannot reliably enumerate a subset (C is wrong), and `KEYS` scans all 50 million keys in one blocking pass that freezes the single-threaded server (D is wrong).

</details>

---

### Question 64
At the end of each day, your cleanup job needs to delete the trending dishes Sorted Set, which contains approximately 100,000 members. You want to minimize impact on concurrent operations. Which approach is best?

- **A.**
  ```text
  ZREMRANGEBYRANK trending:dishes:2025-03-25 0 -1
  ```
- **B.**
  ```text
  EXPIRE trending:dishes:2025-03-25 1
  ```
- **C.**
  ```text
  UNLINK trending:dishes:2025-03-25
  ```
- **D.**
  ```text
  DEL trending:dishes:2025-03-25
  ```

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** `UNLINK` removes the key from the keyspace immediately and reclaims the memory of its 100,000 members asynchronously on a background thread. `ZREMRANGEBYRANK` (A) and `DEL` (D) deallocate all 100,000 elements synchronously on the main command thread and block concurrent traffic, while `EXPIRE ... 1` (B) unnecessarily delays removal by 1 second and may still free memory synchronously unless `lazyfree-lazy-expire` is enabled.

</details>

---

### Question 65
Your cleanup routine receives 500 exact Redis key names to remove from a standalone Redis database. The deletes do not need transaction semantics. Which `StackExchange.Redis` implementation is the most appropriate async approach?

```csharp
public async Task<long> CleanupOldKeysAsync(IDatabase db, string[] keysToDelete)
{
    // Implementation here
}
```

- **A.**
  ```csharp
  var redisKeys = keysToDelete.Select(k => (RedisKey)k).ToArray();
  return await db.KeyDeleteAsync(redisKeys);
  ```
- **B.**
  ```csharp
  var tasks = keysToDelete.Select(key => db.KeyDeleteAsync(key)).ToArray();
  var results = await Task.WhenAll(tasks);
  return results.Count(deleted => deleted);
  ```
- **C.**
  ```csharp
  long deleted = 0;
  foreach (var key in keysToDelete)
  {
      if (await db.KeyDeleteAsync(key)) deleted++;
  }
  return deleted;
  ```
- **D.**
  ```csharp
  return (long)await db.ExecuteAsync("DEL", string.Join(" ", keysToDelete));
  ```

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Passing the `RedisKey[]` array to `KeyDeleteAsync` issues a single variadic `DEL` command — one network round trip and one command execution for all 500 keys. Option B issues 500 separate `DEL` commands, Option C awaits 500 sequential network round trips one by one, and Option D's `string.Join(" ", keysToDelete)` passes a single space-concatenated string as one malformed key name rather than 500 separate arguments.

</details>

