# ⚡ Redis for JavaScript Developers (RU102JS) — Last-Minute Cram & Cheat Sheet

[![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)](https://redis.io/)
[![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org/)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Exam](https://img.shields.io/badge/Certification-RU102JS%20Redis%20for%20JavaScript-red?style=for-the-badge)](#-high-frequency-exam-topics)

High-yield quick-reference cheat sheet for **Redis for JavaScript Developers (RU102JS)**. Covers official `node-redis` (v4+) client syntax, Promises/async-await, native data structures, Redis Stack (RedisJSON, RediSearch, TimeSeries), Streams, Pub/Sub, transactions, and Node.js caching patterns.

---

## 🔴 1. Official `node-redis` (v4+) Client Lifecycle

```javascript
import { createClient } from 'redis';

// 1. Create client instance (singleton pattern)
const client = createClient({
  url: process.env.REDIS_URL || 'redis://localhost:6379',
  socket: {
    connectTimeout: 5000,
    keepAlive: 60000,
    reconnectStrategy: (retries) => Math.min(retries * 50, 2000)
  }
});

// 2. Attach error event listener (CRITICAL: prevents uncaught exception crashes)
client.on('error', (err) => console.error('Redis Client Error:', err));

// 3. Connect asynchronously before serving traffic
await client.connect();
```

> [!IMPORTANT]
> - `node-redis` v4+ is **100% Promise-based**. All commands return Native Promises (`await client.get('key')`).
> - In `node-redis` v4+, command names use **camelCase** (e.g. `client.hGetAll()`, `client.zRangeWithScores()`, `client.xAdd()`).

---

## 🔴 2. Data Structures & `node-redis` Command Methods

| Data Structure | CLI Command | `node-redis` (v4+) Method | Example Usage |
| :--- | :--- | :--- | :--- |
| **String** | `SET key val EX 3600` | `client.set(k, v, { EX: 3600 })` | `await client.set('user:session:1', token, { EX: 86400 })` |
| **String** | `GET key` | `client.get(k)` | `const val = await client.get('user:session:1')` |
| **String** | `INCR key` | `client.incr(k)` | `const hits = await client.incr('page:views')` |
| **Hash** | `HSET key f v [f2 v2]` | `client.hSet(k, obj / f, v)` | `await client.hSet('site:100', { name: 'SolarFarm A', capacity: 50 })` |
| **Hash** | `HGETALL key` | `client.hGetAll(k)` | `const site = await client.hGetAll('site:100')` (returns JS object) |
| **Hash** | `HINCRBY key f num` | `client.hIncrBy(k, f, num)` | `await client.hIncrBy('site:100', 'generatedKwh', 25)` |
| **Set** | `SADD key m1 m2` | `client.sAdd(k, [m1, m2])` | `await client.sAdd('sites:active', ['100', '101', '102'])` |
| **Set** | `SMEMBERS key` | `client.sMembers(k)` | `const activeSites = await client.sMembers('sites:active')` |
| **Set** | `SISMEMBER key m` | `client.sIsMember(k, m)` | `const exists = await client.sIsMember('sites:active', '100')` |
| **Sorted Set** | `ZADD key score m` | `client.zAdd(k, { score, value })`| `await client.zAdd('leaderboard', [{ score: 95.5, value: 'site:100' }])` |
| **Sorted Set** | `ZRANGE key 0 -1 WITHSCORES` | `client.zRangeWithScores(k, 0, -1)`| `const top = await client.zRangeWithScores('leaderboard', 0, 9, { REV: true })` |
| **List** | `LPUSH` / `RPOP` | `client.lPush(k, v)` / `rPop(k)` | `await client.lPush('queue:tasks', JSON.stringify(task))` |
| **Geospatial** | `GEOADD key lon lat m` | `client.geoAdd(k, { longitude, latitude, member })` | `await client.geoAdd('sites:geo', { longitude: -122.41, latitude: 37.77, member: '100' })` |
| **Geospatial** | `GEOSEARCH` | `client.geoSearch(k, from, by)` | `await client.geoSearch('sites:geo', { longitude: -122.4, latitude: 37.7 }, { radius: 50, unit: 'km' })` |

---

## 🔴 3. Redis Streams & Consumer Groups in Node.js

```javascript
// 1. Produce event to a Stream (XADD)
const eventId = await client.xAdd(
  'stream:meterReadings',
  '*', // Auto-generate timestamp ID
  { siteId: '100', kwh: '42.5', timestamp: Date.now().toString() },
  { TRIM: { strategy: 'MAXLEN', threshold: 10000, strategyModifier: '~' } } // Efficient capping
);

// 2. Create Consumer Group (idempotent setup)
try {
  await client.xGroupCreate('stream:meterReadings', 'analytics-group', '$', { MKSTREAM: true });
} catch (err) {
  if (!err.message.includes('BUSYGROUP')) throw err;
}

// 3. Consume events in a worker loop (XREADGROUP)
const response = await client.xReadGroup(
  'analytics-group',
  'worker-1',
  { key: 'stream:meterReadings', id: '>' }, // '>' means new undelivered messages
  { COUNT: 10, BLOCK: 2000 }
);

// 4. Acknowledge processed message (XACK)
await client.xAck('stream:meterReadings', 'analytics-group', messageId);
```

---

## 🔴 4. Transactions, Pipelining & Optimistic Concurrency

### Pipelining & Multi (`client.multi()`)
```javascript
// Executes multiple commands in a single network round-trip
const [res1, res2, res3] = await client.multi()
  .set('key1', 'val1')
  .hSet('hash:1', { a: '1', b: '2' })
  .incr('counter')
  .exec();
```

### Optimistic Concurrency (WATCH / MULTI / EXEC)
```javascript
let committed = null;
while (!committed) {
  await client.watch('inventory:item:42');
  const stock = parseInt(await client.get('inventory:item:42') || '0', 10);
  
  if (stock <= 0) {
    await client.unwatch();
    throw new Error('Out of stock');
  }

  // Multi queues commands; exec() returns null if another client modified 'inventory:item:42'
  committed = await client.multi()
    .decr('inventory:item:42')
    .sAdd('orders:processed', orderId)
    .exec();
}
```

---

## 🔴 5. Pub/Sub in Node.js (`client.duplicate()`)

> [!WARNING]
> When a client enters subscriber mode, it can **only** issue subscribe/unsubscribe commands.
> Always call **`client.duplicate()`** to create a dedicated subscriber instance.

```javascript
const subscriber = client.duplicate();
await subscriber.connect();

// Subscribe to channel
await subscriber.subscribe('alerts:critical', (message, channel) => {
  console.log(`Received alert on ${channel}: ${message}`);
});

// Publisher uses standard client
await client.publish('alerts:critical', JSON.stringify({ siteId: 100, alert: 'High Temp' }));
```

---

## 🔴 6. RedisJSON & RediSearch in `node-redis`

```javascript
// RedisJSON
await client.json.set('user:100', '$', {
  name: 'Sharjeel',
  role: 'Architect',
  skills: ['Node.js', 'Redis', '.NET']
});

// JSON.GET with JSONPath
const skills = await client.json.get('user:100', { path: '$.skills[*]' });

// RediSearch Index Creation
await client.ft.create('idx:users', {
  '$.name': { type: 'TEXT', AS: 'name' },
  '$.role': { type: 'TAG', AS: 'role' }
}, {
  ON: 'JSON',
  PREFIX: 'user:'
});

// RediSearch Query
const results = await client.ft.search('idx:users', '@role:{Architect} @name:Sharjeel');
```

---

## 🔴 7. High-Frequency Exam Trap Alerts 🚨

> [!WARNING]
> - **Trap 1:** Forgetting `await client.connect()` in `node-redis` v4 will throw `ClientClosedError`.
> - **Trap 2:** Always attach `client.on('error', cb)` before connecting; unhandled error events will crash the Node.js process.
> - **Trap 3:** In Pub/Sub, never reuse the publisher connection for subscriptions — use `client.duplicate()`.
> - **Trap 4:** `client.hGetAll()` returns empty object `{}` (truthy in JS) when a key does not exist; check `Object.keys(res).length === 0`.
> - **Trap 5:** Sorted set range commands are 0-indexed: `0, -1` returns all elements.
