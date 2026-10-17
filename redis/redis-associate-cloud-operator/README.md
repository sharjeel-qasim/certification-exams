# Redis Associate Cloud Operator — Practice Question Bank

[![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)](https://redis.io/)
[![Exam](https://img.shields.io/badge/Certification-Redis_Associate_Cloud_Operator-red?style=for-the-badge)](#table-of-contents)
[![Questions](https://img.shields.io/badge/Questions-65%20Verified%20MCQs-success?style=for-the-badge)](#table-of-contents)
[![Cheat Sheet](https://img.shields.io/badge/Study_Guide-Cheat_Sheet-orange?style=for-the-badge)](CHEAT_SHEET.md)

Complete Multiple Choice Question (MCQ) Practice Bank for the **Redis Associate Cloud Operator Certification** exam (`65 Questions`). Covers Redis Cloud architecture, DMC proxy vs. OSS Cluster API, subscription planning (Essentials vs. Pro), high availability, persistence, Search & Query sizing, RBAC & ACL security, private networking (VPC Peering, PrivateLink, PSC, Transit Gateway), Prometheus/Grafana observability, REST API / Terraform / Pulumi automation, and data modeling.

> ⚡ **Quick Review:** Check out the [**Redis Associate Cloud Operator Cheat Sheet**](./CHEAT_SHEET.md) for a high-yield summary of Redis Cloud architecture, HA/replication, PSC/peering, security, and CLI diagnostics before testing yourself below.

---

## Table of Contents

- [Domain 1: Redis Cloud Architecture, Clustering & Sharding (Q1 – Q6)](#domain-1-redis-cloud-architecture-clustering--sharding)
- [Domain 2: Subscription Planning, Sizing, Availability & Durability (Q7 – Q24)](#domain-2-subscription-planning-sizing-availability--durability)
- [Domain 3: Security, Access Control (RBAC / ACLs) & Compliance (Q25 – Q34)](#domain-3-security-access-control-rbac--acls--compliance)
- [Domain 4: Private Networking & Cloud Connectivity (Q35 – Q43)](#domain-4-private-networking--cloud-connectivity)
- [Domain 5: Observability, Prometheus & Grafana Monitoring (Q44 – Q50)](#domain-5-observability-prometheus--grafana-monitoring)
- [Domain 6: Automation (REST API, Terraform, Pulumi) & Data Modeling (Q51 – Q65)](#domain-6-automation-rest-api-terraform-pulumi--data-modeling)

---

## Domain 1: Redis Cloud Architecture, Clustering & Sharding

### Question 1
An application team is considering enabling the **OSS Cluster API** on a Redis Cloud database. They currently use standard (non-cluster-aware) Redis clients. What should the operator explain before they make that change?

- **A.** Enabling OSS Cluster API would add failover replicas automatically.
- **B.** Enabling OSS Cluster API would increase per-shard throughput without affecting clients.
- **C.** Redis Cloud would still fully hide cluster topology, so standard clients could continue unchanged.
- **D.** The clients must be cluster-aware and able to work with cluster topology.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** When the **OSS Cluster API** is enabled (**D**), Redis Cloud exposes the multi-shard cluster topology (`MOVED`/`ASK` slot redirections and `CLUSTER SLOTS` metadata) directly to clients, requiring **cluster-aware Redis clients**. **A** is wrong because replication/HA is configured independently of the OSS Cluster API. **B** and **C** are wrong because enabling OSS Cluster API changes how clients discover and route to shards rather than transparently hiding the topology behind the standard single-endpoint proxy mode.

</details>

---

### Question 2
After a planned resharding event, the application continues using the same database endpoint without any client-side updates to connection details or shard mappings. Which Redis Cloud component makes this seamless behavior possible?

- **A.** REST API
- **B.** Cluster Manager
- **C.** DMC (Data Management Controller) Proxy
- **D.** Replica shard

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** By default, Redis Cloud routes client connections through the **DMC (Data Management Controller) Proxy** (**C**), which abstracts away underlying shard locations, resharding events, and replica promotions behind a single stable database endpoint. **A (REST API)** and **B (Cluster Manager)** are control-plane management components rather than data-plane proxies, and **D (Replica shard)** provides high-availability redundancy rather than connection routing.

</details>

---

### Question 3
Redis Cloud automatically calculates the number of shards needed based on a database's size and throughput configuration. What does that scaling model mean for the data itself?

- **A.** Replica shards split the writable keyspace with the primary to raise throughput.
- **B.** The keyspace is partitioned across multiple shards, with each shard handling a subset of the data.
- **C.** The full keyspace stays on one shard and Redis adds threads to increase capacity.
- **D.** The REST API distributes keys across nodes while the database stays single-process.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Horizontal scaling (sharding/clustering) in Redis Cloud partitions the **16,384 hash slots** across multiple primary shards (**B**), with each primary shard storing and processing a distinct subset of the keyspace. **A** is wrong because replica shards store a read-only copy of their primary shard rather than splitting the writable keyspace. **C** is wrong because core Redis command execution per shard is single-threaded and scales out via multiple shard processes. **D** is wrong because the REST API is for control-plane automation, not data-plane key distribution.

</details>

---

### Question 4
An application is expected to need more than 25 GB of data (requiring multiple shards) and relies on `WATCH`/`MULTI`/`EXEC` transactions across related keys. What should the operator discuss with the application team before deployment?

- **A.** Enabling OSS Cluster API lets transactions run across any shards automatically.
- **B.** Multi-AZ replication removes clustering limits on transactions.
- **C.** The app should have a hash tag strategy so keys used together land in the same hash slot.
- **D.** Redis Cloud automatically keeps related keys together during clustering, so the app needs no changes.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** Multi-key operations and `WATCH`/`MULTI`/`EXEC` transactions in a sharded Redis database require all involved keys to reside in the same hash slot on the same shard. Using **hash tags** (**C**, e.g., `{user:123}:profile` and `{user:123}:cart`) ensures related keys hash to the exact same slot. **A** and **B** are wrong because neither OSS Cluster API nor Multi-AZ enables cross-shard multi-key transactions. **D** is wrong because Redis hashes the full key name by default unless explicit `{...}` hash tags are used by the application.

</details>

---

### Question 5
A master (primary) shard fails on a replicated Redis Cloud database. What outcome should the operator expect?

- **A.** The database stays online but accepts only reads until an operator rebuilds the failed shard.
- **B.** Redis Cloud pauses client traffic until it restores the failed shard from backup.
- **C.** Redis Cloud promotes the replica and keeps serving traffic through the same database endpoint.
- **D.** Clients switch to a new replica endpoint and must update their connection settings.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** When a primary shard fails on a replicated Redis Cloud database, Redis Cloud automatically **promotes the corresponding replica shard to primary** and updates the DMC proxy routing so read and write traffic continues through the **same database endpoint** (**C**). **A** and **B** are wrong because failover is automatic and keeps the database writable without waiting for manual rebuilds or backup restores. **D** is wrong because the database endpoint hostname/port remains unchanged.

</details>

---

### Question 6
A team adds replica shards (enables replication) to improve database availability. What happens to the write capacity of the primary shard?

- **A.** It increases only when the replica is in a different availability zone.
- **B.** It stays the same; replica shards improve availability but do not increase primary-shard write capacity.
- **C.** It increases enough that larger datasets can often stay single-shard.
- **D.** It doubles because the replica contributes extra writable memory to the primary.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** In Redis Cloud, **replica shards** maintain a synchronized copy of the primary shard for high availability and automatic failover—they do **not** add writable memory or increase primary-shard write capacity (**B**). **A**, **C**, and **D** are wrong because scaling writable memory or write throughput requires adding **primary shards** (sharding), not replica shards.

</details>

---

## Domain 2: Subscription Planning, Sizing, Availability & Durability

### Question 7
A SaaS company wants one Redis Cloud subscription that can host several production databases and connect privately to cloud VPCs. Which Redis Cloud subscription plan should the operator choose?

- **A.** Pro
- **B.** Essentials (Free)
- **C.** Essentials with Redis Flex
- **D.** Essentials (Paid)

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Redis Cloud Pro** (**A**) supports hosting multiple production databases within a single subscription, dedicated cloud infrastructure, dynamic auto-scaling/sharding, and private networking options (VPC Peering, PrivateLink, PSC, Transit Gateway). **B**, **C**, and **D** are wrong because Essentials plans do not support private networking (VPC Peering/PrivateLink/PSC/TGW) or multi-database dedicated cluster subscriptions.

</details>

---

### Question 8
A team is launching one small internal cache database. Lowest cost is the priority, and there is no requirement to host multiple databases in one subscription or use private networking. Which subscription is the best fit?

- **A.** Pro
- **B.** Pro with Active-Active enabled
- **C.** Essentials (Free)
- **D.** Essentials with Redis Flex

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **Essentials (Free)** (**C**) provides a zero-cost, single small database tier ideal for lightweight internal caches, development, and testing when Pro features are unnecessary. **A** and **B** incur dedicated Pro cluster infrastructure costs, and **D** (Redis Flex on SSD/Flash) is designed for large datasets rather than a small lowest-cost cache.

</details>

---

### Question 9
A company wants to isolate billing, capacity planning, and operational blast radius for a new critical inventory database that is expected to consume substantial memory and throughput. What is the best recommendation?

- **A.** Create a new dedicated Pro subscription for the inventory database.
- **B.** Place the inventory database in an Essentials subscription to isolate it.
- **C.** Add the database to the existing Pro subscription and lower its throughput setting.
- **D.** Add it to the existing Pro subscription and size memory and throughput appropriately.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Because all databases inside a single Pro subscription share the underlying subscription cluster infrastructure and billing boundary, creating a **new dedicated Pro subscription** (**A**) provides complete infrastructure, billing, and blast-radius isolation for a heavy workload. **B** is wrong because Essentials is for small/fixed-capacity workloads rather than high-memory/high-throughput production systems. **C** and **D** are wrong because keeping the database in the existing Pro subscription still shares billing and cluster-level blast radius with other databases in that subscription.

</details>

---

### Question 10
An operator wants the strongest possible separation between development, QA, and production so each environment can be scaled, changed, or retired without sharing a subscription with the others. All three environments also need Pro-tier capabilities. Which setup best fits?

- **A.** Use one Pro subscription for development and QA, and a second Pro subscription for production.
- **B.** Use separate Pro subscriptions for development, QA, and production.
- **C.** Use one Pro subscription with three databases, one for each environment.
- **D.** Use paid Essentials subscriptions for development and QA, and one Pro subscription for production.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Using **separate Pro subscriptions for development, QA, and production** (**B**) ensures full lifecycle independence, separate network/VPC boundaries, and zero noisy-neighbor contention across all three environments while retaining Pro features in each. **A** and **C** share a subscription across environments, violating the requirement that no environment share a subscription, and **D** fails the requirement that all three environments have Pro-tier capabilities.

</details>

---

### Question 11
A platform team supports two unrelated business units that want separate billing ownership and strict blast-radius isolation between their Redis Cloud environments. Which approach best matches Redis Cloud guidance?

- **A.** Use one shared Pro subscription and separate the units with console users and billing tags.
- **B.** Use separate Pro subscriptions for the two business units.
- **C.** Use one Pro subscription with separate databases for each unit and rely on subscription-level alerts.
- **D.** Use one Pro subscription with separate private connections for each unit.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** In Redis Cloud, payment methods, billing ownership, and underlying cluster VMs are scoped at the **subscription level**. Separate **Pro subscriptions** (**B**) are required to isolate billing and operational blast radius between business units. **A**, **C**, and **D** all place both business units inside a single shared Pro subscription, which shares a single payment method and shared underlying cluster infrastructure.

</details>

---

### Question 12
An engineer asks why overloading one Pro subscription with many databases can still create issues even though each database has its own memory and throughput settings. What should the operator explain?

- **A.** Each database in a Pro subscription is pinned to a separate private network, so contention comes from DNS limits.
- **B.** A Pro subscription is backed by shared subscription infrastructure, so its databases can still contend for resources.
- **C.** A Pro subscription stores metadata only, while the databases run in Essentials infrastructure.
- **D.** Each Pro database gets a completely separate backend cluster even within the same subscription, so only endpoint settings are shared.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Databases within the same Pro subscription run on **shared subscription cluster infrastructure** (nodes/VMs and network interfaces) (**B**), meaning excessive databases or spikes in one database can contend for underlying cluster resources. **A** is wrong because all databases in a subscription share the subscription's VPC/private network. **C** is wrong because Pro databases run on dedicated Pro cluster infrastructure, not Essentials. **D** is wrong because databases in the same Pro subscription share the underlying cluster nodes rather than getting separate backend clusters.

</details>

---

### Question 13
A workload must start as a multi-region writable Redis Cloud deployment and the team does not yet have an existing subscription. Which plan is most correct?

- **A.** Create a standard single-region Pro database first, then convert that database into an Active-Active deployment without creating an Active-Active subscription.
- **B.** Create a new Pro database, choose Custom settings, and enable Active-Active (Multi-region).
- **C.** Start with an Essentials database, then migrate it into an Active-Active deployment when traffic grows.
- **D.** Use Multi-AZ in one region because it provides geo-distributed multi-region writes without Active-Active.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Active-Active (CRDB)** multi-region writable deployments are a **Pro** capability that must be selected during subscription/database creation (via **Pro -> Custom settings -> Enable Active-Active / Multi-region**, **B**). **A** is wrong because a standard single-region Pro subscription cannot be converted in place into an Active-Active subscription. **C** is wrong because the workload must start as multi-region writable and Essentials does not support Active-Active. **D** is wrong because Multi-AZ only distributes shards across availability zones within a **single** cloud region, not across multiple regions.

</details>

---

### Question 14
A team will use Redis Cloud for session data and API responses that can be rebuilt from the primary database, prioritizing lowest cost over durable recovery. Which starting configuration direction is the best fit?

- **A.** Increase Query Performance Factor to reduce the risk of data loss.
- **B.** Start without replication or persistence unless a separate availability requirement justifies it.
- **C.** Enable Multi-AZ and AOF on every write because all Redis data should be treated as permanent.
- **D.** Use Active-Active across regions so rebuilt data survives any outage.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Ephemeral cache data that can be easily reconstructed from a backend system of record does not require the extra 2x memory cost of replication or disk I/O overhead of persistence unless high availability SLAs demand replication (**B**). **A** is wrong because Query Performance Factor accelerates Search & Query rather than durability. **C** and **D** add substantial cost (2x+ memory, disk I/O, and multi-region infrastructure) that contradicts the lowest-cost priority for rebuildable cache data.

</details>

---

### Question 15
A product team will store shopping cart and profile data in Redis Cloud as a primary operational store, prioritizing durability and recovery rather than lowest cost. Which configuration direction is the best fit?

- **A.** Disable persistence and rely on remote backup only.
- **B.** Enable high availability (replication / Multi-AZ) and data persistence.
- **C.** Leave replication and persistence off so the database stays single-copy.
- **D.** Use `noeviction` as the main durability control.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** When Redis Cloud serves as a primary system of record, enabling both **high availability (replication + Multi-AZ)** for automatic failover and **data persistence (AOF / snapshots)** (**B**) protects against both node/AZ failures and data loss. **A** is wrong because periodic remote backups alone leave a large recovery point objective (RPO) window if a node restarts between backups without persistence. **C** risks complete data loss and downtime on shard failure. **D** is wrong because `noeviction` only prevents memory-pressure key eviction—it does not persist data to disk or provide failover replicas.

</details>

---

### Question 16
A team is creating a Redis 8.4 Pro database that will use **Search and Query** heavily. What should the operator know about sizing and enabling this capability?

- **A.** Search and Query does not materially affect sizing, so creation can be based only on base dataset size.
- **B.** Search and Query cannot be used on Redis 8.4 unless Query Performance Factor is configured first.
- **C.** Search and Query must be enabled later from database settings after the initial database is created.
- **D.** Search and Query is included by default on Redis 8.x, so sizing should account for index size and query throughput.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** Starting with Redis 8.x, **Search and Query** capabilities are built in by default (**D**). Because secondary indexes consume additional RAM alongside the keys themselves, operators must size the database memory and throughput to accommodate both the **base dataset and the search indexes**. **A** is wrong because index memory overhead is significant and must be sized for. **B** is wrong because Query Performance Factor is an optional performance multiplier, not a prerequisite to use Search and Query. **C** is wrong because Search and Query is already included by default on Redis 8.x.

</details>

---

### Question 17
A team is using Search and Query heavily on a document database. The operator is willing to allocate more compute/memory resources to speed up search queries without changing the data model. Which setting is intended for that tradeoff?

- **A.** Change the eviction policy to `noeviction`
- **B.** Increase the remote backup frequency
- **C.** Increase the Query Performance Factor
- **D.** Enable Multi-AZ for the database

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** The **Query Performance Factor (QPF)** multiplier (**C**) in Redis Cloud provisions additional shards/CPU cores specifically to accelerate secondary index scanning and Search & Query throughput. **A (`noeviction`)** controls full-memory behavior, **B (remote backup frequency)** controls off-cluster RDB exports, and **D (Multi-AZ)** controls availability zone placement for failover—none of them speed up search query execution.

</details>

---

### Question 18
In the Redis Cloud UI, the operator enters a **60 GB** dataset size and chooses a **highly available (replicated)** database. What total memory requirement should they expect Redis Cloud to calculate behind the scenes?

- **A.** About **120 GB** of total memory required
- **B.** About 30 GB of total memory because replication compresses the second copy
- **C.** About 60 GB of total memory because dataset size already includes the replica
- **D.** About 60 GB of RAM plus a separate 60 GB only if AOF is enabled

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Enabling replication (High Availability) maintains a full in-memory replica shard for every primary shard, **doubling** the total RAM required ($60\text{ GB primary} + 60\text{ GB replica} = 120\text{ GB total}$, **A**). **B** and **C** are wrong because replicas store a full uncompressed copy in RAM on top of the entered dataset size. **D** is wrong because AOF is stored on persistent disk storage, whereas the extra 60 GB of RAM is required by the in-memory replica shards.

</details>

---

### Question 19
An operations team wants client traffic to continue being served automatically if one cloud availability zone (AZ) in the region experiences an outage. Which setting directly addresses that requirement?

- **A.** Increase the Query Performance Factor
- **B.** Choose Multi-AZ during database creation
- **C.** Configure remote backup on a shorter interval
- **D.** Disable eviction

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Multi-AZ** (**B**) places primary shards and their corresponding replica shards in **different cloud Availability Zones** within the same region so an entire AZ failure triggers automatic failover to replicas in healthy AZs. **A** tunes search index compute, **C** exports periodic backups to object storage (requiring manual restore rather than automatic AZ failover), and **D** prevents key eviction when memory is full.

</details>

---

### Question 20
A database already has enough dataset size (memory headroom), but rising traffic means the provisioned operations per second (throughput) are no longer sufficient. What is the best scaling response?

- **A.** Increase throughput without increasing dataset size.
- **B.** Increase both dataset size and throughput even though memory is already sufficient.
- **C.** Add replica shards and keep throughput the same because replication increases primary write capacity.
- **D.** Increase dataset size only because throughput will scale only with memory.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Redis Cloud Pro allows **decoupled scaling of throughput (ops/sec) and dataset size (GB)**. You can increase the provisioned throughput setting independently (**A**) to add shards/compute without paying for unnecessary extra memory. **B** and **D** waste money on unneeded RAM, and **C** is wrong because replica shards in Redis Cloud are for high-availability failover and do not increase primary write throughput.

</details>

---

### Question 21
A production workload places the highest priority on minimizing the loss of recently acknowledged writes and is willing to accept extra write latency/overhead to get that protection. Which Redis Cloud data persistence setting best fits?

- **A.** Append-only file (AOF) every 1 second
- **B.** Snapshot every 1 hour
- **C.** No persistence
- **D.** Append-only file (AOF) on every write

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** **Append-only file (AOF) on every write (`appendfsync always`)** (**D**) flushes every write operation to persistent disk storage before acknowledging it, offering the strongest durability (`RPO ≈ 0`) at the cost of higher write latency. **A (AOF every 1 second)** can lose up to 1 second of writes, **B (Snapshot every 1 hour)** can lose up to 1 hour of writes, and **C (No persistence)** does not write data to disk at all.

</details>

---

### Question 22
A cache database stores many keys without TTLs, and the team would rather evict older least-recently-used data across all keys than fail writes when memory is full. Which eviction policy best matches that goal?

- **A.** `allkeys-lru`
- **B.** `noeviction`
- **C.** `volatile-random`
- **D.** `volatile-lru`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **`allkeys-lru`** (**A**) evicts the least-recently-used keys from the **entire keyspace** regardless of whether a TTL (`EXPIRE`) is set. **B (`noeviction`)** returns Out-Of-Memory (`OOM`) errors on writes when full instead of evicting keys. **C (`volatile-random`)** and **D (`volatile-lru`)** only evict keys that have an expiration (TTL) set, so they fail to evict keys without TTLs.

</details>

---

### Question 23
A company wants a continuously synchronized replica database in another location for disaster recovery, and that target database should remain **read-only** until promoted during a DR event. Which feature is the best fit?

- **A.** Remote backup
- **B.** Active-Passive (`Replica Of`)
- **C.** Active-Active
- **D.** Multi-AZ

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Active-Passive (`Replica Of`)** (**B**) continuously replicates data asynchronously from a source database to one or more **read-only** target databases (including across regions or subscriptions) that can be promoted during a DR event. **A (Remote backup)** only takes periodic point-in-time files rather than maintaining a live synchronized database. **C (Active-Active)** makes all participating regions writable simultaneously rather than read-only. **D (Multi-AZ)** only replicates shards across AZs within the same region and database.

</details>

---

### Question 24
A company's disaster-recovery policy requires restores to come from scheduled point-in-time copies stored in an external cloud object-storage bucket (such as Amazon S3, Google Cloud Storage, or Azure Blob Storage). Which feature should the operator configure?

- **A.** Append-only file every 1 sec
- **B.** Snapshot persistence every 1 hour
- **C.** Remote backup to a supported external target
- **D.** Active-Passive replication to a standby database

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **Remote backups** (**C**) export scheduled point-in-time RDB backup files to customer-managed external cloud storage buckets (S3, GCS, Azure Blob Storage, or FTP/SFTP) for off-cluster retention and disaster recovery. **A** and **B** are internal cluster disk persistence mechanisms rather than exports to external customer object storage, and **D** streams live changes to a standby Redis database rather than saving point-in-time archive files to an object storage bucket.

</details>

---

## Domain 3: Security, Access Control (RBAC / ACLs) & Compliance

### Question 25
According to the Redis Cloud Shared Responsibility Model, who is responsible for patching the operating systems that run the Redis Cloud environment?

- **A.** The customer and cloud provider only
- **B.** The public cloud provider
- **C.** The customer
- **D.** Redis

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** Under the Redis Cloud Shared Responsibility Model, **Redis** (**D**) is responsible for patching and maintaining the operating system nodes and Redis software that run the managed Redis Cloud cluster infrastructure. **C (The customer)** is only responsible for patching OS instances, runtimes, and client libraries in their own client-side application environment. **B (The public cloud provider)** manages the underlying physical data centers, hardware, and hypervisors, and **A** is false because it excludes Redis entirely.

</details>

---

### Question 26
A security team wants an employee to sign in to the Redis Cloud console and see subscription and database details, without being able to create, modify, or delete resources or billing. Which console role is the least-privileged option that still allows that read-only access?

- **A.** Manager
- **B.** Owner
- **C.** Viewer
- **D.** Reader

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** The Redis Cloud console RBAC roles are **Owner**, **Member**, **Manager**, **Billing Admin**, and **Viewer**. The **Viewer** role (**C**) is the least-privileged built-in role that grants read-only visibility into subscriptions and databases in the console. **A (Manager)** and **B (Owner)** grant broad administrative permissions to create, modify, or delete databases/subscriptions, and **D (Reader)** is not a valid Redis Cloud console RBAC role name.

</details>

---

### Question 27
A company uses local Redis Cloud console accounts rather than SAML SSO and wants those users to enforce Multi-Factor Authentication (MFA) and user access policies. Which console role can manage user accounts and account-level settings?

- **A.** An account Owner
- **B.** The cloud provider account administrator
- **C.** Any Viewer
- **D.** Any database user with a Full-Access ACL

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Only an **account Owner** (**A**) in the Redis Cloud console has permissions to manage team user accounts, assign console roles, and configure account-wide security and authentication settings. **B** manages the underlying AWS/GCP/Azure cloud account rather than Redis Cloud console RBAC, **C (Viewer)** has read-only console access, and **D** is a data-plane Redis ACL user rather than a control-plane console administrator.

</details>

---

### Question 28
A company already uses **Okta** to centralize authentication for internal apps and wants Redis Cloud console users to authenticate through that centralized identity provider. Which approach best fits?

- **A.** Share one Owner account among administrators
- **B.** Configure SAML SSO
- **C.** Ask each user to create a social login
- **D.** Use database ACLs instead of console authentication

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Redis Cloud supports enterprise **SAML 2.0 Single Sign-On (SSO)** (**B**) integration with identity providers such as Okta, Microsoft Entra ID (Azure AD), JumpCloud, and OneLogin for centralized console authentication and role mapping. **A** violates security auditing and individual accountability, **C (social login)** uses consumer OAuth accounts rather than enterprise Okta directory policies, and **D (database ACLs)** authenticates Redis data-plane client connections rather than Redis Cloud console users.

</details>

---

### Question 29
An operator plans to convert an existing Redis Cloud console user to social login (Google/GitHub OAuth) or migrate their authentication method. What caveat should the operator explain first?

- **A.** The migration automatically removes the user's database access and ACL assignments.
- **B.** The user must be deleted and recreated before social login can be enabled.
- **C.** The change cannot be reverted once the user is migrated.
- **D.** The migration automatically converts the user to an account Owner.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Converting a local console user account to social login or changing its authentication binding automatically resets/removes the user's associated database-level access and ACL links (**A**), requiring the operator to review and reconfigure those permissions. **B** is wrong because users can be migrated without full deletion/recreation, **C** is wrong because authentication settings are not permanently irreversible, and **D** is wrong because migrating authentication does not escalate a user's role to Owner.

</details>

---

### Question 30
A team needs one application user to run only approved Redis commands (e.g., `+@read`) against a specific subset of keys (e.g., `~app1:*`) in a database. Which Redis Cloud access control model supports that requirement?

- **A.** Console roles such as Owner and Viewer
- **B.** CIDR allow lists on the database endpoint
- **C.** Users assigned to roles, with roles defined by ACL rules
- **D.** MFA for Redis Cloud console users

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** Data-plane access in Redis Cloud is governed by **Redis ACLs** (**C**): you define **ACL rules** (command categories like `+@read`/`-@dangerous` and key patterns like `~app1:*`), group them into **Roles**, and assign those roles to **Database Access Control Users**. **A** and **D** control human sign-in and permissions in the web management console, while **B (CIDR allow lists)** filters network source IP addresses at the endpoint level without restricting which Redis commands or keys a connected client can access.

</details>

---

### Question 31
A new database is created, named database users and least-privilege ACL roles are configured, and the application has been updated to connect using its named user. What is the recommended security next step?

- **A.** Disable the `default` database user
- **B.** Rotate the `default` database user's password and keep it for normal application access
- **C.** Keep the `default` database user enabled as a shared fallback alongside the named users
- **D.** Assign the `default` database user the same ACL role as the named application user

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Every new Redis database starts with a `default` user that has full access (`+@all ~*`). Once named application users with least-privilege ACL roles are in place, security best practice is to **disable the `default` user** (**A**) so no client can connect using shared default credentials. **B**, **C**, and **D** leave the `default` account active, which weakens auditability and least-privilege isolation across services.

</details>

---

### Question 32
A team must keep using the database's **public endpoint** for now. Which guidance best matches Redis Cloud security best practices?

- **A.** Disable TLS to reduce latency and rely only on passwords
- **B.** Use the public endpoint without restrictions because Redis Cloud is managed
- **C.** Enable TLS and restrict access with a CIDR allow list
- **D.** Add more console Owners so endpoint changes can be reviewed

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** If a public endpoint must be used, you should always **enable TLS (encryption in transit, including mTLS if supported)** and configure a **source IP/CIDR allow list** (**C**) alongside strong ACL authentication so only trusted application IPs can reach the endpoint. **A** exposes plaintext credentials and data over the public internet, **B** leaves the endpoint reachable from any IP on the internet, and **D** violates least privilege in the console without securing the network endpoint.

</details>

---

### Question 33
A compliance reviewer asks how **encryption at rest** works in Redis Cloud. What should the operator explain?

- **A.** Encryption at rest happens only on public endpoints.
- **B.** Redis Cloud deployments are always encrypted at rest, and data is written to disk when persistence or backups are enabled.
- **C.** Encryption at rest happens only when TLS is enabled.
- **D.** Encryption at rest requires a custom ACL with write privileges.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Redis Cloud encrypts all underlying storage volumes and backup artifacts **at rest by default** (**B**) using cloud provider disk encryption (AES-256, with optional Customer-Managed Keys on Pro), protecting any data written to disk via persistence (AOF/RDB) or backups. **A** and **C** confuse network endpoints and TLS (encryption in transit) with disk encryption at rest, and **D** is wrong because ACLs govern command/key authorization rather than disk encryption.

</details>

---

### Question 34
An engineer who has managed ACLs in self-managed Redis OSS assumes the exact same `ACL` commands (`ACL SETUSER`, `ACL SAVE`, etc.) work identically from a client connected to Redis Cloud. What should the operator explain?

- **A.** ACL behavior carries over unchanged, but only console Owners can apply it.
- **B.** Redis Cloud supports ACLs, but some direct `ACL` commands/operations are restricted because ACLs are centrally managed by the service control plane.
- **C.** ACLs are supported only on Essentials subscriptions.
- **D.** Redis Cloud does not support ACLs at all.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** In Redis Cloud, ACL users and roles are centrally managed through the **Redis Cloud Console, REST API, or Terraform/Pulumi** so the control plane can persist and synchronize ACLs across all shards and proxies; consequently, direct mutating `ACL` commands over a client connection are restricted (**B**). **A** is wrong because client-side `ACL SETUSER`/`ACL SAVE` commands do not work unchanged. **C** and **D** are wrong because Redis Cloud supports ACLs across both Pro and Essentials tiers.

</details>

---

## Domain 4: Private Networking & Cloud Connectivity

### Question 35
A production application runs in the same cloud provider as a Redis Cloud Pro subscription, and the security team requires that database traffic **never traverse the public internet**. Which endpoint and connection path should the operator recommend?

- **A.** Private endpoint (via VPC Peering, PrivateLink, PSC, or Transit Gateway)
- **B.** REST API endpoint
- **C.** Public endpoint with a stronger password
- **D.** Public endpoint with no allow list

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Using a **Private endpoint** over private cloud networking (VPC Peering, AWS PrivateLink, GCP Private Service Connect, Azure Private Link, or AWS Transit Gateway, **A**) keeps all client-to-database traffic entirely on the cloud provider's private backbone network. **B (REST API endpoint)** is for control-plane management over HTTPS rather than application database traffic, and **C** and **D** still route traffic over a public internet endpoint.

</details>

---

### Question 36
A team on an **Essentials** subscription in AWS asks for a private database endpoint (VPC Peering or PrivateLink) for an internal service. What should the operator explain?

- **A.** Essentials can use a private endpoint if the database is recreated with Multi-AZ.
- **B.** Private endpoints and private connectivity options are available only with **Pro** subscriptions.
- **C.** Essentials can use a private endpoint after upgrading only the database settings, not the subscription.
- **D.** Essentials can make the public endpoint private by adding a CIDR allow list.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Private networking** (VPC Peering, AWS PrivateLink, GCP Private Service Connect, Azure Private Link, AWS Transit Gateway) requires dedicated VPC infrastructure and is available **only on Redis Cloud Pro subscriptions** (**B**). **A** and **C** are wrong because Essentials runs on shared multi-tenant infrastructure that cannot use private VPC connectivity without migrating to a Pro subscription. **D** is wrong because adding a CIDR allow list restricts which public IPs can connect, but traffic still traverses the public endpoint rather than a private VPC connection.

</details>

---

### Question 37
An AWS team enters the Redis Cloud VPC CIDR and the application VPC CIDR during **VPC peering** setup and accepts the peering request in AWS, but connectivity still cannot be established. What is the most likely cause?

- **A.** The two VPC CIDR ranges overlap.
- **B.** The database still has its public endpoint enabled.
- **C.** The database is configured with replication.
- **D.** The peering request was accepted, but no one added the **route-table entries** yet.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** Accepting an AWS VPC peering connection only establishes the peering link; traffic will not flow until the customer **updates their application VPC route tables** (**D**) to route the Redis Cloud VPC CIDR block through the `pcx-...` peering connection ID. **A** would have prevented the peering request from being created/accepted in the first place, and **B** and **C** do not block private VPC peering traffic.

</details>

---

### Question 38
After initiating AWS VPC peering from Redis Cloud, the application team accepts the peering request in their AWS account. What step is still required before traffic can route correctly?

- **A.** Import the Redis Grafana dashboards so the team can confirm the peering setup visually.
- **B.** Update the application VPC route tables so the Redis Cloud VPC CIDR routes through the peering connection.
- **C.** Rotate the database password and reconnect the clients through the new private path.
- **D.** Enable Multi-AZ on the database so traffic can fail over across availability zones automatically.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Both VPCs must know how to route packets to each other. Redis Cloud automatically configures its side of the peering route, and the customer must **add a route in their application VPC route table(s)** pointing the Redis Cloud VPC CIDR to the VPC Peering target (**B**). **A (Grafana dashboards)**, **C (password rotation)**, and **D (Multi-AZ)** have no effect on AWS VPC Layer-3 packet routing.

</details>

---

### Question 39
A security reviewer objects to **VPC peering** because it creates broad VPC-to-VPC network reachability instead of service-level isolation. Which characteristic of VPC peering are they highlighting?

- **A.** VPC peering allows network routing between the two VPCs at the network layer, not just unidirectional access to a single specific service endpoint.
- **B.** VPC peering exposes only a single managed service endpoint instead of opening VPC-level routing.
- **C.** VPC peering always sends the traffic over the public internet unless TLS is enabled.
- **D.** VPC peering is limited to Essentials databases that do not use other private connectivity options.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **VPC Peering** connects two VPC networks bidirectionally at the network (Layer 3) level (**A**), whereas **AWS PrivateLink / GCP Private Service Connect** exposes only a single managed service endpoint unidirectionally into the consumer VPC (**B** describes PrivateLink/PSC, not VPC Peering). **C** is wrong because VPC Peering stays entirely on the cloud provider's private network, and **D** is wrong because VPC Peering is a Pro-only feature.

</details>

---

### Question 40
A **Google Cloud (GCP)** deployment needs private connectivity to Redis Cloud, but the application VPC CIDR overlaps with the default CIDR and the security team does not want full VPC-to-VPC exposure. Which option best fits?

- **A.** Multi-AZ
- **B.** Private Service Connect (PSC)
- **C.** Public endpoint with TLS
- **D.** VPC Peering

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** On Google Cloud, **Private Service Connect (PSC)** (**B**) provides private, unidirectional, service-level connectivity that **tolerates overlapping VPC CIDR ranges** and avoids full VPC-to-VPC network peering. **A (Multi-AZ)** is an availability feature rather than a networking method, **C (Public endpoint)** traverses the public internet instead of private connectivity, and **D (VPC Peering)** fails when VPC CIDRs overlap and exposes bidirectional VPC-level routing.

</details>

---

### Question 41
An **AWS** platform team needs a regional **hub-and-spoke** connectivity model that can connect many spoke VPCs and on-premises networks to Redis Cloud, and is willing to pay more for the added routing flexibility. Which option best matches that requirement?

- **A.** AWS PrivateLink
- **B.** CIDR allow list
- **C.** VPC Peering
- **D.** AWS Transit Gateway

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** **AWS Transit Gateway (TGW)** (**D**) acts as a regional cloud router for **hub-and-spoke** topologies, allowing many spoke VPCs and on-premises VPN/Direct Connect networks to reach Redis Cloud through a central transit hub. **A (AWS PrivateLink)** provides point-to-point service endpoint projections rather than transitive hub-and-spoke routing, **B (CIDR allow list)** is an IP filter rather than a private routing architecture, and **C (VPC Peering)** is non-transitive (1-to-1 VPC links) and does not natively support hub-and-spoke transit routing.

</details>

---

### Question 42
An **AWS** security team wants private Redis Cloud connectivity that **tolerates overlapping CIDR ranges** and exposes **only the specific Redis service endpoint** instead of peering the entire VPC. Which option most directly matches that requirement?

- **A.** Public endpoint with TLS and CIDR allow list
- **B.** AWS Transit Gateway
- **C.** AWS PrivateLink
- **D.** VPC Peering

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **AWS PrivateLink** (**C**) projects an Elastic Network Interface (ENI) endpoint directly into the customer's AWS VPC, allowing private unidirectional connections to the Redis Cloud service even when VPC CIDRs overlap and without peering the entire VPC. **A** uses the public internet rather than private connectivity, while **B (AWS Transit Gateway)** and **D (VPC Peering)** operate via Layer-3 CIDR routing and cannot route across overlapping CIDR blocks without NAT.

</details>

---

### Question 43
An operator asks why **private endpoints** are generally preferred over public endpoints for production workloads in Redis Cloud. Which explanation is the best fit?

- **A.** Private endpoints automatically work even when no private connectivity option is configured.
- **B.** Private endpoints remove the need for TLS or database authentication on client connections.
- **C.** Private endpoints are equally available on Essentials without changing the subscription tier.
- **D.** Private endpoints keep traffic on the cloud provider's internal network instead of exposing it to the public internet.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** Private endpoints eliminate exposure to the public internet by keeping all data-plane traffic inside the cloud provider's private network backbone (**D**), reducing both attack surface and internet routing hops. **A** is wrong because private endpoints require configuring VPC Peering, PrivateLink, PSC, or TGW first. **B** is wrong because defense-in-depth still recommends database authentication and TLS even on private networks. **C** is wrong because private endpoints are only available on Pro subscriptions.

</details>

---

## Domain 5: Observability, Prometheus & Grafana Monitoring

### Question 44
A Pro subscription already has a private connectivity option configured. **Prometheus** is running on an engineer's local laptop outside that private network, so metric scraping fails. What is the best fix?

- **A.** Keep Prometheus on the laptop and add its IP to the database CIDR allow list.
- **B.** Ask Redis support to expose the metrics endpoint publicly instead of using the existing private network.
- **C.** Deploy Prometheus in a network that can reach the subscription through the private connectivity option.
- **D.** Point Prometheus at the public database endpoint instead of the internal Prometheus metrics endpoint.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** The Redis Cloud Prometheus metrics endpoint (`:8070`) is **only exposed on the internal/private cluster network**. Therefore, the Prometheus server must be deployed inside a VPC/network (or reachable via VPN to that VPC) connected to the Pro subscription via VPC Peering, PrivateLink, PSC, or Transit Gateway (**C**). **A** and **B** are wrong because port `8070` is never exposed on the public internet or affected by public database CIDR allow lists, and **D** is wrong because the database port speaks the Redis Serialization Protocol (RESP), not HTTP Prometheus metrics.

</details>

---

### Question 45
An operator reviewing an **Essentials** deployment asks why the Redis-provided Prometheus and Grafana external scraping workflow is not available. What should the operator explain?

- **A.** Essentials supports that workflow only if replication is disabled.
- **B.** Essentials supports that workflow only after enabling TLS.
- **C.** That Redis-provided Prometheus/Grafana scraping workflow is available on **Pro**, not Essentials.
- **D.** Grafana can scrape Essentials directly without Prometheus.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** The dedicated Prometheus metrics exporter endpoint (`:8070`) and private network scraping workflow are features of **Redis Cloud Pro** subscriptions (**C**), which run on dedicated cluster nodes. **A** and **B** are wrong because Essentials uses shared multi-tenant infrastructure and does not expose port `8070` regardless of replication or TLS settings, and **D** is wrong because Grafana visualizes metrics from a data source like Prometheus rather than scraping Essentials directly.

</details>

---

### Question 46
A Prometheus administrator is configuring the Redis Cloud scrape target and must choose the correct endpoint and port. Which target is correct?

- **A.** The REST API URL for the database
- **B.** The Redis Cloud console URL over HTTPS on port `443`
- **C.** The internal cluster address over HTTPS on port **`8070`**
- **D.** The public database endpoint on the database port

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** Redis Cloud Pro exposes its Prometheus metrics exporter (`redis_exporter` / cluster metrics) on the **internal cluster master address over HTTPS on port `8070`** (**C**). **A (REST API URL)** is for asynchronous resource provisioning, **B (Console URL on 443)** is the web UI for human operators, and **D (Public database endpoint)** serves Redis client commands rather than Prometheus `/metrics` scrapes.

</details>

---

### Question 47
An operator wants to scrape the Redis Cloud Prometheus endpoint from the public internet. What should they know?

- **A.** The Prometheus endpoint becomes public after Grafana is configured.
- **B.** The Prometheus endpoint is **not exposed on the public network**, so they must use private connectivity.
- **C.** The Prometheus endpoint can be scraped publicly as long as TLS is enabled.
- **D.** The Prometheus endpoint is reachable through the same public hostname used for normal client traffic.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** For security reasons, the Redis Cloud Prometheus metrics port (`8070`) is never exposed to the public internet; scraping requires private network connectivity to the internal cluster address (**B**). **A**, **C**, and **D** are false because configuring Grafana, enabling TLS, or using the public database hostname does not expose port `8070` on the public network.

</details>

---

### Question 48
Metrics are already being scraped successfully into Prometheus. The operator now wants prebuilt visualizations for database and subscription status. What should they do next?

- **A.** Configure Grafana as the scrape target and have Prometheus query dashboards from it.
- **B.** Configure Grafana to query the Redis Cloud REST API directly instead of Prometheus.
- **C.** Repoint Prometheus from the metrics endpoint to the public database endpoint so Grafana can read keys.
- **D.** Configure Prometheus as a data source in Grafana and import the official Redis Cloud dashboards.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** In the Prometheus + Grafana monitoring architecture, **Prometheus** scrapes and stores time-series metrics from Redis Cloud (`:8070`), and **Grafana** connects to **Prometheus as a data source** using the official **Redis Cloud Grafana dashboard templates** (Subscription and Database dashboards, **D**). **A** reverses the relationship between Prometheus and Grafana, **B** is wrong because the REST API is for control-plane management rather than time-series telemetry, and **C** breaks metric scraping by pointing Prometheus at a Redis RESP port.

</details>

---

### Question 49
A platform team wants threshold-based alerting, long-term capacity visibility, and the ability to correlate Redis Cloud metrics in their existing observability stack (Datadog, Grafana, PagerDuty, etc.). Which approach best fits?

- **A.** Scrape the Redis Cloud Prometheus endpoint and send those metrics into the team's external observability stack.
- **B.** Rely on the Redis Cloud console alone and review metrics manually instead of exporting them.
- **C.** Poll `redis-cli` on a schedule and treat the command output as the primary observability pipeline.
- **D.** Use remote backup history and scheduled export reports as the main source for alerting.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Scraping the **Prometheus endpoint (`:8070`)** (**A**) provides rich, real-time cluster, shard, and database telemetry that integrates natively with Prometheus Alertmanager, Grafana, Datadog, and other enterprise observability platforms for long-term retention and alerting. **B** lacks external correlation and long-term custom alerting, **C** is fragile and misses cluster-level proxy/node metrics exposed on `:8070`, and **D** only tracks backup file exports rather than live operational metrics.

</details>

---

### Question 50
A team has already configured a private connectivity option and asks where the Prometheus server should be placed to scrape Redis Cloud metrics. Which answer is best?

- **A.** On any laptop with internet access
- **B.** On a bastion host that can reach only the public database endpoint, but not the internal cluster address
- **C.** Inside the Redis Cloud console as a built-in monitoring service for the subscription
- **D.** In a network that can reach the internal cluster address through that private connectivity option

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** Because the Prometheus metrics endpoint is bound to the **internal cluster address on port `8070`**, the Prometheus server must run inside a VPC/VNet that routes to the internal cluster address via the configured private connectivity option (**D**). **A** and **B** cannot reach the internal cluster address, and **C** is wrong because Redis Cloud does not host customer Prometheus servers inside the console.

</details>

---

## Domain 6: Automation (REST API, Terraform, Pulumi) & Data Modeling

### Question 51
A team needs to automate a newly released Redis Cloud capability before the official Terraform or Pulumi providers are updated. Which automation interface is most likely to support it first?

- **A.** Redis Insight
- **B.** Pulumi provider
- **C.** Redis Cloud REST API
- **D.** Terraform provider

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** Both the Terraform provider (**D**) and Pulumi provider (**B**) are built on top of the **Redis Cloud REST API** (**C**). New platform capabilities are exposed in the **REST API** first before downstream IaC providers wrap them. **A (Redis Insight)** is a developer GUI for inspecting data and running Redis commands, not a control-plane provisioning API.

</details>

---

### Question 52
A CI pipeline can create Redis Cloud resources when run from an engineer's laptop, but the exact same API call fails from a shared cloud build runner. The operator recently tightened API key security as a best practice. What is the most likely explanation?

- **A.** The build runner's IP is not included in the API key's allowed CIDR list.
- **B.** CIDR allow lists apply only to database endpoints, not REST API keys.
- **C.** API keys created for one user account cannot be used from CI systems.
- **D.** Shared runners can use Redis Cloud only through Terraform or Pulumi, not directly through the REST API.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Redis Cloud REST API keys support **HTTP source IP/CIDR allow lists** (**A**). If an operator restricts an API key to office/VPN CIDR ranges, requests from external shared CI/CD runners whose IPs are not allow-listed will be rejected with `403 Forbidden`. **B** is false because REST API keys directly support CIDR allow lists. **C** and **D** are false because REST API keys (`x-api-key` and `x-api-secret-key`) work from any CI system or HTTP client whose source IP is permitted.

</details>

---

### Question 53
A `POST` Cloud API request to create a Pro subscription returns `202 Accepted` successfully with a `taskId`. How should the automation script track that asynchronous provisioning request to completion?

- **A.** Test the database endpoint directly to infer whether the subscription task is done.
- **B.** Poll `GET /tasks/{taskId}` until the task status reaches `processing-completed`.
- **C.** Re-send the `POST` request every few minutes until provisioning finishes.
- **D.** Poll the subscriptions list and treat the new subscription appearing as the final completion signal.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Mutating operations in the Redis Cloud REST API are **asynchronous** and return `202 Accepted` with a `taskId`. Clients must poll **`GET /tasks/{taskId}`** until the task status reaches `processing-completed` (**B**, and inspect `response.resourceId` or `response.error`). **A** is wrong because the database endpoint is not known or ready until the task completes, **C** would repeatedly attempt to create duplicate subscriptions, and **D** is unreliable because a subscription appears in the list in a `pending` state before provisioning is actually finished.

</details>

---

### Question 54
An operator wants an Infrastructure-as-Code (IaC) tool for Redis Cloud, prefers writing infrastructure definitions in **Python or JavaScript/TypeScript**, and does not want to use HCL. Which tool is the best fit?

- **A.** Swagger UI only
- **B.** Redis Cloud console
- **C.** Terraform
- **D.** Pulumi

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** **Pulumi** (**D**, via the `@pulumi/rediscloud` / `pulumi_rediscloud` package) lets teams define Redis Cloud infrastructure using general-purpose programming languages such as **Python, TypeScript/JavaScript, Go, and C#**. **A (Swagger UI)** and **B (Redis Cloud console)** are interactive web interfaces rather than declarative IaC tools, and **C (Terraform)** uses HashiCorp Configuration Language (HCL).

</details>

---

### Question 55
An operator wants to preview and review the infrastructure changes **Terraform** intends to make to Redis Cloud before actually applying them. What is the best practice?

- **A.** Create the subscription manually in the console first so Terraform has a target to import.
- **B.** Skip straight to `terraform apply` because Redis Cloud validates everything server-side.
- **C.** Poll `GET /tasks` before the first run to confirm Terraform can reach the API.
- **D.** Run `terraform plan` first to review the execution plan before applying.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** Running **`terraform plan`** (**D**) compares the desired HCL configuration against the current state and displays a dry-run diff of resources to be created, modified, or destroyed before any changes are executed. **A** defeats the purpose of automated IaC provisioning, **B** risks unintended modifications or deletions without review, and **C** is a manual REST API call unrelated to generating a Terraform execution plan.

</details>

---

### Question 56
An automation team wants Redis Cloud infrastructure changes to be repeatable, peer-reviewable before execution, and tracked in Git version control instead of being made manually in the console. Which approach best fits?

- **A.** Manage the infrastructure with an IaC workflow such as Terraform or Pulumi.
- **B.** Poll the tasks API regularly without defining the desired infrastructure state.
- **C.** Record the console steps in a runbook and repeat them manually for each environment.
- **D.** Use Redis Insight as the primary provisioning system for subscriptions and databases.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Declarative **Infrastructure-as-Code (IaC)** workflows using **Terraform** or **Pulumi** (**A**) allow teams to store Redis Cloud configurations in Git, review `plan`/`preview` diffs in pull requests, and apply repeatable changes across environments. **B** only reads task status without managing state, **C** relies on error-prone manual console clicks, and **D (Redis Insight)** is a data-plane GUI client that cannot provision Redis Cloud subscriptions or databases.

</details>

---

### Question 57
A Terraform configuration must reference an **existing** Redis Cloud payment method (or cloud account) that was created outside of Terraform. Which Terraform construct should the operator use to read that existing object?

- **A.** An `output` block
- **B.** A `creation_plan` block
- **C.** A `resource` block
- **D.** A `data` source (`data "rediscloud_payment_method" ...`)

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** In Terraform, a **`data` source** (`data "rediscloud_payment_method" ...`, **D**) queries and reads attributes (such as `id`) of existing infrastructure managed outside the current Terraform state. **A (`output` block)** exports values after execution, **B (`creation_plan`)** is a nested configuration block inside a subscription resource for initial shard sizing rather than a top-level way to read external objects, and **C (`resource` block)** attempts to create and manage a new object rather than reading an existing one.

</details>

---

### Question 58
A retailer sizes a Redis Cloud database based on average daily traffic and throughput today, then struggles during a flash sale when request volume spikes far above normal. Which capacity-planning dimension was most underestimated?

- **A.** Data relationships
- **B.** Key naming conventions
- **C.** Data velocity (peak throughput / ops per second)
- **D.** MFA enforcement

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **Data velocity** (**C**) measures the rate at which data is read and written—specifically **peak operations per second** during traffic spikes like flash sales. Sizing only for average daily throughput causes shard saturation and high latency under peak load. **A (Data relationships)** and **B (Key naming conventions)** concern data modeling rather than throughput sizing, and **D (MFA enforcement)** is a console security control.

</details>

---

### Question 59
A gaming application needs a leaderboard that can return players in rank order and update player scores frequently in $O(\log N)$ time. Which Redis data structure is the best fit?

- **A.** List
- **B.** Sorted Set (`ZSET`)
- **C.** Hash
- **D.** Set

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** A **Sorted Set (`ZSET`)** (**B**) maintains unique members (`playerId`) ordered automatically by a floating-point `score`, supporting $O(\log N)$ score updates (`ZADD`/`ZINCRBY`) and fast rank/range queries (`ZRANGE`, `ZREVRANK`). **A (List)** orders elements by insertion position rather than score, **C (Hash)** maps fields to values without ordering, and **D (Set)** stores unique members without any score or rank ordering.

</details>

---

### Question 60
An operator needs to store flat user profile fields such as `first_name`, `last_name`, `email`, and `loyalty_tier` under a single key (e.g., `user:1001`) with individual field-value access. Which Redis data structure is the best fit?

- **A.** Hash
- **B.** List
- **C.** Set
- **D.** Sorted Set

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** A **Redis Hash** (**A**) maps named fields to values under a single key (`HSET`, `HGET`, `HMGET`, `HGETALL`), providing memory-efficient storage and individual field reads/writes for flat object attributes. **B (List)** is an ordered sequence of strings without field names, **C (Set)** is an unordered collection of unique strings, and **D (Sorted Set)** associates members with numeric scores rather than arbitrary string fields.

</details>

---

### Question 61
A product catalog record contains deeply **nested arrays and objects**, and the team wants to store and retrieve partial nested paths directly using JSONPath syntax. Assuming the database has the needed capability enabled, which structure is the best fit?

- **A.** String with client-side JSON serialization
- **B.** Hash
- **C.** JSON Document (`RedisJSON`)
- **D.** Sorted Set

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **JSON Document (`RedisJSON` — `JSON.SET`, `JSON.GET`)** (**C**) stores hierarchical JSON trees natively in Redis and allows reading or mutating nested sub-objects and arrays via JSONPath without fetching and re-serializing the entire document. **A (String)** requires transferring and re-serializing the entire JSON blob on the client for any sub-field update, **B (Hash)** only supports flat field-value pairs rather than deeply nested arrays/objects with JSONPath, and **D (Sorted Set)** is for score-ordered members.

</details>

---

### Question 62
A service must track one boolean (`yes`/`no`) completion flag for each of millions of sequentially numbered users, and **memory efficiency** is the top priority. Which Redis data structure is the best fit?

- **A.** JSON Document
- **B.** Hash
- **C.** Bitmap
- **D.** Sorted Set

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** A **Bitmap** (`SETBIT`, `GETBIT`, `BITCOUNT`, **C**) stores each user's boolean flag as a single bit at their integer offset, tracking 10 million users in roughly **1.2 MB** of memory. **A (JSON Document)**, **B (Hash)**, and **D (Sorted Set)** store per-element string keys/field names or pointers that consume orders of magnitude more memory for simple boolean flags across millions of sequential IDs.

</details>

---

### Question 63
A marketing system needs to track the **unique** users who have redeemed a coupon so duplicate redemptions are prevented and membership can be checked in $O(1)$ time. Which Redis data structure is the best fit?

- **A.** List
- **B.** JSON Document
- **C.** Set
- **D.** Hash

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** A **Redis Set** (`SADD`, `SISMEMBER`, `SCARD`, **C**) stores an unordered collection of unique strings, automatically ignoring duplicates and providing $O(1)$ membership checks. **A (List)** permits duplicates and requires $O(N)$ scans (`LPOS`) to check membership, **B (JSON Document)** is heavier than needed for simple unique membership checks, and **D (Hash)** requires storing a dummy value for every field and lacks native set operations (`SUNION`, `SINTER`, `SDIFF`).

</details>

---

### Question 64
An operator reviewing a latency issue finds that the application stores **very large values** (multi-megabyte blobs) under single keys, causing event-loop blocking during reads and writes. What is the best recommendation for the application team?

- **A.** Move the same payloads into a Set so Redis treats them as smaller.
- **B.** Increase the key size until it reaches Redis's theoretical 512 MB maximum.
- **C.** Keep the values as they are and rely only on TTL to remove latency.
- **D.** Split the oversized values into smaller logical pieces across multiple keys or fields.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** Because Redis command execution on a shard is single-threaded, reading or writing huge single-key values blocks other commands on that shard and spikes tail latency. **Splitting oversized values into smaller logical keys or Hash fields** (**D**) keeps individual operations fast and allows partial reads. **A** still stores the same oversized payload inside a single key, **B** worsens event-loop blocking and network serialization stalls, and **C** does not prevent latency spikes whenever the key is read or written before expiration.

</details>

---

### Question 65
A developer wants to model relationships in Redis the same way they would in a relational database (using normalized tables and foreign keys). What should they do instead?

- **A.** Create normalized tables and foreign keys inside each Redis database.
- **B.** Store all related data in one very large value so the relationships are hidden inside it.
- **C.** Use structured key naming conventions and Redis data structures (such as Sets, Sorted Sets, Hashes, and JSON) to represent links and access patterns between related data.
- **D.** Rely on API endpoint names instead of storing relationships in Redis.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** Redis is an in-memory key-value and data-structure store designed around **application access patterns**. Relationships are modeled using structured **key naming conventions** (e.g., `customer:42:orders` as a Set/Sorted Set of order IDs) and native Redis data structures or secondary indexes with Search & Query (**C**). **A** is wrong because Redis does not have relational tables or foreign-key constraints, **B** creates hot/oversized keys that degrade performance, and **D** fails to model the data relationships in the data store at all.

</details>
