# ⚡ Redis Associate Cloud Operator — Last-Minute Cram & Cheat Sheet

[![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)](https://redis.io/)
[![Exam](https://img.shields.io/badge/Certification-Redis_Associate_Cloud_Operator-red?style=for-the-badge)](#-1-redis-cloud-architecture-sharding--failover)
[![Question Bank](https://img.shields.io/badge/Practice_Questions-65_MCQs-success?style=for-the-badge)](README.md)

High-yield, last-minute cram sheet for the **Redis Associate Cloud Operator Certification** exam. Covers DMC Proxy vs. OSS Cluster API, Essentials vs. Pro subscriptions, memory sizing & replication math, persistence & durability, RBAC & ACL security, private networking (VPC Peering, PrivateLink, PSC, Transit Gateway), Prometheus port `8070` & Grafana, REST API / Terraform / Pulumi automation, and Redis data structures.

---

## 🔴 1. Redis Cloud Architecture, Sharding & Failover

| Concept | How It Works in Redis Cloud | Exam Takeaway |
| :--- | :--- | :--- |
| **DMC (Data Management Controller) Proxy** | Default proxy layer sitting in front of shards. | Masks resharding, slot migrations, and replica failovers behind **one stable database endpoint** so standard clients need no updates. |
| **OSS Cluster API** | Optional mode that exposes Redis Cluster topology directly to clients. | **Requires cluster-aware clients** that handle `MOVED`/`ASK` slot redirections. |
| **Primary Shards (Horizontal Scaling)** | Partitions the 16,384 hash slots across multiple shards. | Each primary shard handles a **subset of the keyspace**; adding primary shards scales both **memory and write throughput**. |
| **Replica Shards (High Availability)** | Synchronous/asynchronous standby copies of primary shards. | Improves **availability** (automatic failover promotion on primary failure) but does **NOT** increase primary write capacity or writable dataset size. |
| **Multi-Key Operations & Transactions (`WATCH`/`MULTI`/`EXEC`)** | In a sharded database, all keys in a transaction must be on the same shard. | Use **hash tags** (e.g., `{user:100}:cart` and `{user:100}:orders`) so related keys hash to the **same slot**. |

---

## 🔴 2. Subscription Tiers: Essentials vs. Pro

| Feature / Requirement | Redis Cloud Essentials | Redis Cloud Pro |
| :--- | :--- | :--- |
| **Best Use Case** | Single small internal cache, dev/test, lowest cost (`Free` tier available). | Production workloads, multiple databases, high throughput, strict SLAs. |
| **Infrastructure** | Shared / multi-tenant (or fixed tiers). | **Dedicated cluster infrastructure** per subscription. |
| **Private Networking (VPC Peering, PrivateLink, PSC, TGW)** | ❌ **Not supported** | ✅ **Supported** |
| **Active-Active (Multi-Region Writable CRDB)** | ❌ **Not supported** | ✅ **Supported** (must enable during database creation via Custom settings). |
| **External Prometheus (`:8070`) & Grafana Scraping** | ❌ **Not supported** | ✅ **Supported** (over private connectivity). |
| **Subscription Isolation Rule** | N/A | All databases in **one Pro subscription share underlying cluster infrastructure**. Use **separate Pro subscriptions** to isolate dev/QA/prod, separate business units, or isolate a high-throughput workload's blast radius and billing. |

---

## 🔴 3. Sizing, Availability, Persistence & DR

### Memory, Throughput & Search Sizing
- **Replication Memory Math:** Choosing High Availability (Replication) **doubles total memory** ($60\text{ GB dataset} \times 2 = \mathbf{120\text{ GB}}$ total RAM).
- **Decoupled Throughput Scaling:** If memory is sufficient but ops/sec are saturated, **increase throughput without increasing dataset size**.
- **Peak Velocity Planning:** Always size for **Data Velocity** (peak ops/sec during flash sales/traffic spikes), not just daily averages.
- **Redis 8.x Search & Query:** Included by default on Redis 8.x; size memory for **dataset + index overhead**. To boost search speed without changing the data model, **increase the Query Performance Factor (QPF)**.

### High Availability, Persistence & Disaster Recovery
| Goal / Scenario | Recommended Redis Cloud Setting |
| :--- | :--- |
| **Survive a single cloud Availability Zone (AZ) outage** | Enable **Multi-AZ** during database creation. |
| **Ephemeral session/API cache (reconstructible, lowest cost)** | Start **without replication or persistence**; use **`allkeys-lru`** to evict older keys when full (even if keys lack TTLs). |
| **Primary operational database (shopping cart / profile store)** | Enable **High Availability (Replication + Multi-AZ)** + **Data Persistence** + `noeviction`. |
| **Minimize loss of recently acknowledged writes (`RPO ≈ 0`)** | **Append-Only File (AOF) on every write** (highest durability, extra write latency). |
| **Continuously synced read-only standby DB for DR** | **Active-Passive (`Replica Of`)**. |
| **Scheduled point-in-time recovery files in external cloud bucket** | **Remote backup** to a supported external target (S3, GCS, Azure Blob Storage). |

---

## 🔴 4. Security, RBAC, ACLs & Compliance

- **Shared Responsibility Model:**
  - **Redis** patches and manages the **Redis Cloud cluster nodes & OS**.
  - **The Customer** patches and manages **client/application OS environments**, configures ACLs, and secures client connections.
- **Console Access (Control Plane):**
  - **Owner:** Full administrative control; only role that can manage console users, roles, MFA, and SSO settings.
  - **Viewer:** Least-privileged **read-only** console role to view subscriptions and databases.
  - **Enterprise IdP (Okta, Entra ID):** Configure **SAML SSO**.
  - **Social Login Migration Caveat:** Converting a local user to social login **automatically removes the user's database access and ACL assignments**.
- **Database Access (Data Plane):**
  - Use **Users assigned to Roles, with Roles defined by ACL rules** (e.g., command subsets + key prefixes).
  - After configuring named application users, **disable the `default` database user**.
  - Some raw Redis OSS `ACL` client commands are restricted because Redis Cloud manages ACLs centrally via the control plane.
- **Encryption & Public Endpoint Hardening:**
  - **Encryption at Rest:** Always enabled by default on Redis Cloud; data is written to encrypted disk when persistence or backups are enabled.
  - **If using a Public Endpoint:** Always **enable TLS** and restrict source IPs with a **CIDR allow list**.

---

## 🔴 5. Private Networking Comparison (Pro Only)

| Connectivity Option | Cloud Provider | Key Characteristics & Exam Triggers |
| :--- | :--- | :--- |
| **VPC Peering** | AWS, GCP, Azure | Direct Layer-3 VPC-to-VPC routing. **Requires non-overlapping CIDRs.** After accepting peering, you **must update the application VPC route tables**! Note: Security teams may object that it grants **broad VPC-to-VPC network access** rather than single-service isolation. |
| **AWS PrivateLink** | AWS | Unidirectional **service-level endpoint**; **tolerates overlapping CIDRs**; does not expose the entire VPC. |
| **Private Service Connect (PSC)** | GCP | GCP's service-level private endpoint; **tolerates overlapping CIDRs** and avoids full VPC-to-VPC peering trust. |
| **AWS Transit Gateway (TGW)** | AWS | Regional **hub-and-spoke** router connecting multiple VPCs and on-premises networks to Redis Cloud (higher cost, maximum flexibility). |

---

## 🔴 6. Observability: Prometheus & Grafana

- **Tier Requirement:** External Prometheus scraping is available on **Redis Cloud Pro only** (not Essentials).
- **Target Endpoint & Port:** Scrape the **internal cluster address over HTTPS on port `8070`**.
- **Network Requirement:** Port `8070` is **never exposed on the public internet**. Prometheus must be deployed **inside a network connected to the Pro subscription via private connectivity** (VPC Peering, PrivateLink, PSC, or TGW).
- **Grafana Setup:** Configure **Prometheus as a data source in Grafana** and **import the official Redis Cloud dashboards**.

---

## 🔴 7. Automation (REST API, Terraform, Pulumi) & Data Modeling

### Automation & Infrastructure as Code (IaC)
| Scenario | Best Tool / Practice |
| :--- | :--- |
| **Automate a brand-new Redis Cloud feature on Day 1** | **Redis Cloud REST API** (updated before Terraform/Pulumi providers). |
| **Track async `POST` REST API requests to completion** | Poll **`GET /tasks/{taskId}`** until the task completes. |
| **CI build runner fails API calls after tightening API key security** | Add the **build runner's IP to the API key's allowed CIDR list**. |
| **IaC using Python or JavaScript/TypeScript (no HCL)** | **Pulumi**. |
| **Preview Terraform changes before applying** | Run **`terraform plan`** first. |
| **Reference an existing payment method created outside Terraform** | Use a Terraform **`data` source** (`data "rediscloud_payment_method"`). |

### Data Modeling Quick Reference
| Use Case | Best Redis Data Structure / Pattern |
| :--- | :--- |
| **Real-time gaming leaderboard (rank order + score updates)** | **Sorted Set (`ZSET`)** |
| **Flat user profile fields (`first_name`, `email`, `tier`) under one key** | **Hash** |
| **Product catalog with nested arrays/objects & partial path access** | **JSON Document (`RedisJSON`)** |
| **Yes/No boolean flag across millions of users (minimum memory)** | **Bitmap** (1 bit per user) |
| **Track unique coupon redemptions & $O(1)$ membership check** | **Set** |
| **High latency caused by huge single-key values** | **Split oversized values into smaller logical pieces across multiple keys** |
| **Model relationships between entities in Redis** | **Use key naming conventions and Redis data structures** to represent links (no relational foreign keys). |
