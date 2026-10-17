# Redis Associate Cloud Operator — Practice Question Bank

[![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)](https://redis.io/)
[![Exam](https://img.shields.io/badge/Certification-Redis_Associate_Cloud_Operator-red?style=for-the-badge)](#table-of-contents)
[![Questions](https://img.shields.io/badge/Questions-65%20Verified%20MCQs-success?style=for-the-badge)](#table-of-contents)
[![Cheat Sheet](https://img.shields.io/badge/Study_Guide-Cheat_Sheet-orange?style=for-the-badge)](CHEAT_SHEET.md)

Complete Multiple Choice Question (MCQ) Practice Bank for the **Redis Associate Cloud Operator Certification** exam (`65 Questions`). Covers Redis Cloud architecture, DMC proxy vs. OSS Cluster API, subscription planning (Essentials vs. Pro), high availability, persistence, Search & Query sizing, RBAC & ACL security, private networking (VPC Peering, PrivateLink, PSC, Transit Gateway), Prometheus/Grafana observability, REST API / Terraform / Pulumi automation, and data modeling.

> [!TIP]
> Preparing for the exam? Review the [Redis Associate Cloud Operator Last-Minute Cram Sheet](CHEAT_SHEET.md) for quick-fire comparison tables on Essentials vs. Pro, private connectivity options across AWS/GCP/Azure, Prometheus port `8070` scraping, and durability settings.

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

**Correct answer:** D

> **Why:** When the **OSS Cluster API** is enabled, Redis Cloud exposes the multi-shard cluster topology (`MOVED`/`ASK` slot redirections) directly to clients instead of masking it behind the DMC proxy. Therefore, applications must use **cluster-aware Redis clients**.

---

### Question 2
After a planned resharding event, the application continues using the same database endpoint without any client-side updates to connection details or shard mappings. Which Redis Cloud component makes this seamless behavior possible?

- **A.** REST API
- **B.** Cluster Manager
- **C.** DMC (Data Management Controller) Proxy
- **D.** Replica shard

**Correct answer:** C

> **Why:** By default, Redis Cloud routes client connections through the **DMC (Data Management Controller) Proxy**, which abstracts away underlying shard locations, resharding events, and replica promotions behind a single stable database endpoint.

---

### Question 3
Redis Cloud automatically calculates the number of shards needed based on a database's size and throughput configuration. What does that scaling model mean for the data itself?

- **A.** Replica shards split the writable keyspace with the primary to raise throughput.
- **B.** The keyspace is partitioned across multiple shards, with each shard handling a subset of the data.
- **C.** The full keyspace stays on one shard and Redis adds threads to increase capacity.
- **D.** The REST API distributes keys across nodes while the database stays single-process.

**Correct answer:** B

> **Why:** Horizontal scaling (sharding/clustering) in Redis Cloud partitions the **16,384 hash slots** across multiple primary shards, with each primary shard storing and processing a distinct subset of the keyspace.

---

### Question 4
An application is expected to need more than 25 GB of data (requiring multiple shards) and relies on `WATCH`/`MULTI`/`EXEC` transactions across related keys. What should the operator discuss with the application team before deployment?

- **A.** Enabling OSS Cluster API lets transactions run across any shards automatically.
- **B.** Multi-AZ replication removes clustering limits on transactions.
- **C.** The app should have a hash tag strategy so keys used together land in the same hash slot.
- **D.** Redis Cloud automatically keeps related keys together during clustering, so the app needs no changes.

**Correct answer:** C

> **Why:** Multi-key operations and `WATCH`/`MULTI`/`EXEC` transactions in a sharded Redis database require all involved keys to reside on the same shard. Using **hash tags** (e.g., `{user:123}:profile` and `{user:123}:cart`) forces related keys into the exact same hash slot.

---

### Question 5
A master (primary) shard fails on a replicated Redis Cloud database. What outcome should the operator expect?

- **A.** The database stays online but accepts only reads until an operator rebuilds the failed shard.
- **B.** Redis Cloud pauses client traffic until it restores the failed shard from backup.
- **C.** Redis Cloud promotes the replica and keeps serving traffic through the same database endpoint.
- **D.** Clients switch to a new replica endpoint and must update their connection settings.

**Correct answer:** C

> **Why:** When a primary shard fails on a replicated Redis Cloud database, Redis Cloud automatically **promotes the corresponding replica shard to primary** and updates the DMC proxy routing so traffic continues through the **same database endpoint** without client configuration changes.

---

### Question 6
A team adds replica shards (enables replication) to improve database availability. What happens to the write capacity of the primary shard?

- **A.** It increases only when the replica is in a different availability zone.
- **B.** It stays the same; replica shards improve availability but do not increase primary-shard write capacity.
- **C.** It increases enough that larger datasets can often stay single-shard.
- **D.** It doubles because the replica contributes extra writable memory to the primary.

**Correct answer:** B

> **Why:** In Redis Cloud, **replica shards** maintain a synchronized copy of the primary shard for high availability and automatic failover—they do **not** add writable memory or increase write throughput (scaling write throughput or keyspace capacity requires adding **primary shards**).

---

## Domain 2: Subscription Planning, Sizing, Availability & Durability

### Question 7
A SaaS company wants one Redis Cloud subscription that can host several production databases and connect privately to cloud VPCs. Which Redis Cloud subscription plan should the operator choose?

- **A.** Pro
- **B.** Essentials (Free)
- **C.** Essentials with Redis Flex
- **D.** Essentials (Paid)

**Correct answer:** A

> **Why:** **Redis Cloud Pro** supports hosting multiple production databases within a single subscription, dedicated cloud infrastructure, auto-scaling/sharding, and private networking options (VPC Peering, PrivateLink, PSC, Transit Gateway).

---

### Question 8
A team is launching one small internal cache database. Lowest cost is the priority, and there is no requirement to host multiple databases in one subscription or use private networking. Which subscription is the best fit?

- **A.** Pro
- **B.** Pro with Active-Active enabled
- **C.** Essentials (Free)
- **D.** Essentials with Redis Flex

**Correct answer:** C

> **Why:** **Essentials (Free)** provides a zero-cost, single small database tier ideal for lightweight internal caches, development, and testing when Pro features are unnecessary.

---

### Question 9
A company wants to isolate billing, capacity planning, and operational blast radius for a new critical inventory database that is expected to consume substantial memory and throughput. What is the best recommendation?

- **A.** Create a new dedicated Pro subscription for the inventory database.
- **B.** Place the inventory database in an Essentials subscription to isolate it.
- **C.** Add the database to the existing Pro subscription and lower its throughput setting.
- **D.** Add it to the existing Pro subscription and size memory and throughput appropriately.

**Correct answer:** A

> **Why:** Because all databases inside a single Pro subscription share the underlying subscription cluster infrastructure and billing boundary, creating a **new dedicated Pro subscription** provides complete infrastructure, billing, and blast-radius isolation for a heavy workload.

---

### Question 10
An operator wants the strongest possible separation between development, QA, and production so each environment can be scaled, changed, or retired without sharing a subscription with the others. All three environments also need Pro-tier capabilities. Which setup best fits?

- **A.** Use one Pro subscription for development and QA, and a second Pro subscription for production.
- **B.** Use separate Pro subscriptions for development, QA, and production.
- **C.** Use one Pro subscription with three databases, one for each environment.
- **D.** Use paid Essentials subscriptions for development and QA, and one Pro subscription for production.

**Correct answer:** B

> **Why:** Using **separate Pro subscriptions for development, QA, and production** ensures full lifecycle independence, separate network/VPC boundaries, and zero noisy-neighbor contention across environments while retaining Pro features in all three.

---

### Question 11
A platform team supports two unrelated business units that want separate billing ownership and strict blast-radius isolation between their Redis Cloud environments. Which approach best matches Redis Cloud guidance?

- **A.** Use one shared Pro subscription and separate the units with console users and billing tags.
- **B.** Use separate Pro subscriptions for the two business units.
- **C.** Use one Pro subscription with separate databases for each unit and rely on subscription-level alerts.
- **D.** Use one Pro subscription with separate private connections for each unit.

**Correct answer:** B

> **Why:** In Redis Cloud, payment methods, billing ownership, and underlying cluster VMs are scoped at the **subscription level**. Separate **Pro subscriptions** are required to isolate billing and operational blast radius between business units.

---

### Question 12
An engineer asks why overloading one Pro subscription with many databases can still create issues even though each database has its own memory and throughput settings. What should the operator explain?

- **A.** Each database in a Pro subscription is pinned to a separate private network, so contention comes from DNS limits.
- **B.** A Pro subscription is backed by shared subscription infrastructure, so its databases can still contend for resources.
- **C.** A Pro subscription stores metadata only, while the databases run in Essentials infrastructure.
- **D.** Each Pro database gets a completely separate backend cluster even within the same subscription, so only endpoint settings are shared.

**Correct answer:** B

> **Why:** Databases within the same Pro subscription run on **shared subscription cluster infrastructure** (nodes/VMs and network interfaces), meaning excessive databases or spikes in one database can contend for underlying cluster resources.

---

### Question 13
A workload must start as a multi-region writable Redis Cloud deployment and the team does not yet have an existing subscription. Which plan is most correct?

- **A.** Create a standard single-region Pro database first, then convert that database into an Active-Active deployment without creating an Active-Active subscription.
- **B.** Create a new Pro database, choose Custom settings, and enable Active-Active (Multi-region).
- **C.** Start with an Essentials database, then migrate it into an Active-Active deployment when traffic grows.
- **D.** Use Multi-AZ in one region because it provides geo-distributed multi-region writes without Active-Active.

**Correct answer:** B

> **Why:** **Active-Active (CRDB)** multi-region writable deployments are a **Pro** capability that must be selected during creation (via **Pro -> Custom settings -> Enable Active-Active / Multi-region**); standard single-region databases cannot be converted in place to Active-Active.

---

### Question 14
A team will use Redis Cloud for session data and API responses that can be rebuilt from the primary database, prioritizing lowest cost over durable recovery. Which starting configuration direction is the best fit?

- **A.** Increase Query Performance Factor to reduce the risk of data loss.
- **B.** Start without replication or persistence unless a separate availability requirement justifies it.
- **C.** Enable Multi-AZ and AOF on every write because all Redis data should be treated as permanent.
- **D.** Use Active-Active across regions so rebuilt data survives any outage.

**Correct answer:** B

> **Why:** Ephemeral cache data that can be easily reconstructed from a backend system of record does not require the extra 2x memory cost of replication or disk I/O overhead of persistence unless high availability SLAs demand replication.

---

### Question 15
A product team will store shopping cart and profile data in Redis Cloud as a primary operational store, prioritizing durability and recovery rather than lowest cost. Which configuration direction is the best fit?

- **A.** Disable persistence and rely on remote backup only.
- **B.** Enable high availability (replication / Multi-AZ) and data persistence.
- **C.** Leave replication and persistence off so the database stays single-copy.
- **D.** Use `noeviction` as the main durability control.

**Correct answer:** B

> **Why:** When Redis Cloud serves as a primary system of record, enabling both **high availability (replication + Multi-AZ)** for automatic failover and **data persistence (AOF / snapshots)** + **noeviction** protects against both node failures and data loss.

---

### Question 16
A team is creating a Redis 8.4 Pro database that will use **Search and Query** heavily. What should the operator know about sizing and enabling this capability?

- **A.** Search and Query does not materially affect sizing, so creation can be based only on base dataset size.
- **B.** Search and Query cannot be used on Redis 8.4 unless Query Performance Factor is configured first.
- **C.** Search and Query must be enabled later from database settings after the initial database is created.
- **D.** Search and Query is included by default on Redis 8.x, so sizing should account for index size and query throughput.

**Correct answer:** D

> **Why:** Starting with Redis 8.x, **Search and Query** capabilities are built in by default. Because secondary indexes consume additional RAM alongside the keys themselves, operators must size the database memory to accommodate both the **dataset and the search indexes**.

---

### Question 17
A team is using Search and Query heavily on a document database. The operator is willing to allocate more compute/memory resources to speed up search queries without changing the data model. Which setting is intended for that tradeoff?

- **A.** Change the eviction policy to `noeviction`
- **B.** Increase the remote backup frequency
- **C.** Increase the Query Performance Factor
- **D.** Enable Multi-AZ for the database

**Correct answer:** C

> **Why:** The **Query Performance Factor (QPF)** multiplier in Redis Cloud provisions additional shards/CPU cores specifically to accelerate secondary index scanning and Search & Query throughput.

---

### Question 18
In the Redis Cloud UI, the operator enters a **60 GB** dataset size and chooses a **highly available (replicated)** database. What total memory requirement should they expect Redis Cloud to calculate behind the scenes?

- **A.** About **120 GB** of total memory required
- **B.** About 30 GB of total memory because replication compresses the second copy
- **C.** About 60 GB of total memory because dataset size already includes the replica
- **D.** About 60 GB of RAM plus a separate 60 GB only if AOF is enabled

**Correct answer:** A

> **Why:** Enabling replication (High Availability) maintains a full in-memory replica for every primary shard, **doubling** the total RAM required ($60\text{ GB primary} + 60\text{ GB replica} = 120\text{ GB total}$).

---

### Question 19
An operations team wants client traffic to continue being served automatically if one cloud availability zone (AZ) in the region experiences an outage. Which setting directly addresses that requirement?

- **A.** Increase the Query Performance Factor
- **B.** Choose Multi-AZ during database creation
- **C.** Configure remote backup on a shorter interval
- **D.** Disable eviction

**Correct answer:** B

> **Why:** **Multi-AZ** places primary shards and their corresponding replica shards in **different cloud Availability Zones** within the same region so an entire AZ failure triggers automatic failover to replicas in healthy AZs.

---

### Question 20
A database already has enough dataset size (memory headroom), but rising traffic means the provisioned operations per second (throughput) are no longer sufficient. What is the best scaling response?

- **A.** Increase throughput without increasing dataset size.
- **B.** Increase both dataset size and throughput even though memory is already sufficient.
- **C.** Add replica shards and keep throughput the same because replication increases primary write capacity.
- **D.** Increase dataset size only because throughput will scale only with memory.

**Correct answer:** A

> **Why:** Redis Cloud Pro allows **decoupled scaling of throughput (ops/sec) and dataset size (GB)**. You can increase the provisioned throughput setting independently to add shards/compute without paying for unnecessary extra memory.

---

### Question 21
A production workload places the highest priority on minimizing the loss of recently acknowledged writes and is willing to accept extra write latency/overhead to get that protection. Which Redis Cloud data persistence setting best fits?

- **A.** Append-only file (AOF) every 1 second
- **B.** Snapshot every 1 hour
- **C.** No persistence
- **D.** Append-only file (AOF) on every write

**Correct answer:** D

> **Why:** **Append-only file (AOF) on every write (`appendfsync always`)** flushes every write operation to persistent disk storage before acknowledging it, offering the strongest durability (`RPO ≈ 0`) at the cost of higher write latency.

---

### Question 22
A cache database stores many keys without TTLs, and the team would rather evict older least-recently-used data across all keys than fail writes when memory is full. Which eviction policy best matches that goal?

- **A.** `allkeys-lru`
- **B.** `noeviction`
- **C.** `volatile-random`
- **D.** `volatile-lru`

**Correct answer:** A

> **Why:** **`allkeys-lru`** evicts the least-recently-used keys from the **entire keyspace** regardless of whether a TTL (`EXPIRE`) is set, whereas `volatile-*` policies only evict keys that have a TTL configured.

---

### Question 23
A company wants a continuously synchronized replica database in another location for disaster recovery, and that target database should remain **read-only** until promoted during a DR event. Which feature is the best fit?

- **A.** Remote backup
- **B.** Active-Passive (`Replica Of`)
- **C.** Active-Active
- **D.** Multi-AZ

**Correct answer:** B

> **Why:** **Active-Passive (`Replica Of`)** continuously replicates data from a source database to one or more read-only target databases (including across regions or subscriptions) for disaster recovery and read offloading.

---

### Question 24
A company's disaster-recovery policy requires restores to come from scheduled point-in-time copies stored in an external cloud object-storage bucket (such as Amazon S3, Google Cloud Storage, or Azure Blob Storage). Which feature should the operator configure?

- **A.** Append-only file every 1 sec
- **B.** Snapshot persistence every 1 hour
- **C.** Remote backup to a supported external target
- **D.** Active-Passive replication to a standby database

**Correct answer:** C

> **Why:** **Remote backups** export scheduled RDB backup files to customer-managed external cloud storage buckets (S3, GCS, Azure Blob Storage, or FTP/SFTP) for off-cluster retention and disaster recovery.

---

## Domain 3: Security, Access Control (RBAC / ACLs) & Compliance

### Question 25
During an audit, a customer asks who is responsible for patching the operating systems in the **customer's application environment** (or contrastingly, the Redis Cloud cluster nodes) under the shared responsibility model. Which answer is correct?

- **A.** The customer and cloud provider only
- **B.** The public cloud provider
- **C.** The customer *(for client/application VMs)* / **D. Redis** *(for Redis Cloud cluster OS nodes)*
- **D.** Redis

**Correct answer:** C *(or **D** if the question text reads "patching the operating systems that run the Redis Cloud environment")*

> **Why:** Under the Redis Cloud Shared Responsibility Model:
> - **Redis** is responsible for patching and maintaining the **operating systems and Redis software of the managed Redis Cloud cluster nodes**.
> - **The customer** is responsible for patching the **operating systems, runtimes, and client libraries in their own application environment**.

---

### Question 26
A security team wants an employee to sign in to the Redis Cloud console and see subscription and database details, without being able to create, modify, or delete resources or billing. Which console role is the least-privileged option that still allows that read-only access?

- **A.** Manager
- **B.** Owner
- **C.** Viewer
- **D.** Reader

**Correct answer:** C

> **Why:** The Redis Cloud console RBAC roles are **Owner**, **Member**, **Manager**, **Billing Admin**, and **Viewer**. The **Viewer** role provides read-only visibility into subscriptions and databases in the console.

---

### Question 27
A company uses local Redis Cloud console accounts rather than SAML SSO and wants those users to enforce Multi-Factor Authentication (MFA) and user access policies. Which console role can manage user accounts and account-level settings?

- **A.** An account Owner
- **B.** The cloud provider account administrator
- **C.** Any Viewer
- **D.** Any database user with a Full-Access ACL

**Correct answer:** A

> **Why:** Only an **account Owner** in the Redis Cloud console has permissions to manage team users, roles, SSO/authentication settings, and account-wide security configuration.

---

### Question 28
A company already uses **Okta** to centralize authentication for internal apps and wants Redis Cloud console users to authenticate through that centralized identity provider. Which approach best fits?

- **A.** Share one Owner account among administrators
- **B.** Configure SAML SSO
- **C.** Ask each user to create a social login
- **D.** Use database ACLs instead of console authentication

**Correct answer:** B

> **Why:** Redis Cloud supports enterprise **SAML 2.0 Single Sign-On (SSO)** integration with identity providers such as Okta, Microsoft Entra ID (Azure AD), JumpCloud, and OneLogin for centralized console authentication and role mapping.

---

### Question 29
An operator plans to convert an existing Redis Cloud console user to social login (Google/GitHub OAuth) or migrate their authentication method. What caveat should the operator explain first?

- **A.** The migration automatically removes the user's database access and ACL assignments.
- **B.** The user must be deleted and recreated before social login can be enabled.
- **C.** The change cannot be reverted once the user is migrated.
- **D.** The migration automatically converts the user to an account Owner.

**Correct answer:** A

> **Why:** Converting a local console user account to social login or changing its authentication binding resets/removes associated database-level access/ACL links, requiring the operator to review permissions before migrating.

---

### Question 30
A team needs one application user to run only approved Redis commands (e.g., `+@read`) against a specific subset of keys (e.g., `~app1:*`) in a database. Which Redis Cloud access control model supports that requirement?

- **A.** Console roles such as Owner and Viewer
- **B.** CIDR allow lists on the database endpoint
- **C.** Users assigned to roles, with roles defined by ACL rules
- **D.** MFA for Redis Cloud console users

**Correct answer:** C

> **Why:** Data-plane access in Redis Cloud is governed by **Redis ACLs**: you define **ACL rules** (command categories `+@read`/`-@dangerous` and key patterns `~prefix:*`), group them into **Roles**, and assign those roles to **Database Access Control Users**.

---

### Question 31
A new database is created, named database users and least-privilege ACL roles are configured, and the application has been updated to connect using its named user. What is the recommended security next step?

- **A.** Disable the `default` database user
- **B.** Rotate the `default` database user's password and keep it for normal application access
- **C.** Keep the `default` database user enabled as a shared fallback alongside the named users
- **D.** Assign the `default` database user the same ACL role as the named application user

**Correct answer:** A

> **Why:** Every new Redis database starts with a `default` user that has full access (`+@all ~*`). Once named application users with least-privilege ACL roles are in place, security best practice is to **disable the `default` user** (or restrict it) so no client can connect with broad default credentials.

---

### Question 32
A team must keep using the database's **public endpoint** for now. Which guidance best matches Redis Cloud security best practices?

- **A.** Disable TLS to reduce latency and rely only on passwords
- **B.** Use the public endpoint without restrictions because Redis Cloud is managed
- **C.** Enable TLS and restrict access with a CIDR allow list
- **D.** Add more console Owners so endpoint changes can be reviewed

**Correct answer:** C

> **Why:** If a public endpoint must be used, you should always **enable TLS (encryption in transit, including mTLS if supported)**, enforce strong ACL authentication, and configure a **source IP/CIDR allow list** (security groups) so only trusted application IPs can reach the endpoint.

---

### Question 33
A compliance reviewer asks how **encryption at rest** works in Redis Cloud. What should the operator explain?

- **A.** Encryption at rest happens only on public endpoints.
- **B.** Redis Cloud deployments are always encrypted at rest, and data is written to disk when persistence or backups are enabled.
- **C.** Encryption at rest happens only when TLS is enabled.
- **D.** Encryption at rest requires a custom ACL with write privileges.

**Correct answer:** B

> **Why:** Redis Cloud encrypts all underlying storage volumes and backup artifacts **at rest by default** (using cloud provider disk encryption / AES-256, with optional Customer-Managed Keys on Pro), protecting any data written to disk via persistence (AOF/RDB) or backups.

---

### Question 34
An engineer who has managed ACLs in self-managed Redis OSS assumes the exact same `ACL` commands (`ACL SETUSER`, `ACL SAVE`, etc.) work identically from a client connected to Redis Cloud. What should the operator explain?

- **A.** ACL behavior carries over unchanged, but only console Owners can apply it.
- **B.** Redis Cloud supports ACLs, but some direct `ACL` commands/operations are restricted because ACLs are centrally managed by the service control plane.
- **C.** ACLs are supported only on Essentials subscriptions.
- **D.** Redis Cloud does not support ACLs at all.

**Correct answer:** B

> **Why:** In Redis Cloud, ACL users and roles are managed through the **Redis Cloud Console, REST API, or Terraform/Pulumi** so the control plane can synchronize ACLs across all shards and proxies; consequently, direct mutating `ACL` commands over the client connection are restricted.

---

## Domain 4: Private Networking & Cloud Connectivity

### Question 35
A production application runs in the same cloud provider as a Redis Cloud Pro subscription, and the security team requires that database traffic **never traverse the public internet**. Which endpoint and connection path should the operator recommend?

- **A.** Private endpoint (via VPC Peering, PrivateLink, PSC, or Transit Gateway)
- **B.** REST API endpoint
- **C.** Public endpoint with a stronger password
- **D.** Public endpoint with no allow list

**Correct answer:** A

> **Why:** Using a **Private endpoint** over private cloud networking keeps all client-to-database traffic entirely on the cloud provider's private backbone network.

---

### Question 36
A team on an **Essentials** subscription in AWS asks for a private database endpoint (VPC Peering or PrivateLink) for an internal service. What should the operator explain?

- **A.** Essentials can use a private endpoint if the database is recreated with Multi-AZ.
- **B.** Private endpoints and private connectivity options are available only with **Pro** subscriptions.
- **C.** Essentials can use a private endpoint after upgrading only the database settings, not the subscription.
- **D.** Essentials can make the public endpoint private by adding a CIDR allow list.

**Correct answer:** B

> **Why:** **Private networking** (VPC Peering, AWS PrivateLink, GCP Private Service Connect, Azure Private Link, AWS Transit Gateway) requires dedicated VPC infrastructure and is available **only on Redis Cloud Pro subscriptions**.

---

### Question 37
An AWS team enters the Redis Cloud VPC CIDR and the application VPC CIDR during **VPC peering** setup and accepts the peering request in AWS, but connectivity still cannot be established. What is the most likely cause?

- **A.** The two VPC CIDR ranges overlap.
- **B.** The database still has its public endpoint enabled.
- **C.** The database is configured with replication.
- **D.** The peering request was accepted, but no one added the **route-table entries** yet.

**Correct answer:** D

> **Why:** Accepting an AWS VPC peering connection only establishes the link; traffic will not flow until the customer **updates their application VPC route tables** to route the Redis Cloud VPC CIDR block through the `pcx-...` peering connection ID.

---

### Question 38
After initiating AWS VPC peering from Redis Cloud, the application team accepts the peering request in their AWS account. What step is still required before traffic can route correctly?

- **A.** Import the Redis Grafana dashboards so the team can confirm the peering setup visually.
- **B.** Update the application VPC route tables so the Redis Cloud VPC CIDR routes through the peering connection.
- **C.** Rotate the database password and reconnect the clients through the new private path.
- **D.** Enable Multi-AZ on the database so traffic can fail over across availability zones automatically.

**Correct answer:** B

> **Why:** Both VPCs must know how to route packets to each other. Redis Cloud automatically configures its side, and the customer must **add a route in their application VPC route table(s)** pointing the Redis Cloud CIDR to the VPC Peering target.

---

### Question 39
A security reviewer objects to **VPC peering** because it creates broad VPC-to-VPC network reachability instead of service-level isolation. Which characteristic of VPC peering are they highlighting?

- **A.** VPC peering allows network routing between the two VPCs at the network layer, not just unidirectional access to a single specific service endpoint.
- **B.** VPC peering exposes only a single managed service endpoint instead of opening VPC-level routing.
- **C.** VPC peering always sends the traffic over the public internet unless TLS is enabled.
- **D.** VPC peering is limited to Essentials databases that do not use other private connectivity options.

**Correct answer:** A

> **Why:** **VPC Peering** connects two VPC networks bidirectionally at Layer 3 (and requires non-overlapping CIDRs), whereas **AWS PrivateLink / GCP Private Service Connect** exposes only the specific Redis Cloud service endpoint unidirectionally into the consumer VPC.

---

### Question 40
A **Google Cloud (GCP)** deployment needs private connectivity to Redis Cloud, but the application VPC CIDR overlaps with the default CIDR and the security team does not want full VPC-to-VPC exposure. Which option best fits?

- **A.** Multi-AZ
- **B.** Private Service Connect (PSC)
- **C.** Public endpoint with TLS
- **D.** VPC Peering

**Correct answer:** B

> **Why:** On Google Cloud, **Private Service Connect (PSC)** provides private, unidirectional, service-level connectivity that **tolerates overlapping VPC CIDR ranges** and avoids full VPC-to-VPC peering trust.

---

### Question 41
An **AWS** platform team needs a regional **hub-and-spoke** connectivity model that can connect many spoke VPCs and on-premises networks to Redis Cloud, and is willing to pay more for the added routing flexibility. Which option best matches that requirement?

- **A.** AWS PrivateLink
- **B.** CIDR allow list
- **C.** VPC Peering
- **D.** AWS Transit Gateway

**Correct answer:** D

> **Why:** **AWS Transit Gateway (TGW)** acts as a regional cloud router for hub-and-spoke topologies, allowing multiple spoke VPCs and VPN/Direct Connect networks to reach Redis Cloud through a central transit hub.

---

### Question 42
An **AWS** security team wants private Redis Cloud connectivity that **tolerates overlapping CIDR ranges** and exposes **only the specific Redis service endpoint** instead of peering the entire VPC. Which option most directly matches that requirement?

- **A.** Public endpoint with TLS and CIDR allow list
- **B.** AWS Transit Gateway
- **C.** AWS PrivateLink
- **D.** VPC Peering

**Correct answer:** C

> **Why:** **AWS PrivateLink** projects an Elastic Network Interface (ENI) endpoint directly into the customer's AWS VPC, allowing private unidirectional connections to Redis Cloud even when VPC CIDRs overlap and without exposing the entire VPC.

---

### Question 43
An operator asks why **private endpoints** are generally preferred over public endpoints for production workloads in Redis Cloud. Which explanation is the best fit?

- **A.** Private endpoints automatically work even when no private connectivity option is configured.
- **B.** Private endpoints remove the need for TLS or database authentication on client connections.
- **C.** Private endpoints are equally available on Essentials without changing the subscription tier.
- **D.** Private endpoints keep traffic on the cloud provider's internal network instead of exposing it to the public internet.

**Correct answer:** D

> **Why:** Private endpoints eliminate exposure to the public internet by keeping all data-plane traffic inside the cloud provider's private network backbone, reducing both attack surface and internet routing hops.

---

## Domain 5: Observability, Prometheus & Grafana Monitoring

### Question 44
A Pro subscription already has a private connectivity option configured. **Prometheus** is running on an engineer's local laptop outside that private network, so metric scraping fails. What is the best fix?

- **A.** Keep Prometheus on the laptop and add its IP to the database CIDR allow list.
- **B.** Ask Redis support to expose the metrics endpoint publicly instead of using the existing private network.
- **C.** Deploy Prometheus in a network that can reach the subscription through the private connectivity option.
- **D.** Point Prometheus at the public database endpoint instead of the internal Prometheus metrics endpoint.

**Correct answer:** C

> **Why:** The Redis Cloud Prometheus metrics endpoint (`:8070`) is **only exposed on the internal/private cluster network**. Therefore, the Prometheus server must be deployed inside a VPC/network connected to the Pro subscription via VPC Peering, PrivateLink, PSC, or Transit Gateway.

---

### Question 45
An operator reviewing an **Essentials** deployment asks why the Redis-provided Prometheus and Grafana external scraping workflow is not available. What should the operator explain?

- **A.** Essentials supports that workflow only if replication is disabled.
- **B.** Essentials supports that workflow only after enabling TLS.
- **C.** That Redis-provided Prometheus/Grafana scraping workflow is available on **Pro**, not Essentials.
- **D.** Grafana can scrape Essentials directly without Prometheus.

**Correct answer:** C

> **Why:** The dedicated Prometheus metrics exporter endpoint (`:8070`) and private network scraping workflow are features of **Redis Cloud Pro** subscriptions (which run on dedicated cluster nodes), whereas Essentials uses shared multi-tenant infrastructure and provides metrics in the Redis Cloud Console UI.

---

### Question 46
A Prometheus administrator is configuring the Redis Cloud scrape target and must choose the correct endpoint and port. Which target is correct?

- **A.** The REST API URL for the database
- **B.** The Redis Cloud console URL over HTTPS on port `443`
- **C.** The internal cluster address over HTTPS on port **`8070`**
- **D.** The public database endpoint on the database port

**Correct answer:** C

> **Why:** Redis Cloud Pro exposes its Prometheus metrics exporter (`redis_exporter` / cluster metrics) on the **internal cluster master address over HTTPS on port `8070`**.

---

### Question 47
An operator wants to scrape the Redis Cloud Prometheus endpoint from the public internet. What should they know?

- **A.** The Prometheus endpoint becomes public after Grafana is configured.
- **B.** The Prometheus endpoint is **not exposed on the public network**, so they must use private connectivity.
- **C.** The Prometheus endpoint can be scraped publicly as long as TLS is enabled.
- **D.** The Prometheus endpoint is reachable through the same public hostname used for normal client traffic.

**Correct answer:** B

> **Why:** For security reasons, the Redis Cloud Prometheus metrics port (`8070`) is never exposed to the public internet; scraping requires private network connectivity to the internal cluster address.

---

### Question 48
Metrics are already being scraped successfully into Prometheus. The operator now wants prebuilt visualizations for database and subscription status. What should they do next?

- **A.** Configure Grafana as the scrape target and have Prometheus query dashboards from it.
- **B.** Configure Grafana to query the Redis Cloud REST API directly instead of Prometheus.
- **C.** Repoint Prometheus from the metrics endpoint to the public database endpoint so Grafana can read keys.
- **D.** Configure Prometheus as a data source in Grafana and import the official Redis Cloud dashboards.

**Correct answer:** D

> **Why:** In the Prometheus + Grafana monitoring architecture, **Prometheus** scrapes and stores time-series metrics from Redis Cloud (`:8070`), and **Grafana** connects to **Prometheus as a data source** using the official **Redis Cloud Grafana dashboard templates** (Subscription and Database dashboards).

---

### Question 49
A platform team wants threshold-based alerting, long-term capacity visibility, and the ability to correlate Redis Cloud metrics in their existing observability stack (Datadog, Grafana, PagerDuty, etc.). Which approach best fits?

- **A.** Scrape the Redis Cloud Prometheus endpoint and send those metrics into the team's external observability stack.
- **B.** Rely on the Redis Cloud console alone and review metrics manually instead of exporting them.
- **C.** Poll `redis-cli` on a schedule and treat the command output as the primary observability pipeline.
- **D.** Use remote backup history and scheduled export reports as the main source for alerting.

**Correct answer:** A

> **Why:** Scraping the **Prometheus endpoint (`:8070`)** provides rich, real-time cluster, shard, and database telemetry that integrates natively with Prometheus Alertmanager, Grafana, Datadog, and other enterprise observability platforms for long-term retention and alerting.

---

### Question 50
A team has already configured a private connectivity option and asks where the Prometheus server should be placed to scrape Redis Cloud metrics. Which answer is best?

- **A.** On any laptop with internet access
- **B.** On a bastion host that can reach only the public database endpoint, but not the internal cluster address
- **C.** Inside the Redis Cloud console as a built-in monitoring service for the subscription
- **D.** In a network that can reach the internal cluster address through that private connectivity option

**Correct answer:** D

> **Why:** Because the Prometheus metrics endpoint is bound to the **internal cluster address on port `8070`**, the Prometheus server must run inside a VPC/VNet that routes to the internal cluster address via the configured private connectivity option.

---

## Domain 6: Automation (REST API, Terraform, Pulumi) & Data Modeling

### Question 51
A team needs to automate a newly released Redis Cloud capability before the official Terraform or Pulumi providers are updated. Which automation interface is most likely to support it first?

- **A.** Redis Insight
- **B.** Pulumi provider
- **C.** Redis Cloud REST API
- **D.** Terraform provider

**Correct answer:** C

> **Why:** Both the Terraform provider and Pulumi provider are built on top of the **Redis Cloud REST API**. New platform capabilities are exposed in the **REST API** first before downstream IaC providers wrap them.

---

### Question 52
A CI pipeline can create Redis Cloud resources when run from an engineer's laptop, but the exact same API call fails from a shared cloud build runner. The operator recently tightened API key security as a best practice. What is the most likely explanation?

- **A.** The build runner's IP is not included in the API key's allowed CIDR list.
- **B.** CIDR allow lists apply only to database endpoints, not REST API keys.
- **C.** API keys created for one user account cannot be used from CI systems.
- **D.** Shared runners can use Redis Cloud only through Terraform or Pulumi, not directly through the REST API.

**Correct answer:** A

> **Why:** Redis Cloud REST API keys support **HTTP source IP/CIDR allow lists**. If an operator restricts an API key to office/VPN CIDR ranges, requests from external shared CI/CD runners whose IPs are not allow-listed will be rejected with `403 Forbidden`.

---

### Question 53
A `POST` Cloud API request to create a Pro subscription returns `202 Accepted` successfully with a `taskId`. How should the automation script track that asynchronous provisioning request to completion?

- **A.** Test the database endpoint directly to infer whether the subscription task is done.
- **B.** Poll `GET /tasks/{taskId}` until the task status reaches `processing-completed`.
- **C.** Re-send the `POST` request every few minutes until provisioning finishes.
- **D.** Poll the subscriptions list and treat the new subscription appearing as the final completion signal.

**Correct answer:** B

> **Why:** Mutating operations in the Redis Cloud REST API are **asynchronous** and return a `taskId`. Clients must poll **`GET /tasks/{taskId}`** until the task transitions to `processing-completed` (and inspect `response.resourceId` or `response.error`).

---

### Question 54
An operator wants an Infrastructure-as-Code (IaC) tool for Redis Cloud, prefers writing infrastructure definitions in **Python or JavaScript/TypeScript**, and does not want to use HCL. Which tool is the best fit?

- **A.** Swagger UI only
- **B.** Redis Cloud console
- **C.** Terraform
- **D.** Pulumi

**Correct answer:** D

> **Why:** **Pulumi** (via the `@pulumi/rediscloud` / `pulumi_rediscloud` package) lets teams define Redis Cloud infrastructure using general-purpose programming languages such as **Python, TypeScript/JavaScript, Go, and C#**, whereas Terraform uses HashiCorp Configuration Language (HCL).

---

### Question 55
An operator wants to preview and review the infrastructure changes **Terraform** intends to make to Redis Cloud before actually applying them. What is the best practice?

- **A.** Create the subscription manually in the console first so Terraform has a target to import.
- **B.** Skip straight to `terraform apply` because Redis Cloud validates everything server-side.
- **C.** Poll `GET /tasks` before the first run to confirm Terraform can reach the API.
- **D.** Run `terraform plan` first to review the execution plan before applying.

**Correct answer:** D

> **Why:** Running **`terraform plan`** compares the desired HCL state against the current state and displays a dry-run diff of resources to be created, modified, or destroyed before any changes are executed.

---

### Question 56
An automation team wants Redis Cloud infrastructure changes to be repeatable, peer-reviewable before execution, and tracked in Git version control instead of being made manually in the console. Which approach best fits?

- **A.** Manage the infrastructure with an IaC workflow such as Terraform or Pulumi.
- **B.** Poll the tasks API regularly without defining the desired infrastructure state.
- **C.** Record the console steps in a runbook and repeat them manually for each environment.
- **D.** Use Redis Insight as the primary provisioning system for subscriptions and databases.

**Correct answer:** A

> **Why:** Declarative **Infrastructure-as-Code (IaC)** workflows using **Terraform** or **Pulumi** allow teams to store Redis Cloud configurations in Git, review `plan`/`preview` diffs in pull requests, and apply repeatable changes across environments.

---

### Question 57
A Terraform configuration must reference an **existing** Redis Cloud payment method (or cloud account) that was created outside of Terraform. Which Terraform construct should the operator use to read that existing object?

- **A.** An `output` block
- **B.** A `creation_plan` block
- **C.** A `resource` block
- **D.** A `data` source (`data "rediscloud_payment_method" ...`)

**Correct answer:** D

> **Why:** In Terraform, a **`data` source** queries and reads read-only attributes (like `id`) of existing infrastructure managed outside the current Terraform state, whereas a `resource` block creates and manages a new object.

---

### Question 58
A retailer sizes a Redis Cloud database based on average daily traffic and throughput today, then struggles during a flash sale when request volume spikes far above normal. Which capacity-planning dimension was most underestimated?

- **A.** Data relationships
- **B.** Key naming conventions
- **C.** Data velocity (peak throughput / ops per second)
- **D.** MFA enforcement

**Correct answer:** C

> **Why:** **Data velocity** measures the rate at which data is read and written (specifically **peak operations per second** during traffic spikes like flash sales). Sizing only for average throughput causes saturation under peak load.

---

### Question 59
A gaming application needs a leaderboard that can return players in rank order and update player scores frequently in $O(\log N)$ time. Which Redis data structure is the best fit?

- **A.** List
- **B.** Sorted Set (`ZSET`)
- **C.** Hash
- **D.** Set

**Correct answer:** B

> **Why:** A **Sorted Set (`ZSET`)** maintains unique members (`playerId`) ordered automatically by a floating-point `score`, supporting fast score updates (`ZADD`/`ZINCRBY`) and rank/range queries (`ZRANGE`, `ZREVRANK`).

---

### Question 60
An operator needs to store flat user profile fields such as `first_name`, `last_name`, `email`, and `loyalty_tier` under a single key (e.g., `user:1001`) with individual field-value access. Which Redis data structure is the best fit?

- **A.** Hash
- **B.** List
- **C.** Set
- **D.** Sorted Set

**Correct answer:** A

> **Why:** A **Redis Hash** maps field names to values under a single key (`HSET`, `HGET`, `HMGET`, `HGETALL`), providing memory-efficient storage and individual field reads/writes for flat object attributes.

---

### Question 61
A product catalog record contains deeply **nested arrays and objects**, and the team wants to store and retrieve partial nested paths directly using JSONPath syntax. Assuming the database has the needed capability enabled, which structure is the best fit?

- **A.** String with client-side JSON serialization
- **B.** Hash
- **C.** JSON Document (`RedisJSON`)
- **D.** Sorted Set

**Correct answer:** C

> **Why:** **JSON Document (`RedisJSON` — `JSON.SET`, `JSON.GET`)** stores hierarchical JSON trees natively in Redis and allows reading or mutating nested sub-objects and arrays via JSONPath without fetching and re-serializing the entire document.

---

### Question 62
A service must track one boolean (`yes`/`no`) completion flag for each of millions of sequentially numbered users, and **memory efficiency** is the top priority. Which Redis data structure is the best fit?

- **A.** JSON Document
- **B.** Hash
- **C.** Bitmap
- **D.** Sorted Set

**Correct answer:** C

> **Why:** A **Bitmap** (`SETBIT`, `GETBIT`, `BITCOUNT`) stores each user's boolean flag as a single bit at their integer offset, tracking 10 million users in roughly **1.2 MB** of memory.

---

### Question 63
A marketing system needs to track the **unique** users who have redeemed a coupon so duplicate redemptions are prevented and membership can be checked in $O(1)$ time. Which Redis data structure is the best fit?

- **A.** List
- **B.** JSON Document
- **C.** Set
- **D.** Hash

**Correct answer:** C

> **Why:** A **Redis Set** (`SADD`, `SISMEMBER`, `SCARD`) stores an unordered collection of unique strings, automatically ignoring duplicates and providing $O(1)$ membership checks.

---

### Question 64
An operator reviewing a latency issue finds that the application stores **very large values** (multi-megabyte blobs) under single keys, causing event-loop blocking during reads and writes. What is the best recommendation for the application team?

- **A.** Move the same payloads into a Set so Redis treats them as smaller.
- **B.** Increase the key size until it reaches Redis's theoretical 512 MB maximum.
- **C.** Keep the values as they are and rely only on TTL to remove latency.
- **D.** Split the oversized values into smaller logical pieces across multiple keys or fields.

**Correct answer:** D

> **Why:** Because Redis command execution on a shard is single-threaded, reading or writing huge single-key values blocks other commands on that shard and spikes tail latency. **Splitting oversized values into smaller logical keys or Hash fields** keeps individual operations fast.

---

### Question 65
A developer wants to model relationships in Redis the same way they would in a relational database (using normalized tables and foreign keys). What should they do instead?

- **A.** Create normalized tables and foreign keys inside each Redis database.
- **B.** Store all related data in one very large value so the relationships are hidden inside it.
- **C.** Use structured key naming conventions and Redis data structures (such as Sets, Sorted Sets, Hashes, and JSON) to represent links and access patterns between related data.
- **D.** Rely on API endpoint names instead of storing relationships in Redis.

**Correct answer:** C

> **Why:** Redis is an in-memory key-value and data-structure store designed around **application access patterns**. Relationships are modeled using structured **key naming conventions** (e.g., `customer:42:orders` as a Set/Sorted Set of order IDs) or indexed fields with Search & Query rather than relational foreign-key joins.
