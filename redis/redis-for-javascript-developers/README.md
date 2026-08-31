# Redis for JavaScript Developers (RU102JS) — Question Bank

[![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)](https://redis.io/)
[![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org/)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Questions](https://img.shields.io/badge/Questions-45%20Verified%20MCQs-success?style=for-the-badge)](#table-of-contents)
[![Cheat Sheet](https://img.shields.io/badge/Study_Guide-Cheat_Sheet-orange?style=for-the-badge)](CHEAT_SHEET.md)

Comprehensive Multiple Choice Question (MCQ) Practice Bank for the **Redis for JavaScript Developers (RU102JS)** certification from Redis University. Verified against official course objectives, Node.js (`node-redis` v4+) client design patterns, Streams, Geospatial indexing, and Redis Stack modules.

> [!TIP]
> Preparing for the exam? Review the [Redis for JavaScript Developers Last-Minute Cram Sheet](CHEAT_SHEET.md) for quick-fire code snippets, `node-redis` v4 methods, Streams consumer groups, and transaction patterns.

---

## Table of Contents

- [Domain 1: Node.js & `node-redis` Client Lifecycle (Q1 – Q8)](#domain-1-nodejs--node-redis-client-lifecycle)
- [Domain 2: Data Structures & Key Design Patterns in JavaScript (Q9 – Q18)](#domain-2-data-structures--key-design-patterns-in-javascript)
- [Domain 3: Geospatial Indexing & Search (Q19 – Q24)](#domain-3-geospatial-indexing--search)
- [Domain 4: Redis Streams & Event Streaming (Q25 – Q32)](#domain-4-redis-streams--event-streaming)
- [Domain 5: Transactions, Concurrency & Pub/Sub in Node.js (Q33 – Q39)](#domain-5-transactions-concurrency--pubsub-in-nodejs)
- [Domain 6: RedisJSON, RediSearch & Caching Architecture (Q40 – Q45)](#domain-6-redisjson-redisearch--caching-architecture)

---

## Domain 1: Node.js & `node-redis` Client Lifecycle

### Question 1
When using the official `node-redis` (v4+) library in a Node.js application, which step is **mandatory** before sending commands to the Redis server?

- **A.** Passing a callback function to every command.
- **B.** Calling `await client.connect()`.
- **C.** Instantiating a new client for every HTTP request.
- **D.** Calling `client.authSync()`.

**Correct answer:** B

> **Why:** In `node-redis` v4+, `createClient()` creates an unestablished client instance. You must explicitly invoke `await client.connect()` to open the socket connection before executing commands.

---

### Question 2
What happens in a Node.js application if a `node-redis` client encounters a connection drop and no `'error'` event listener has been registered on the client?

- **A.** The client silently swallows the error and reconnects without logging.
- **B.** Node.js emits an unhandled `'error'` event that terminates the Node.js process.
- **C.** The operating system restarts the Redis server.
- **D.** The command automatically falls back to an in-memory Map.

**Correct answer:** B

> **Why:** In Node.js EventEmitters, emitting an `'error'` event without an attached listener causes Node.js to throw an unhandled exception, crashing the process. Always attach `client.on('error', cb)`.

---

### Question 3
How should the `node-redis` client instance be managed across an Express.js web application?

- **A.** Create and connect a new client inside each route handler and call `client.disconnect()` when the response ends.
- **B.** Create a single shared client instance (Singleton), connect on application startup, and reuse it across all route handlers.
- **C.** Create a new client per active user session.
- **D.** Store the client instance in `localStorage`.

**Correct answer:** B

> **Why:** Redis clients maintain an asynchronous multiplexed TCP connection designed to handle concurrent requests efficiently. Reusing a single connected client avoids TCP connection overhead.

---

### Question 4
In `node-redis` v4+, what data type do all command methods return?

- **A.** Node.js style error-first callbacks `(err, result) => {}`
- **B.** Native JavaScript Promises (`Promise<T>`)
- **C.** Synchronous blocking values
- **D.** Observables

**Correct answer:** B

> **Why:** `node-redis` v4 is 100% Promise-based, allowing clean modern asynchronous programming using `async/await`.

---

### Question 5
Which option in `createClient({ socket: { ... } })` configures a custom reconnection backoff strategy in `node-redis`?

- **A.** `retry_strategy` (in v3) / `reconnectStrategy` (in v4+)
- **B.** `auto_restart`
- **C.** `loopInterval`
- **D.** `reconnect_timer`

**Correct answer:** A

> **Why:** In `node-redis` v4+, `socket.reconnectStrategy` is a function that receives the retry attempt count and returns the delay in milliseconds (or an `Error` to stop reconnecting).

---

### Question 6
You need to set a key `'session:abc'` with value `'user_123'` that expires automatically in 3600 seconds (1 hour). What is the correct syntax in `node-redis` v4?

- **A.** `await client.set('session:abc', 'user_123', 'EX', 3600)`
- **B.** `await client.set('session:abc', 'user_123', { EX: 3600 })`
- **C.** `await client.setExpire('session:abc', 'user_123', 3600)`
- **D.** `await client.set('session:abc', 'user_123', 3600)`

**Correct answer:** B

> **Why:** `node-redis` v4 uses options objects for modifiers such as expiration (`{ EX: seconds }`, `{ PX: milliseconds }`, `{ NX: true }`, `{ XX: true }`).

---

### Question 7
What does `await client.hGetAll('non_existent_key')` return in `node-redis` v4 when the requested key does not exist?

- **A.** `null`
- **B.** `undefined`
- **C.** An empty JavaScript object `{}`
- **D.** Throws a `KeyNotFoundError`

**Correct answer:** C

> **Why:** `node-redis` returns an empty object `{}` for non-existent Hashes. Because `{}` is truthy in JavaScript, check `Object.keys(result).length === 0` to verify existence.

---

### Question 8
Which method should be called to gracefully drain pending commands and close the Redis connection when shutting down a Node.js server?

- **A.** `client.destroy()`
- **B.** `client.quit()` / `client.disconnect()`
- **C.** `client.kill()`
- **D.** `client.close()`

**Correct answer:** B

> **Why:** `client.quit()` sends the `QUIT` command to Redis, waiting for in-flight commands to finish before closing the connection gracefully.

---

## Domain 2: Data Structures & Key Design Patterns in JavaScript

### Question 9
In a solar energy monitoring application, each solar site has properties like `name`, `capacityKwh`, `installedYear`, and `status`. Which Redis data structure is most appropriate to store each site as a single record without JSON parsing overhead?

- **A.** Redis String
- **B.** Redis Hash
- **C.** Redis List
- **D.** Redis Bitmap

**Correct answer:** B

> **Why:** Hashes represent flat objects with field-value pairs efficiently in memory, allowing individual fields (e.g. `capacityKwh`) to be retrieved or incremented without reading the full object.

---

### Question 10
You need to store solar site metadata using key namespacing best practices in Redis. Which key naming convention follows recommended Redis conventions?

- **A.** `sites-9001-info`
- **B.** `sites:9001:info`
- **C.** `SELECT * FROM sites WHERE id = 9001`
- **D.** `site9001`

**Correct answer:** B

> **Why:** Colon-separated namespaces (`entity:id:attribute`) are the standard Redis convention, providing logical grouping in tools like RedisInsight.

---

### Question 11
You want to atomically increment a site's daily generated kilowatt-hours field (`generatedKwh`) by `15.5` in a Redis Hash (`site:100`). Which command should you use?

- **A.** `HINCRBY site:100 generatedKwh 15.5`
- **B.** `HINCRBYFLOAT site:100 generatedKwh 15.5`
- **C.** `HSET site:100 generatedKwh 15.5`
- **D.** `INCRBY site:100.generatedKwh 15.5`

**Correct answer:** B

> **Why:** `HINCRBYFLOAT` increments hash fields containing floating-point decimal numbers atomically, whereas `HINCRBY` is strictly for 64-bit signed integers.

---

### Question 12
Which Redis data structure guarantees that all members are **unique** and provides mathematical operations like union, intersection, and difference?

- **A.** List
- **B.** Set
- **C.** String
- **D.** Stream

**Correct answer:** B

> **Why:** Redis Sets store unique, unordered string members and provide \(O(1)\) membership tests (`SISMEMBER`) along with set algebraic operations (`SINTER`, `SUNION`, `SDIFF`).

---

### Question 13
You are building a real-time leaderboard in Node.js ranking solar farms by their current power output. Which Redis data structure should you use?

- **A.** List
- **B.** Set
- **C.** Sorted Set (ZSet)
- **D.** Hash

**Correct answer:** C

> **Why:** Sorted Sets associate every unique member with a floating-point score, maintaining elements in sorted order for fast range queries (`ZRANGE`, `ZREVRANGEBYSCORE`) in \(O(\log N + M)\).

---

### Question 14
How do you retrieve the top 10 highest-ranked sites with their scores using `node-redis` v4?

- **A.** `await client.zRangeWithScores('leaderboard', 0, 9, { REV: true })`
- **B.** `await client.zGetTop('leaderboard', 10)`
- **C.** `await client.zRange('leaderboard', 0, 10)`
- **D.** `await client.sort('leaderboard', 'DESC')`

**Correct answer:** A

> **Why:** `zRangeWithScores` with `{ REV: true }` retrieves elements in descending order (highest score first) along with their scores.

---

### Question 15
An application needs to track unique daily website visitors across millions of users while keeping memory usage strictly under 15 KB per day. Which data structure should you use?

- **A.** Set
- **B.** List
- **C.** HyperLogLog
- **D.** Hash

**Correct answer:** C

> **Why:** HyperLogLog estimates the cardinality (unique items) of sets with a standard error of ~0.81% while consuming a fixed memory maximum of 12 KB regardless of how many millions of items are counted.

---

### Question 16
You need to record whether each user in a system with 1,000,000 users logged in today, using the minimum possible memory footprint. Which data structure should you use?

- **A.** Bitmap (`SETBIT` / `BITCOUNT`)
- **B.** Sorted Set
- **C.** Stream
- **D.** List

**Correct answer:** A

> **Why:** Bitmaps represent boolean flags mapped to integer offsets (e.g. `user_id`), allowing 1 million user flags to be stored in only ~122 KB of memory.

---

### Question 17
Which Redis command implements a blocking FIFO queue pop in Node.js worker processes?

- **A.** `LPOP`
- **B.** `RPOP`
- **C.** `BRPOP` / `BLPOP`
- **D.** `GET`

**Correct answer:** C

> **Why:** `BRPOP` blocks the client connection until an element is available on the list or a timeout occurs, avoiding CPU-intensive polling loops.

---

### Question 18
What is the time complexity of adding an element to the head of a Redis List using `LPUSH`?

- **A.** \(O(N)\)
- **B.** \(O(1)\)
- **C.** \(O(\log N)\)
- **D.** \(O(N^2)\)

**Correct answer:** B

> **Why:** Redis Lists are implemented as doubly-linked quicklists, making insertions and deletions at either head (`LPUSH`) or tail (`RPUSH`) \(O(1)\) constant time operations.

---

## Domain 3: Geospatial Indexing & Search

### Question 19
Under the hood, which Redis data structure powers Redis Geospatial commands (`GEOADD`, `GEODIST`, `GEOSEARCH`)?

- **A.** Hashes
- **B.** Sorted Sets (ZSets)
- **C.** Streams
- **D.** Bitmaps

**Correct answer:** B

> **Why:** Redis Geospatial indexes encode longitude and latitude coordinates into 52-bit integer Geohash values stored as scores inside standard Sorted Sets.

---

### Question 20
What is the correct order of coordinate arguments when invoking `GEOADD` in Redis and `node-redis`?

- **A.** Latitude, Longitude, Member
- **B.** Longitude, Latitude, Member
- **C.** Member, Latitude, Longitude
- **D.** Latitude, Member, Longitude

**Correct answer:** B

> **Why:** Redis Geospatial commands follow the standard spatial format: **Longitude first**, followed by **Latitude**, then **Member name** (`GEOADD key lon lat member`).

---

### Question 21
You need to find all solar sites located within a 50 km radius of San Francisco coordinates `(-122.4194, 37.7749)`. Which modern Redis command should you use?

- **A.** `GEOSEARCH`
- **B.** `GEOPOS`
- **C.** `GEODEL`
- **D.** `GEOSCAN`

**Correct answer:** A

> **Why:** `GEOSEARCH` (introduced in Redis 6.2 to replace deprecated `GEORADIUS`) searches for members within a circular radius or rectangular bounding box.

---

### Question 22
How do you invoke `GEOSEARCH` using `node-redis` v4?

- **A.** `await client.geoSearch('sites:geo', { longitude: -122.41, latitude: 37.77 }, { radius: 50, unit: 'km' })`
- **B.** `await client.geoRadius('sites:geo', -122.41, 37.77, 50, 'km')`
- **C.** `await client.geoFind('sites:geo', 50, 'km')`
- **D.** `await client.findNearby('sites:geo', -122.41, 37.77)`

**Correct answer:** A

> **Why:** In `node-redis` v4, `client.geoSearch()` accepts the key name, origin coordinate object (`{ longitude, latitude }`), and circle/box search parameters (`{ radius, unit }`).

---

### Question 23
What unit options are supported by Redis Geospatial distance queries?

- **A.** `m` (meters), `km` (kilometers), `mi` (miles), `ft` (feet)
- **B.** `km` and `miles` only
- **C.** `degrees` and `radians`
- **D.** `pixels` and `inches`

**Correct answer:** A

> **Why:** Redis supports four distance units: meters (`m`), kilometers (`km`), miles (`mi`), and feet (`ft`).

---

### Question 24
What is the valid latitude range supported by Redis Geospatial indexing?

- **A.** -90.0 to +90.0 degrees
- **B.** -85.05112878 to +85.05112878 degrees (Web Mercator projection limit)
- **C.** -180.0 to +180.0 degrees
- **D.** 0.0 to 360.0 degrees

**Correct answer:** B

> **Why:** Because Redis uses EPSG:3857 (Web Mercator), valid latitudes are bounded between **-85.05112878 and +85.05112878 degrees**, while longitudes span **-180 to +180 degrees**.

---

## Domain 4: Redis Streams & Event Streaming

### Question 25
Which Redis command is used to append a new event entry to a Redis Stream?

- **A.** `LPUSH`
- **B.** `XADD`
- **C.** `APPEND`
- **D.** `PUBLISH`

**Correct answer:** B

> **Why:** `XADD` appends a new message containing field-value pairs to a stream and returns the unique generated entry ID (e.g. `1693526400000-0`).

---

### Question 26
When appending events to a stream using `client.xAdd('mystream', '*', fields)`, what does the `'*'` argument signify?

- **A.** Broadcast the message to all channels.
- **B.** Instruct Redis to automatically generate the entry ID based on current Unix millisecond timestamp and sequence number.
- **C.** Match all wildcards.
- **D.** Delete all previous entries in the stream.

**Correct answer:** B

> **Why:** Passing `'*'` instructs Redis to auto-generate a monotonically increasing stream ID composed of `<millisecondsTime>-<sequenceNumber>`.

---

### Question 27
To prevent a Redis Stream from growing indefinitely in memory, how can you cap the stream to approximately 10,000 entries efficiently?

- **A.** Run a daily cron job that deletes the stream.
- **B.** Use `XADD mystream MAXLEN ~ 10000 * field value`.
- **C.** Set a TTL on each message.
- **D.** Manually execute `LTRIM`.

**Correct answer:** B

> **Why:** Using `MAXLEN ~ <count>` (approximate trimming using the tilde `~`) allows Redis to trim whole macro-nodes in the stream's radix tree with negligible CPU overhead.

---

### Question 28
What is the purpose of a **Consumer Group** in Redis Streams?

- **A.** To encrypt messages before transmission.
- **B.** To allow multiple consumer worker instances to cooperate by distributing messages so each message is processed by only one consumer in the group.
- **C.** To convert stream messages into PDF documents.
- **D.** To group users by geographical region.

**Correct answer:** B

> **Why:** Consumer groups allow load balancing across multiple worker processes, keeping track of which consumer has read which message and managing unacknowledged messages.

---

### Question 29
Which command does a worker in a consumer group execute to fetch **new, undelivered** messages from a stream?

- **A.** `XREADGROUP GROUP mygroup worker1 STREAMS mystream >`
- **B.** `XREADGROUP GROUP mygroup worker1 STREAMS mystream 0`
- **C.** `XPOP mystream`
- **D.** `RPOP mystream`

**Correct answer:** A

> **Why:** In `XREADGROUP`, passing the special ID `>` means "fetch only messages that have never been delivered to any consumer in this group." Passing `0` fetches the consumer's Pending Entries List (PEL).

---

### Question 30
What must a worker process do after successfully processing a stream message read from a consumer group?

- **A.** Call `client.xDel()`
- **B.** Send an acknowledgment using `client.xAck('stream', 'group', messageId)`
- **C.** Restart the Node.js server
- **D.** Call `client.save()`

**Correct answer:** B

> **Why:** `XACK` removes the message from the consumer group's Pending Entries List (PEL), confirming it has been processed and preventing duplicate redelivery.

---

### Question 31
What happens to messages that have been delivered to a worker via `XREADGROUP` but have **not** yet been acknowledged with `XACK`?

- **A.** They are immediately deleted from the stream.
- **B.** They remain recorded in the Pending Entries List (PEL) and can be inspected via `XPENDING` or claimed by another worker using `XCLAIM` / `XAUTOCLAIM`.
- **C.** They are returned to the sender.
- **D.** They trigger an immediate Redis crash.

**Correct answer:** B

> **Why:** The PEL tracks all in-flight messages awaiting confirmation. If a worker crashes, other workers can discover and claim abandoned messages using `XAUTOCLAIM`.

---

### Question 32
How can you implement a **Sliding Window Rate Limiter** (e.g. maximum 10 requests per minute per IP) in Node.js using Redis?

- **A.** Store each request timestamp as both score and member in a Sorted Set, remove timestamps older than 60 seconds (`ZREMRANGEBYSCORE`), count elements (`ZCARD`), and allow the request if count < 10.
- **B.** Use a single string key with `INCR` without expiration.
- **C.** Append IP addresses to a List.
- **D.** Run an asynchronous `setTimeout()` in Node.js memory.

**Correct answer:** A

> **Why:** Sorted sets enable atomic sliding window rate limiting by pruning old timestamps with `ZREMRANGEBYSCORE` and counting active window requests with `ZCARD`.

---

## Domain 5: Transactions, Concurrency & Pub/Sub in Node.js

### Question 33
What is the primary difference between standard **Pipelining** and a **Transaction** (`MULTI`/`EXEC`) in Redis?

- **A.** Pipelining sends multiple commands in a batch to save network roundtrips without transactional isolation; `MULTI`/`EXEC` guarantees that all commands execute sequentially and atomically without interference from other clients.
- **B.** Pipelining only works with Strings.
- **C.** Transactions do not work in Node.js.
- **D.** Pipelining requires root server privileges.

**Correct answer:** A

> **Why:** Pipelining batches network packets for performance. `MULTI`/`EXEC` ensures atomic, uninterrupted execution of the queued commands on the Redis server.

---

### Question 34
How is **Optimistic Concurrency Control** implemented in Redis to prevent race conditions during read-modify-write operations?

- **A.** `LOCK` and `UNLOCK` commands
- **B.** Using `WATCH key`, checking values, queuing modifications in `MULTI`, and executing with `EXEC` (which returns `null` if the watched key changed)
- **C.** Stopping the Redis event loop
- **D.** Disabling all other client connections

**Correct answer:** B

> **Why:** `WATCH` monitors keys for changes made by other connections. If any watched key is modified before `EXEC` is called, the transaction aborts and returns `null`.

---

### Question 35
You are building a Pub/Sub event subscriber in a Node.js microservice. Why must you create a separate client using **`client.duplicate()`** for the subscriber?

- **A.** Because Redis only allows one subscription per operating system.
- **B.** Because once a client enters subscriber mode (`SUBSCRIBE`), it is dedicated to listening for messages and cannot execute regular data commands (`GET`, `SET`).
- **C.** To double the bandwidth of the connection.
- **D.** Because Node.js does not support asynchronous networking.

**Correct answer:** B

> **Why:** A Redis client in Pub/Sub mode is locked into the subscription state and only accepts subscription management commands. `client.duplicate()` creates a dedicated socket connection for listening.

---

### Question 36
How does Redis Pub/Sub handle message delivery when a subscriber client is offline or disconnected when a message is published?

- **A.** Messages are saved on disk and replayed when the subscriber reconnects.
- **B.** Pub/Sub is **fire-and-forget**; messages sent while a subscriber is disconnected are lost permanently.
- **C.** Messages are automatically redirected to email.
- **D.** Redis pauses all publishers until the subscriber reconnects.

**Correct answer:** B

> **Why:** Redis Pub/Sub provides no persistence or buffering. If guaranteed delivery or offline playback is required, use **Redis Streams** instead.

---

### Question 37
What is the purpose of the `UNWATCH` command in Redis?

- **A.** To clear all keys currently monitored by `WATCH` on the current client connection.
- **B.** To delete the Redis database.
- **C.** To disconnect all subscribers from a channel.
- **D.** To reset user passwords.

**Correct answer:** A

> **Why:** `UNWATCH` flushes all monitored keys on the current connection, which is useful when an application detects that it does not need to proceed with a transaction.

---

### Question 38
In `node-redis` v4+, how do you execute a transactional batch of commands?

- **A.** `const results = await client.multi().set('k', 'v').incr('counter').exec();`
- **B.** `await client.transaction(['SET k v', 'INCR counter'])`
- **C.** `await client.begin(); await client.commit();`
- **D.** `client.execSync()`

**Correct answer:** A

> **Why:** `client.multi()` returns a transaction builder where commands are chained and atomically dispatched via `exec()`.

---

### Question 39
If a Redis transaction (`MULTI`/`EXEC`) contains a command that causes a runtime data error (e.g. calling `INCR` on a string that contains letters), how does Redis behave?

- **A.** Redis rolls back all previous commands in the transaction.
- **B.** Redis executes all other commands in the transaction; only the faulty command fails.
- **C.** The entire database is cleared.
- **D.** The Redis server shuts down.

**Correct answer:** B

> **Why:** Redis transactions do not support relational rollback (`ROLLBACK`). Commands with syntax errors are rejected before execution, but runtime errors execute remaining commands and report errors individually.

---

## Domain 6: RedisJSON, RediSearch & Caching Architecture

### Question 40
Which Redis Stack module allows storing, querying, and mutating nested JSON documents natively in-memory?

- **A.** RedisBloom
- **B.** RedisJSON
- **C.** RedisGraph
- **D.** RedisRaft

**Correct answer:** B

> **Why:** RedisJSON (`JSON.*`) provides high-performance native storage and manipulation of JSON documents according to the JSONPath standard.

---

### Question 41
Using RedisJSON, how do you atomically increment a numeric property `$.stats.views` inside a JSON document `user:100`?

- **A.** `JSON.NUMINCRBY user:100 $.stats.views 1`
- **B.** `INCR user:100.stats.views`
- **C.** `JSON.SET user:100 $.stats.views 1`
- **D.** `HINCRBY user:100 stats.views 1`

**Correct answer:** A

> **Why:** `JSON.NUMINCRBY` modifies numeric JSON properties in place on the server without needing to fetch, deserialize, increment in JavaScript, and re-serialize.

---

### Question 42
When creating a secondary search index with RediSearch (`FT.CREATE`), which field type is best suited for exact-match categorical values such as status codes (`active`, `pending`) or GUIDs?

- **A.** `TEXT`
- **B.** `TAG`
- **C.** `NUMERIC`
- **D.** `GEO`

**Correct answer:** B

> **Why:** `TAG` fields index exact strings without stemming or tokenization, enabling efficient exact-match filters (`@status:{active}`). `TEXT` fields perform full-text stemmed search.

---

### Question 43
In the **Cache-Aside (Lazy Loading)** caching pattern for Node.js applications, what should the application do when updating data in the database?

- **A.** Update the cache only and never write to the database.
- **B.** Update the primary database first, then delete (invalidate) the corresponding key in Redis.
- **C.** Delete the database record and write directly to Redis.
- **D.** Reboot the Redis instance.

**Correct answer:** B

> **Why:** Updating the database and then deleting the cached key prevents race conditions and ensures subsequent read requests reload the latest data on demand.

---

### Question 44
Which memory eviction policy should you configure in Redis when using it as a general-purpose LRU cache where all keys are eligible for eviction when memory is full?

- **A.** `noeviction`
- **B.** `allkeys-lru`
- **C.** `volatile-ttl`
- **D.** `volatile-random`

**Correct answer:** B

> **Why:** `allkeys-lru` evicts the least recently used keys out of all stored keys when memory reaches `maxmemory`, making it ideal for caching architectures.

---

### Question 45
What is **Cache Stampede** (Thundering Herd problem) in Node.js web applications, and how can it be mitigated?

- **A.** When Redis runs out of disk space during snapshotting.
- **B.** When a high-traffic cache key expires, causing hundreds of concurrent Node.js requests to simultaneously hit the database; mitigated using distributed locks (`Redlock`), early probabilistic background refresh (XFetch), or mutexes.
- **C.** When Node.js crashes due to out-of-memory errors.
- **D.** When network cables are disconnected from the server.

**Correct answer:** B

> **Why:** Cache Stampede occurs when simultaneous cache misses overwhelm the origin database. Using distributed mutexes or probabilistic early recomputation ensures only one worker refreshes the cache.
