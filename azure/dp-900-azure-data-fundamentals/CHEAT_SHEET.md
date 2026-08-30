# ⚡ DP-900: Microsoft Azure Data Fundamentals — Cram & Cheat Sheet

[![Azure](https://img.shields.io/badge/Microsoft_Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Exam](https://img.shields.io/badge/Exam-DP--900-blue?style=for-the-badge)](#-high-frequency-exam-topics)

Quick-reference cheat sheet for **Microsoft Certified: Azure Data Fundamentals (DP-900)**. Designed for last-minute review, high-frequency topic disambiguation, and core concept mastery.

---

## 🔵 Cosmos DB APIs — Fast Memory Matrix

| API | Primary Data Model | Data Wire Format | Typical Use Case |
| :--- | :--- | :--- | :--- |
| **NoSQL (Core SQL)** | Document | JSON | Native API, JSON document storage, SQL querying |
| **Apache Gremlin** | Graph | Vertices & Edges | Social networks, relationship graphs, fraud rings |
| **MongoDB** | Document | BSON | Lift-and-shift existing MongoDB document apps |
| **Apache Cassandra** | Column-Family | Tabular / Column-family | Large-scale column-family writes, Cassandra migrations |
| **Table** | Key/Value | Key/Value entities | Low-cost key-value pairs, premium Table storage |

> [!IMPORTANT]
> **Key Exam Mnemonics**:
> - **G**remlin = **G**raph (Nodes/Vertices + Relationships/Edges).
> - **BSON** = **MongoDB**.
> - **Native / JSON** = **NoSQL API**.

---

## 🔵 Azure SQL Tiers & Deployment Models

| Deployment Option | Management Level | SQL Feature Parity | Serverless Option? | Primary Best Fit |
| :--- | :--- | :--- | :---: | :--- |
| **Azure SQL Database** | Fully Managed (PaaS) | Subset of SQL Server | ✅ Yes | Modern cloud-native apps, single DB, elastic pools |
| **Azure SQL Managed Instance** | Fully Managed (PaaS) | ~100% SQL Server | ❌ No | Lift-and-shift legacy on-prem SQL apps with cross-DB / SQL Agent |
| **SQL Server on Azure VM** | Self-Managed (IaaS) | 100% (Full control) | ❌ No | OS-level access needed, specific SQL version, non-PaaS third-party tools |
| **Azure SQL Edge** | Small-Footprint Container | Optimized subset | ❌ No | IoT edge gateways, streaming time-series data |

---

## 🔵 Azure Blob Storage Types & Access Tiers

### Blob Types
- **Block Blob**: Standard unstructured files (documents, images, videos, backups). Made of blocks that can be updated independently.
- **Append Blob**: Optimized for append-only operations (log files, continuous telemetry). Blocks can only be added to the end (no edit/delete).
- **Page Blob**: Collection of 512-byte pages optimized for random read/write operations. Used for Azure Virtual Machine Virtual Hard Disks (VHDs).

### Access Tiers
| Tier | Access Frequency | Storage Cost | Retrieval Cost | Availability / Retrieval Time |
| :--- | :--- | :--- | :--- | :--- |
| **Hot** | Daily / Active | Highest | Lowest | Immediate (milliseconds) |
| **Cool** | Infrequent (≥ 30 days) | Lower | Moderate | Immediate (milliseconds) |
| **Cold** | Rarely (≥ 90 days) | Low | High | Immediate (milliseconds) |
| **Archive** | Yearly / Retained (≥ 180 days) | Lowest | Highest | **Hours** (rehydration required) |

---

## 🔵 File Formats: Columnar vs Row-Based

| Format | Storage Layout | Best Used For |
| :--- | :--- | :--- |
| **Parquet** | ✅ **Columnar** | Big data analytics, Spark, Synapse, Power BI querying |
| **ORC** | ✅ **Columnar** | Optimized Row Columnar for Hive, Spark, analytical workloads |
| **Avro** | ❌ **Row-Based** | Event streaming pipelines (Kafka, Event Hubs), schema evolution |
| **CSV / TSV** | ❌ **Row-Based** | Plain-text delimited data exchange |
| **JSON** | ❌ **Semi-Structured** | Hierarchical document exchange, web APIs |

---

## 🔵 Transactional (OLTP) vs Analytical (OLAP)

| Characteristic | OLTP (Transactional) | OLAP (Analytical) |
| :--- | :--- | :--- |
| **Primary Goal** | Fast transaction processing (CRUD) | Deep historical analysis and reporting |
| **Schema Design** | Highly **Normalized** (3NF) | Highly **Denormalized** (Star / Snowflake) |
| **Data Scope** | Current, live operational data | Consolidated multi-year historical data |
| **Workload Type** | High-volume single-row reads & writes | Low-volume multi-million row aggregate scans |
| **Azure Example** | Azure SQL Database | Azure Synapse Analytics Dedicated SQL Pool |

---

## 🔵 Azure Analytics Ecosystem Summary

- **Azure Data Factory (ADF)**: Code-free ETL/ELT pipeline orchestration with event triggers.
  - *Order of creation:* **Linked Service** (connection) ➔ **Dataset** (data shape) ➔ **Activity** (work) ➔ **Pipeline**.
- **Azure Synapse Analytics**: Unified enterprise analytics (Serverless SQL, Dedicated SQL Pools, Spark Pools, Data Pipelines).
- **Azure Databricks**: Collaborative Apache Spark platform for big data processing, data science, and Delta Lake.
- **Azure Data Explorer (ADX / Kusto)**: High-speed ingestion and querying of logs, telemetry, and time-series using **KQL**.
- **Azure Stream Analytics (ASA)**: Real-time stream processing engine using SQL-based streaming queries.
- **Microsoft Power BI**:
  - **Power BI Desktop**: Authoring reports, data transformations (Power Query), and building **analytical semantic models**.
  - **Power BI Service**: Cloud collaboration, scheduling refreshes, and building single-page **dashboards**.

---

## 🔵 Security & Identity in Azure Data

- **Row-Level Security (RLS)**: Filters query results based on user identity or role (users only see their allowed rows).
- **Dynamic Data Masking (DDM)**: Obfuscates sensitive column values (e.g. credit card `XXXX-XXXX-XXXX-1234`) without altering stored data.
- **Always Encrypted**: Encrypts sensitive data inside client applications before transmitting to the database (protects data at rest and in use).
- **Transparent Data Encryption (TDE)**: Encrypts database files and backups at rest automatically using AES-256.
- **Azure SQL Database Authentication**: Supports **Microsoft Entra ID** and **SQL Authentication** only (no certificate authentication).
