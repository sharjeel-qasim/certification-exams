# Redis for JavaScript Developers — Practice Question Bank

[![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)](https://redis.io/)
[![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org/)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Questions](https://img.shields.io/badge/Questions-45%20Verified%20MCQs-success?style=for-the-badge)](#table-of-contents)
[![Cheat Sheet](https://img.shields.io/badge/Study_Guide-Cheat_Sheet-orange?style=for-the-badge)](CHEAT_SHEET.md)

Complete Multiple Choice Question (MCQ) Practice Bank for the **Redis for JavaScript Developers** certification. Verified against Node.js (`node-redis` v4+) client design patterns, Streams, Geospatial indexing, and Redis Stack modules.

> ⚡ **Quick Review:** Check out the [**Redis for JavaScript Developers Cheat Sheet**](./CHEAT_SHEET.md) for a high-yield summary of `node-redis` v4 commands, data structures, RediSearch, and Streams before testing yourself below.

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** In `node-redis` v4+, `createClient()` only instantiates the client object; you must explicitly call `await client.connect()` to establish the TCP connection before executing commands. Option **A** is wrong because `node-redis` v4 uses native Promises rather than callbacks (which was v3 behavior). Option **C** is an anti-pattern that exhausts server sockets and adds TCP handshake overhead per request. Option **D** is wrong because `authSync()` does not exist—authentication credentials are passed in the `createClient()` configuration object or URL and handled asynchronously during connection.

</details>

---

### Question 2
What happens in a Node.js application if a `node-redis` client encounters a connection drop and no `'error'` event listener has been registered on the client?

- **A.** The client silently swallows the error and reconnects without logging.
- **B.** Node.js emits an unhandled `'error'` event that terminates the Node.js process.
- **C.** The operating system restarts the Redis server.
- **D.** The command automatically falls back to an in-memory Map.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Because the `node-redis` client extends Node.js `EventEmitter`, emitting an `'error'` event when no listener (`client.on('error', cb)`) is registered causes Node.js to throw an unhandled error exception and crash the process. Option **A** is wrong because `EventEmitter` never silently ignores unhandled `'error'` events. Option **C** is wrong because a client-side Node.js exception has no control over the external Redis server daemon. Option **D** is wrong because `node-redis` does not provide automatic fallback to a local JavaScript `Map`.

</details>

---

### Question 3
How should the `node-redis` client instance be managed across an Express.js web application?

- **A.** Create and connect a new client inside each route handler and call `client.disconnect()` when the response ends.
- **B.** Create a single shared client instance (Singleton), connect on application startup, and reuse it across all route handlers.
- **C.** Create a new client per active user session.
- **D.** Store the client instance in `localStorage`.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** A single `node-redis` client multiplexes commands asynchronously over one persistent TCP connection, so sharing a Singleton instance across the app maximizes throughput and avoids connection churn. Option **A** and Option **C** are wrong because creating connections per request or per user session adds heavy TCP/TLS handshake latency and can quickly hit Redis's `maxclients` limit. Option **D** is wrong because `localStorage` is a browser Web Storage API and does not exist on a Node.js backend server.

</details>

---

### Question 4
In `node-redis` v4+, what data type do all command methods return?

- **A.** Node.js style error-first callbacks `(err, result) => {}`
- **B.** Native JavaScript Promises (`Promise<T>`)
- **C.** Synchronous blocking values
- **D.** Observables

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `node-redis` v4+ is 100% Promise-based out of the box, returning a `Promise` from every command method for use with `async/await`. Option **A** is wrong because error-first callbacks were the default in `node-redis` v3 and are only supported in v4 if `legacyMode: true` is enabled. Option **C** is wrong because all Redis network I/O in Node.js is non-blocking and asynchronous. Option **D** is wrong because `node-redis` returns standard Promises, not RxJS `Observable` streams.

</details>

---

### Question 5
Which option in `createClient({ socket: { ... } })` configures a custom reconnection backoff strategy in `node-redis`?

- **A.** `retry_strategy` (in v3) / `reconnectStrategy` (in v4+)
- **B.** `auto_restart`
- **C.** `loopInterval`
- **D.** `reconnect_timer`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** In `node-redis` v4+, `socket.reconnectStrategy` (formerly `retry_strategy` in v3) accepts a function `(retries) => delayInMs | Error` to customize backoff delays or stop reconnecting. Options **B** (`auto_restart`), **C** (`loopInterval`), and **D** (`reconnect_timer`) are fabricated configuration properties that do not exist in the `node-redis` client API.

</details>

---

### Question 6
You need to set a key `'session:abc'` with value `'user_123'` that expires automatically in 3600 seconds (1 hour). What is the correct syntax in `node-redis` v4?

- **A.** `await client.set('session:abc', 'user_123', 'EX', 3600)`
- **B.** `await client.set('session:abc', 'user_123', { EX: 3600 })`
- **C.** `await client.setExpire('session:abc', 'user_123', 3600)`
- **D.** `await client.set('session:abc', 'user_123', 3600)`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `node-redis` v4 passes command modifiers like expiration and existence checks as a third options object (`{ EX: 3600 }`). Option **A** is wrong because positional string arguments (`'EX', 3600`) were used in `node-redis` v3 / `ioredis`, not `node-redis` v4's native API. Option **C** is wrong because `setExpire` is not a valid method (the legacy dedicated command is `setEx(key, seconds, value)`). Option **D** is wrong because passing a raw number as the third argument does not match the v4 options object signature.

</details>

---

### Question 7
What does `await client.hGetAll('non_existent_key')` return in `node-redis` v4 when the requested key does not exist?

- **A.** `null`
- **B.** `undefined`
- **C.** An empty JavaScript object `{}`
- **D.** Throws a `KeyNotFoundError`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** In Redis, `HGETALL` on a non-existent key returns an empty list, which `node-redis` v4 transforms into an empty JavaScript object `{}` (`Object.create(null)`). Because `{}` is truthy in JavaScript, developers must check `Object.keys(res).length === 0`. Options **A** and **B** are wrong because `hGetAll` returns `{}` rather than `null` (which `get` returns for missing strings) or `undefined`. Option **D** is wrong because Redis does not throw an error when querying a missing key.

</details>

---

### Question 8
Which method should be called to gracefully drain pending commands and close the Redis connection when shutting down a Node.js server?

- **A.** `client.destroy()`
- **B.** `client.quit()` / `client.disconnect()`
- **C.** `client.kill()`
- **D.** `client.close()`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `await client.quit()` gracefully waits for all queued in-flight commands to complete before sending the `QUIT` command and closing the socket (while `client.disconnect()` forcefully closes the connection immediately). Options **A** (`destroy()`), **C** (`kill()`), and **D** (`close()`) are not valid connection lifecycle methods on the `node-redis` v4 client instance.

</details>

---

## Domain 2: Data Structures & Key Design Patterns in JavaScript

### Question 9
In a solar energy monitoring application, each solar site has properties like `name`, `capacityKwh`, `installedYear`, and `status`. Which Redis data structure is most appropriate to store each site as a single record without JSON parsing overhead?

- **A.** Redis String
- **B.** Redis Hash
- **C.** Redis List
- **D.** Redis Bitmap

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** A Redis Hash maps field names to values inside a single key, allowing individual properties (e.g., `capacityKwh`) to be read or updated via `HGET`/`HSET`/`HINCRBYFLOAT` without serializing or deserializing the entire object. Option **A** is wrong because storing a flat object in a String requires JSON serialization/deserialization on every read and write. Option **C** is wrong because Lists store ordered sequences of strings, not named key-value attributes. Option **D** is wrong because Bitmaps store bit-level boolean flags, not structured entity fields.

</details>

---

### Question 10
You need to store solar site metadata using key namespacing best practices in Redis. Which key naming convention follows recommended Redis conventions?

- **A.** `sites-9001-info`
- **B.** `sites:9001:info`
- **C.** `SELECT * FROM sites WHERE id = 9001`
- **D.** `site9001`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Redis community convention uses colons (`:`) to delimit hierarchical key namespaces (`<entity>:<id>:<attribute>`), which tools like RedisInsight automatically parse into collapsible folder trees. Option **A** uses hyphens, which can collide with UUIDs or slugs and aren't recognized as standard namespace delimiters by default. Option **C** is a SQL query, not a Redis key name. Option **D** lacks any delimiter or attribute descriptor, making keys hard to organize or scan by pattern.

</details>

---

### Question 11
You want to atomically increment a site's daily generated kilowatt-hours field (`generatedKwh`) by `15.5` in a Redis Hash (`site:100`). Which command should you use?

- **A.** `HINCRBY site:100 generatedKwh 15.5`
- **B.** `HINCRBYFLOAT site:100 generatedKwh 15.5`
- **C.** `HSET site:100 generatedKwh 15.5`
- **D.** `INCRBY site:100.generatedKwh 15.5`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `HINCRBYFLOAT` atomically increments a Hash field by a floating-point number (`15.5`). Option **A** is wrong because `HINCRBY` only accepts 64-bit signed integers and throws `ERR value is not an integer or out of range` for `15.5`. Option **C** is wrong because `HSET` overwrites the field value with `15.5` instead of incrementing it. Option **D** is wrong because `INCRBY` operates on top-level String keys with integer increments, not Hash fields or floats.

</details>

---

### Question 12
Which Redis data structure guarantees that all members are **unique** and provides mathematical operations like union, intersection, and difference?

- **A.** List
- **B.** Set
- **C.** String
- **D.** Stream

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Redis Sets store unordered collections of unique strings and natively support set operations such as `SUNION`, `SINTER`, and `SDIFF` alongside $O(1)$ membership checks (`SISMEMBER`). Option **A** is wrong because Lists allow duplicate elements and do not offer set algebra commands. Option **C** is wrong because a String holds a single scalar value. Option **D** is wrong because a Stream is an append-only log of timestamped events, not a mathematical set of unique members.

</details>

---

### Question 13
You are building a real-time leaderboard in Node.js ranking solar farms by their current power output. Which Redis data structure should you use?

- **A.** List
- **B.** Set
- **C.** Sorted Set (ZSet)
- **D.** Hash

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** Sorted Sets (`ZSet`) pair each unique member with a floating-point score and automatically keep members ordered by score in $O(\log N)$ time, making real-time rank and top-$K$ queries effortless. Option **A** is wrong because Lists are ordered by insertion position rather than dynamic numeric scores and allow duplicates. Option **B** is wrong because Sets are unordered and have no scores. Option **D** is wrong because Hashes map fields to values without maintaining any sorted order across fields.

</details>

---

### Question 14
How do you retrieve the top 10 highest-ranked sites with their scores using `node-redis` v4?

- **A.** `await client.zRangeWithScores('leaderboard', 0, 9, { REV: true })`
- **B.** `await client.zGetTop('leaderboard', 10)`
- **C.** `await client.zRange('leaderboard', 0, 10)`
- **D.** `await client.sort('leaderboard', 'DESC')`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** `client.zRangeWithScores('leaderboard', 0, 9, { REV: true })` returns an array of `{ value, score }` objects for indices `0` through `9` (inclusive, totaling 10 items) in descending score order (`REV: true`). Option **B** is wrong because `zGetTop` is not a valid `node-redis` method. Option **C** is wrong because `0, 10` fetches 11 items (stop index is inclusive), omits scores, and sorts in ascending (lowest-first) order. Option **D** is wrong because `SORT` does not return `ZSet` scores in `{ value, score }` format and has invalid argument syntax here.

</details>

---

### Question 15
An application needs to track unique daily website visitors across millions of users while keeping memory usage strictly under 15 KB per day. Which data structure should you use?

- **A.** Set
- **B.** List
- **C.** HyperLogLog
- **D.** Hash

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** HyperLogLog (`PFADD` / `PFCOUNT`) probabilistically estimates the cardinality (unique count) of huge datasets with ~0.81% standard error while using at most 12 KB of memory per key. Option **A** (Set) and Option **D** (Hash) are wrong because storing millions of distinct user IDs requires tens of megabytes of RAM, far exceeding the 15 KB limit. Option **B** (List) is wrong because it neither deduplicates visitors nor stays within 15 KB for millions of entries.

</details>

---

### Question 16
You need to record whether each user in a system with 1,000,000 users logged in today, using the minimum possible memory footprint. Which data structure should you use?

- **A.** Bitmap (`SETBIT` / `BITCOUNT`)
- **B.** Sorted Set
- **C.** Stream
- **D.** List

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** A Redis Bitmap stores 1 bit per integer offset (user ID), meaning 1,000,000 users require only $1,000,000 / 8 \approx 122\text{ KB}$ of memory and support fast $O(N)$ population counts via `BITCOUNT`. Options **B** (Sorted Set), **C** (Stream), and **D** (List) store full member/entry payloads plus structural pointers per user, consuming tens of megabytes for 1,000,000 records.

</details>

---

### Question 17
Which Redis command implements a blocking FIFO queue pop in Node.js worker processes?

- **A.** `LPOP`
- **B.** `RPOP`
- **C.** `BRPOP` / `BLPOP`
- **D.** `GET`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** `BRPOP` and `BLPOP` are the blocking variants of `RPOP` and `LPOP`; when a queue list is empty, they block the connection until an item is pushed or a timeout expires, eliminating wasteful polling loops. Options **A** (`LPOP`) and **B** (`RPOP`) are non-blocking and return `null` immediately if the list is empty. Option **D** (`GET`) reads a String value and does not pop from a List or block.

</details>

---

### Question 18
What is the time complexity of adding an element to the head of a Redis List using `LPUSH`?

- **A.** $O(N)$
- **B.** $O(1)$
- **C.** $O(\log N)$
- **D.** $O(N^2)$

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Redis Lists are implemented as doubly-linked quicklists of packed listpacks, so pushing a single element to the head (`LPUSH`) or tail (`RPUSH`) always executes in $O(1)$ constant time regardless of list length. Option **A** ($O(N)$) applies to index-based access like `LINDEX` or `LREM`, not head/tail pushes. Option **C** ($O(\log N)$) applies to Sorted Set operations (`ZADD`). Option **D** ($O(N^2)$) is not the complexity of any Redis List insertion.

</details>

---

## Domain 3: Geospatial Indexing & Search

### Question 19
Under the hood, which Redis data structure powers Redis Geospatial commands (`GEOADD`, `GEODIST`, `GEOSEARCH`)?

- **A.** Hashes
- **B.** Sorted Sets (ZSets)
- **C.** Streams
- **D.** Bitmaps

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Redis stores geospatial items inside a standard Sorted Set (`ZSet`), encoding each location's longitude and latitude into a 52-bit Geohash integer stored as the member's score (which is why `ZREM` deletes geo members). Options **A** (Hashes), **C** (Streams), and **D** (Bitmaps) do not maintain numeric score ordering required for Geohash range scans.

</details>

---

### Question 20
What is the correct order of coordinate arguments when invoking `GEOADD` in Redis and `node-redis`?

- **A.** Latitude, Longitude, Member
- **B.** Longitude, Latitude, Member
- **C.** Member, Latitude, Longitude
- **D.** Latitude, Member, Longitude

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Redis Geospatial commands strictly take `(x, y)` Cartesian order: **Longitude first**, **Latitude second**, and **Member third** (`GEOADD key longitude latitude member`). Options **A**, **C**, and **D** place latitude or member in the wrong position, which either causes a coordinate range error (if longitude > 85.05° is passed as latitude) or indexes the point at the swapped coordinates on Earth.

</details>

---

### Question 21
You need to find all solar sites located within a 50 km radius of San Francisco coordinates `(-122.4194, 37.7749)`. Which modern Redis command should you use?

- **A.** `GEOSEARCH`
- **B.** `GEOPOS`
- **C.** `GEODEL`
- **D.** `GEOSCAN`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** `GEOSEARCH` (added in Redis 6.2 to replace the deprecated `GEORADIUS` command) queries a geospatial index for members inside a circular radius (`BYRADIUS`) or rectangular box (`BYBOX`). Option **B** (`GEOPOS`) only returns the stored coordinates of specific named members rather than searching by radius. Options **C** (`GEODEL`) and **D** (`GEOSCAN`) are non-existent Redis commands (use `ZREM` and `ZSCAN` on the underlying Sorted Set instead).

</details>

---

### Question 22
How do you invoke `GEOSEARCH` using `node-redis` v4?

- **A.** `await client.geoSearch('sites:geo', { longitude: -122.41, latitude: 37.77 }, { radius: 50, unit: 'km' })`
- **B.** `await client.geoRadius('sites:geo', -122.41, 37.77, 50, 'km')`
- **C.** `await client.geoFind('sites:geo', 50, 'km')`
- **D.** `await client.findNearby('sites:geo', -122.41, 37.77)`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** In `node-redis` v4, `client.geoSearch(key, from, by, options)` takes the key, an origin (`{ longitude, latitude }` or member name), and a search shape (`{ radius, unit }` or `{ width, height, unit }`). Option **B** uses the deprecated `GEORADIUS` command with v3-style positional arguments. Options **C** (`geoFind`) and **D** (`findNearby`) are non-existent methods in `node-redis`.

</details>

---

### Question 23
What unit options are supported by Redis Geospatial distance queries?

- **A.** `m` (meters), `km` (kilometers), `mi` (miles), `ft` (feet)
- **B.** `km` and `miles` only
- **C.** `degrees` and `radians`
- **D.** `pixels` and `inches`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Redis Geospatial commands (`GEODIST`, `GEOSEARCH`, `GEOSEARCHSTORE`) exclusively support four unit abbreviations: `m` (meters), `km` (kilometers), `mi` (miles), and `ft` (feet). Option **B** is wrong because `m` and `ft` are also supported and miles is abbreviated `mi`, not `miles`. Options **C** and **D** list unsupported angular or screen/imperial units that cause a syntax error in Redis.

</details>

---

### Question 24
What is the valid latitude range supported by Redis Geospatial indexing?

- **A.** -90.0 to +90.0 degrees
- **B.** -85.05112878 to +85.05112878 degrees (Web Mercator projection limit)
- **C.** -180.0 to +180.0 degrees
- **D.** 0.0 to 360.0 degrees

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Redis uses the EPSG:900913 / EPSG:3857 Web Mercator projection to compute 52-bit Geohashes, which restricts indexable latitudes to **-85.05112878° to +85.05112878°** (trying to index polar latitudes closer to ±90° throws an error). Option **A** is the geographic pole range, which Web Mercator cannot project. Option **C** (-180° to +180°) is the valid range for **longitude**, not latitude. Option **D** is an invalid coordinate range for both latitude and longitude in Redis.

</details>

---

## Domain 4: Redis Streams & Event Streaming

### Question 25
Which Redis command is used to append a new event entry to a Redis Stream?

- **A.** `LPUSH`
- **B.** `XADD`
- **C.** `APPEND`
- **D.** `PUBLISH`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `XADD` appends a new entry of field-value pairs to a Redis Stream and returns its unique entry ID. Option **A** (`LPUSH`) prepends elements to a Redis List, not a Stream. Option **C** (`APPEND`) concatenates bytes to the end of a Redis String. Option **D** (`PUBLISH`) broadcasts an ephemeral message to a Pub/Sub channel without storing it in a Stream.

</details>

---

### Question 26
When appending events to a stream using `client.xAdd('mystream', '*', fields)`, what does the `'*'` argument signify?

- **A.** Broadcast the message to all channels.
- **B.** Instruct Redis to automatically generate the entry ID based on current Unix millisecond timestamp and sequence number.
- **C.** Match all wildcards.
- **D.** Delete all previous entries in the stream.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Passing `'*'` as the ID parameter in `XADD` tells the Redis server to auto-generate a monotonically increasing ID in the format `<millisecondsTime>-<sequenceNumber>` (e.g., `1693526400000-0`). Options **A**, **C**, and **D** confuse `'*'` in `XADD` with Pub/Sub pattern wildcards (`PSUBSCRIBE`), `KEYS *` glob matching, or stream trimming.

</details>

---

### Question 27
To prevent a Redis Stream from growing indefinitely in memory, how can you cap the stream to approximately 10,000 entries efficiently?

- **A.** Run a daily cron job that deletes the stream.
- **B.** Use `XADD mystream MAXLEN ~ 10000 * field value`.
- **C.** Set a TTL on each message.
- **D.** Manually execute `LTRIM`.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Passing `MAXLEN ~ 10000` (with the approximate `~` modifier) during `XADD` caps the stream at roughly 10,000 entries in $O(1)$ amortized cost by evicting only whole macro-nodes in the underlying radix tree. Option **A** is wrong because deleting the entire stream loses all recent unprocessed events and consumer group state. Option **C** is wrong because Redis does not support per-entry TTLs inside a Stream (though `MINID` can trim by timestamp). Option **D** is wrong because `LTRIM` only works on Redis Lists (`XTRIM` is the stream command).

</details>

---

### Question 28
What is the purpose of a **Consumer Group** in Redis Streams?

- **A.** To encrypt messages before transmission.
- **B.** To allow multiple consumer worker instances to cooperate by distributing messages so each message is processed by only one consumer in the group.
- **C.** To convert stream messages into PDF documents.
- **D.** To group users by geographical region.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** A Redis Streams Consumer Group (`XGROUP CREATE`) partitions stream entries across multiple named consumers in the group for horizontal scaling and tracks each consumer's unacknowledged messages in a Pending Entries List (PEL). Options **A**, **C**, and **D** are unrelated to Redis Streams; Consumer Groups do not perform encryption, file format conversion, or geospatial user grouping.

</details>

---

### Question 29
Which command does a worker in a consumer group execute to fetch **new, undelivered** messages from a stream?

- **A.** `XREADGROUP GROUP mygroup worker1 STREAMS mystream >`
- **B.** `XREADGROUP GROUP mygroup worker1 STREAMS mystream 0`
- **C.** `XPOP mystream`
- **D.** `RPOP mystream`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** In `XREADGROUP`, specifying the special ID `>` requests only new messages that have never been delivered to any consumer in `mygroup`. Option **B** is wrong because passing ID `0` (or `0-0`) returns previously delivered messages that are still pending (`PEL`) for `worker1` rather than new messages. Option **C** is wrong because `XPOP` does not exist in Redis. Option **D** is wrong because `RPOP` pops from a Redis List, not a Stream.

</details>

---

### Question 30
What must a worker process do after successfully processing a stream message read from a consumer group?

- **A.** Call `client.xDel()`
- **B.** Send an acknowledgment using `client.xAck('stream', 'group', messageId)`
- **C.** Restart the Node.js server
- **D.** Call `client.save()`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Calling `client.xAck(streamKey, groupName, messageId)` (`XACK`) removes the entry from the consumer group's Pending Entries List (PEL) so Redis knows processing succeeded. Option **A** is wrong because `XDEL` physically deletes the message from the stream for all consumer groups without clearing the PEL entry. Option **C** is wrong because restarting the server is unnecessary and disruptive. Option **D** is wrong because `SAVE` performs a synchronous RDB disk snapshot and has nothing to do with stream acknowledgments.

</details>

---

### Question 31
What happens to messages that have been delivered to a worker via `XREADGROUP` but have **not** yet been acknowledged with `XACK`?

- **A.** They are immediately deleted from the stream.
- **B.** They remain recorded in the Pending Entries List (PEL) and can be inspected via `XPENDING` or claimed by another worker using `XCLAIM` / `XAUTOCLAIM`.
- **C.** They are returned to the sender.
- **D.** They trigger an immediate Redis crash.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Every message delivered via `XREADGROUP` is tracked in the group's Pending Entries List (PEL) with its consumer name, delivery timestamp, and delivery count until `XACK` is called; if a worker fails, another worker can inspect pending messages with `XPENDING` and take ownership via `XCLAIM` or `XAUTOCLAIM`. Option **A** is wrong because stream messages persist until explicitly trimmed or deleted. Options **C** and **D** are wrong because Redis neither bounces unacknowledged entries back to producers nor crashes.

</details>

---

### Question 32
How can you implement a **Sliding Window Rate Limiter** (e.g. maximum 10 requests per minute per IP) in Node.js using Redis?

- **A.** Store each request timestamp as both score and member in a Sorted Set, remove timestamps older than 60 seconds (`ZREMRANGEBYSCORE`), count elements (`ZCARD`), and allow the request if count < 10.
- **B.** Use a single string key with `INCR` without expiration.
- **C.** Append IP addresses to a List.
- **D.** Run an asynchronous `setTimeout()` in Node.js memory.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Using a Sorted Set where each request's Unix timestamp is the score allows atomic pruning of expired timestamps outside the rolling 60-second window (`ZREMRANGEBYSCORE`) and counting remaining active requests (`ZCARD`). Option **B** is wrong because `INCR` without expiration permanently blocks users after 10 lifetime requests (and even with a TTL, implements a fixed-window counter rather than a true sliding window). Option **C** is wrong because Lists cannot efficiently prune entries by timestamp range. Option **D** is wrong because in-memory Node.js timers are not shared across multiple server instances and are lost on restart.

</details>

---

## Domain 5: Transactions, Concurrency & Pub/Sub in Node.js

### Question 33
What is the primary difference between standard **Pipelining** and a **Transaction** (`MULTI`/`EXEC`) in Redis?

- **A.** Pipelining sends multiple commands in a batch to save network roundtrips without transactional isolation; `MULTI`/`EXEC` guarantees that all commands execute sequentially and atomically without interference from other clients.
- **B.** Pipelining only works with Strings.
- **C.** Transactions do not work in Node.js.
- **D.** Pipelining requires root server privileges.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Pipelining is purely a network optimization that sends multiple commands in one TCP write without waiting for individual replies, meaning commands from other clients can interleave on the server; `MULTI`/`EXEC` queues commands on the server and executes the entire block atomically without interleaving. Option **B** is wrong because pipelining works with any Redis command and data structure. Option **C** is wrong because `node-redis` supports transactions via `client.multi()`. Option **D** is wrong because pipelining is a standard client protocol technique requiring no special OS or Redis privileges.

</details>

---

### Question 34
How is **Optimistic Concurrency Control** implemented in Redis to prevent race conditions during read-modify-write operations?

- **A.** `LOCK` and `UNLOCK` commands
- **B.** Using `WATCH key`, checking values, queuing modifications in `MULTI`, and executing with `EXEC` (which returns `null` if the watched key changed)
- **C.** Stopping the Redis event loop
- **D.** Disabling all other client connections

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `WATCH` implements optimistic locking (CAS — check-and-set) by monitoring one or more keys before `MULTI`; if another client modifies any watched key before `EXEC`, the entire transaction aborts and `EXEC` returns `null`. Option **A** is wrong because Redis has no built-in `LOCK`/`UNLOCK` commands (pessimistic locking instead uses `SET key token NX PX ms`). Options **C** and **D** are wrong because you neither stop the Redis event loop nor disconnect other clients to perform a safe read-modify-write.

</details>

---

### Question 35
You are building a Pub/Sub event subscriber in a Node.js microservice. Why must you create a separate client using **`client.duplicate()`** for the subscriber?

- **A.** Because Redis only allows one subscription per operating system.
- **B.** Because once a client enters subscriber mode (`SUBSCRIBE`), it is dedicated to listening for messages and cannot execute regular data commands (`GET`, `SET`).
- **C.** To double the bandwidth of the connection.
- **D.** Because Node.js does not support asynchronous networking.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** When a Redis connection issues `SUBSCRIBE` or `PSUBSCRIBE`, the protocol state changes to subscriber mode where the connection can only receive pushed messages or run Pub/Sub commands (`UNSUBSCRIBE`, `PING`, `RESET`, `QUIT`), so `node-redis` requires a dedicated duplicated connection (`client.duplicate()`). Option **A** is wrong because a single client or OS can subscribe to many channels. Option **C** is wrong because `duplicate()` is for protocol state separation, not bandwidth bonding. Option **D** is wrong because Node.js is fundamentally built on asynchronous non-blocking networking.

</details>

---

### Question 36
How does Redis Pub/Sub handle message delivery when a subscriber client is offline or disconnected when a message is published?

- **A.** Messages are saved on disk and replayed when the subscriber reconnects.
- **B.** Pub/Sub is **fire-and-forget**; messages sent while a subscriber is disconnected are lost permanently.
- **C.** Messages are automatically redirected to email.
- **D.** Redis pauses all publishers until the subscriber reconnects.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Redis Pub/Sub is an ephemeral, fire-and-forget messaging system (`at-most-once` delivery): `PUBLISH` immediately pushes the message to currently connected subscribers and discards it, so offline subscribers miss the message forever (use Redis Streams if durability and replay are needed). Option **A** describes Redis Streams, not Pub/Sub. Option **C** is wrong because Redis has no email integration. Option **D** is wrong because `PUBLISH` never blocks waiting for offline subscribers.

</details>

---

### Question 37
What is the purpose of the `UNWATCH` command in Redis?

- **A.** To clear all keys currently monitored by `WATCH` on the current client connection.
- **B.** To delete the Redis database.
- **C.** To disconnect all subscribers from a channel.
- **D.** To reset user passwords.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** `UNWATCH` cancels optimistic monitoring of all previously `WATCH`ed keys on the current connection (useful when a client reads a watched key and decides not to run `MULTI`/`EXEC`). Option **B** is wrong because `FLUSHDB` / `FLUSHALL` delete database keys, not `UNWATCH`. Option **C** is wrong because `UNSUBSCRIBE` removes channel subscriptions. Option **D** is wrong because `ACL SETUSER` manages user passwords.

</details>

---

### Question 38
In `node-redis` v4+, how do you execute a transactional batch of commands?

- **A.** `const results = await client.multi().set('k', 'v').incr('counter').exec();`
- **B.** `await client.transaction(['SET k v', 'INCR counter'])`
- **C.** `await client.begin(); await client.commit();`
- **D.** `client.execSync()`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** In `node-redis` v4, calling `client.multi()` creates a transaction command queue on which you chain commands (`.set(...)`, `.incr(...)`) and finally call `await .exec()` to send `MULTI`, the queued commands, and `EXEC` to Redis. Options **B** (`client.transaction()`), **C** (`begin()` / `commit()`, which are SQL idioms), and **D** (`execSync()`) are not valid methods in `node-redis`.

</details>

---

### Question 39
If a Redis transaction (`MULTI`/`EXEC`) contains a command that causes a runtime data error (e.g. calling `INCR` on a string that contains letters), how does Redis behave?

- **A.** Redis rolls back all previous commands in the transaction.
- **B.** Redis executes all other commands in the transaction; only the faulty command fails.
- **C.** The entire database is cleared.
- **D.** The Redis server shuts down.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** By design, Redis does not support transaction rollbacks on runtime type/value errors in order to keep the server fast and simple—every valid command in the `MULTI`/`EXEC` block still runs, and the returned results array contains an error entry only for the failed command. (Note: syntax errors caught while queuing before `EXEC` *will* abort the whole transaction via `EXECABORT`.) Option **A** is a common misconception from SQL databases. Options **C** and **D** are wrong because runtime command errors never wipe data or crash the server.

</details>

---

## Domain 6: RedisJSON, RediSearch & Caching Architecture

### Question 40
Which Redis Stack module allows storing, querying, and mutating nested JSON documents natively in-memory?

- **A.** RedisBloom
- **B.** RedisJSON
- **C.** RedisGraph
- **D.** RedisRaft

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **RedisJSON** (`JSON.SET`, `JSON.GET`, `JSON.NUMINCRBY`, etc.) stores JSON documents as binary tree structures in memory, allowing direct JSONPath access and mutation of nested fields without pulling the full document into Node.js. Option **A** (`RedisBloom`) provides probabilistic data structures (Bloom, Cuckoo, Count-Min Sketch, Top-K). Option **C** (`RedisGraph`, now EOL) was for property graphs using Cypher. Option **D** (`RedisRaft`) is an experimental consensus module, not a JSON document store.

</details>

---

### Question 41
Using RedisJSON, how do you atomically increment a numeric property `$.stats.views` inside a JSON document `user:100`?

- **A.** `JSON.NUMINCRBY user:100 $.stats.views 1`
- **B.** `INCR user:100.stats.views`
- **C.** `JSON.SET user:100 $.stats.views 1`
- **D.** `HINCRBY user:100 stats.views 1`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** `JSON.NUMINCRBY` (`client.json.numIncrBy('user:100', '$.stats.views', 1)` in `node-redis`) atomically adds the specified number to the numeric value at the given JSONPath inside a RedisJSON document. Option **B** is wrong because `INCR` operates on a top-level String key named `"user:100.stats.views"`, not inside the `user:100` JSON document. Option **C** is wrong because `JSON.SET` overwrites `$.stats.views` to `1` rather than incrementing it. Option **D** is wrong because `HINCRBY` only works on Redis Hashes and fails with a `WRONGTYPE` error on a RedisJSON key.

</details>

---

### Question 42
When creating a secondary search index with RediSearch (`FT.CREATE`), which field type is best suited for exact-match categorical values such as status codes (`active`, `pending`) or GUIDs?

- **A.** `TEXT`
- **B.** `TAG`
- **C.** `NUMERIC`
- **D.** `GEO`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `TAG` fields store compact, un-stemmed strings separated by a configurable delimiter (default `,`) and are optimized for exact-match categorical filtering (`@status:{active | pending}`) and exact ID/GUID lookups. Option **A** (`TEXT`) tokenizes, stems, and scores words for full-text human-language search, which splits GUIDs on hyphens and adds unnecessary overhead. Option **C** (`NUMERIC`) is only for numbers and numeric range queries. Option **D** (`GEO`) is only for longitude/latitude coordinate pairs.

</details>

---

### Question 43
In the **Cache-Aside (Lazy Loading)** caching pattern for Node.js applications, what should the application do when updating data in the database?

- **A.** Update the cache only and never write to the database.
- **B.** Update the primary database first, then delete (invalidate) the corresponding key in Redis.
- **C.** Delete the database record and write directly to Redis.
- **D.** Reboot the Redis instance.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** In the Cache-Aside pattern, writes go to the system-of-record database first and then invalidate (`DEL`) the cached key in Redis so the next read lazy-loads fresh data—avoiding stale cache anomalies and write-write race conditions. Option **A** and Option **C** are wrong because Redis is acting as a cache, not the primary persistent database, so skipping or deleting the database record causes permanent data loss when keys expire or evict. Option **D** is wrong because rebooting Redis wipes all cached keys and disrupts all active clients.

</details>

---

### Question 44
Which memory eviction policy should you configure in Redis when using it as a general-purpose LRU cache where all keys are eligible for eviction when memory is full?

- **A.** `noeviction`
- **B.** `allkeys-lru`
- **C.** `volatile-ttl`
- **D.** `volatile-random`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** `allkeys-lru` evicts the least-recently-used keys across the **entire** keyspace whenever `maxmemory` is reached, making it the standard policy for a general-purpose LRU cache. Option **A** (`noeviction`) never evicts keys and instead returns `OOM` write errors once memory is full. Options **C** (`volatile-ttl`) and **D** (`volatile-random`) only evict keys that have an explicit TTL (`EXPIRE`) set, leaving any key without a TTL un-evictable, and do not use LRU ordering.

</details>

---

### Question 45
What is **Cache Stampede** (Thundering Herd problem) in Node.js web applications, and how can it be mitigated?

- **A.** When Redis runs out of disk space during snapshotting.
- **B.** When a high-traffic cache key expires, causing hundreds of concurrent Node.js requests to simultaneously hit the database; mitigated using distributed locks (`Redlock`), early probabilistic background refresh (XFetch), or mutexes.
- **C.** When Node.js crashes due to out-of-memory errors.
- **D.** When network cables are disconnected from the server.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** A Cache Stampede happens when a popular cached key expires and many concurrent requests experience a cache miss at the exact same moment, all querying and recomputing from the primary database simultaneously; it is prevented with request coalescing/mutex locks (so only one worker rebuilds the cache) or probabilistic early expiration. Option **A** describes an RDB persistence disk issue, not a cache stampede. Option **C** describes a Node.js V8 heap exhaustion crash. Option **D** describes a physical network outage.

</details>
