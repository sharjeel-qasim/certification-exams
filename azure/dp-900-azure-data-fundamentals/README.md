# DP-900: Microsoft Azure Data Fundamentals — Practice Question Bank

[![Azure](https://img.shields.io/badge/Microsoft_Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Exam](https://img.shields.io/badge/Exam-DP--900-blue?style=for-the-badge)](#table-of-contents)
[![Questions](https://img.shields.io/badge/Questions-50%20MCQs-success?style=for-the-badge)](#table-of-contents)
[![Cheat Sheet](https://img.shields.io/badge/Study_Guide-Cheat_Sheet-orange?style=for-the-badge)](CHEAT_SHEET.md)

Complete Multiple Choice Question (MCQ) Practice Bank for the **Microsoft Certified: Azure Data Fundamentals (DP-900)** exam. Verified against official Microsoft Learn exam objectives with answer keys and concise technical explanations.

> ⚡ **Quick Review:** Check out the [**DP-900 Exam Cheat Sheet**](./CHEAT_SHEET.md) for a high-yield summary of relational vs. non-relational stores, Azure SQL, Cosmos DB, and analytics workloads before testing yourself below.

---

## Table of Contents

- [Domain 1: Describe Core Data Concepts (Q1 – Q20)](#domain-1-describe-core-data-concepts-q1--q20)
- [Domain 2: Describe How to Work with Relational Data on Azure (Q21 – Q26)](#domain-2-describe-how-to-work-with-relational-data-on-azure-q21--q26)
- [Domain 3: Describe How to Work with Non-Relational Data on Azure (Q27 – Q35)](#domain-3-describe-how-to-work-with-non-relational-data-on-azure-q27--q35)
- [Domain 4: Describe an Analytics Workload on Azure (Q36 – Q50)](#domain-4-describe-an-analytics-workload-on-azure-q36--q50)

---

## Domain 1: Describe Core Data Concepts (Q1 – Q20)

### Question 1
Which Azure data service allows you to store document, graph, and column-family databases?

- **A.** Azure Cosmos DB
- **B.** Azure SQL Database
- **C.** Azure Table storage
- **D.** Apache HBase

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Azure Cosmos DB is a multi-model NoSQL database service that natively supports document (NoSQL, MongoDB), graph (Apache Gremlin), key-value (Table API), and column-family (Apache Cassandra) models. Azure SQL Database is purely relational, Azure Table storage only supports key-value storage, and Apache HBase only supports column-family storage (not document or graph databases).

</details>

---

### Question 2
You have data stored in two tables in a database. You create a relationship between the tables. Which type of data do you have?

- **A.** structured
- **B.** semi-structured
- **C.** unstructured
- **D.** streaming

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Structured data adheres to a rigid, predefined tabular schema consisting of rows and columns with explicit relational integrity and keys between tables. Semi-structured data (like JSON or XML) uses tags and hierarchies without fixed relational table schemas, unstructured data (like video or audio) has no predefined structure, and streaming refers to real-time data ingestion velocity rather than data structure.

</details>

---

### Question 3
You have data that describes products and is stored in JSON documents. The product structure changes over time as new attributes are added. Which type of data do you have?

- **A.** structured
- **B.** semi-structured
- **C.** unstructured
- **D.** binary

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** Semi-structured data contains organizational tags, markers, or hierarchical key-value pairs (e.g., JSON, XML) without requiring a rigid tabular schema, enabling entity structures and attributes to vary per document over time. Structured data requires a fixed table schema where every row shares the same columns, unstructured data lacks built-in field organization altogether, and binary refers to raw byte encoding rather than a flexible document format.

</details>

---

### Question 4
Which type of data should be sent from video cameras in a native binary format?

- **A.** structured
- **B.** semi-structured
- **C.** unstructured
- **D.** relational

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** Unstructured data encompasses raw media such as video streams, images, audio recordings, and binary files that do not conform to a predefined tabular or hierarchical schema. Structured and relational data require fixed tabular rows and columns, while semi-structured data organizes fields using text tags or keys like JSON or XML.

</details>

---

### Question 5
You need to aggregate and store multiple JSON files that contain records for sales transactions. The solution must minimize the development effort. Which storage solution should you implement?

- **A.** Azure Cosmos DB
- **B.** Azure Files
- **C.** Azure Blob storage
- **D.** Azure SQL Database

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Azure Cosmos DB for NoSQL natively stores JSON documents and allows querying, filtering, and aggregating records directly using SQL syntax without custom ETL transformations. Azure Files and Azure Blob storage are file/object stores that lack a built-in database query engine to automatically index and aggregate JSON documents, while Azure SQL Database is a relational engine that requires parsing and mapping JSON into tabular structures.

</details>

---

### Question 6
Which type of database should you use to store sequential data in the fastest way possible?

- **A.** Time series database
- **B.** Graph database
- **C.** Azure Table storage
- **D.** Azure SQL Database

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Time series databases (such as Azure Data Explorer) are specifically engineered and indexed for high-throughput append-only ingestion and rapid retrieval of sequential, timestamped telemetry, IoT, or log records. Graph databases are designed for traversing complex many-to-many relationships, Azure Table storage is a simple key-value store not optimized for sequential time-window analytics, and Azure SQL Database is a relational database with higher transactional overhead for massive sequential streams.

</details>

---

### Question 7
You design an application that needs to store data based on the following requirements:
- Store historical data from multiple data sources.
- Load data on a scheduled basis.
- Use a denormalized star or snowflake schema.

Which type of database should you use?

- **A.** OLAP Database
- **B.** OLTP Database
- **C.** Document database
- **D.** Graph database

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** OLAP (Online Analytical Processing) databases and data warehouses are designed for multi-source historical reporting using scheduled batch loads and denormalized star or snowflake schemas (fact and dimension tables). OLTP databases are optimized for real-time transactional CRUD operations on normalized schemas, document databases store semi-structured JSON documents rather than relational star schemas, and graph databases model nodes and edges for relationship traversal.

</details>

---

### Question 8
Which type of database can be used for semi-structured data that will be processed by an Apache Spark pool in Azure Synapse Analytics?

- **A.** column-family
- **B.** relational
- **C.** graph
- **D.** object

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Column-family databases organize semi-structured data into rows with dynamic column sets that can be efficiently distributed and processed by Apache Spark pools in Azure Synapse Analytics. Relational databases enforce a rigid structured schema, graph databases model network relationships (vertices and edges), and object storage holds unstructured files rather than functioning as a database model.

</details>

---

### Question 9
Which two types of file store data in columnar format?

*Each correct answer presents a complete solution.*
*Choose 2 answers*

- **A.** Parquet
- **B.** ORC
- **C.** Avro
- **D.** CSV
- **E.** JSON

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** A, B

> **Why:** Parquet and ORC (Optimized Row Columnar) store data organized by columns rather than rows, enabling high compression ratios and efficient analytical query scanning by reading only required columns. Avro is a row-based binary serialization format, CSV is a row-oriented plain-text delimited format, and JSON is a hierarchical document format.

</details>

---

### Question 10
Which Azure Cosmos DB API allows you to implement a non-relational database and model nodes that have relationships between them?

- **A.** Apache Gremlin
- **B.** NoSQL
- **C.** MongoDB
- **D.** Apache Cassandra
- **E.** Table

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Azure Cosmos DB for Apache Gremlin is a graph database engine designed for modeling entities as vertices (nodes) and their relationships as edges. The NoSQL and MongoDB APIs are document-based stores, Apache Cassandra is a column-family API, and the Table API is a key-value store.

</details>

---

### Question 11
Which Azure SQL Database feature ensures that users can see only their own rows when multiple customers share the same tables?

- **A.** Row-Level Security (RLS)
- **B.** Dynamic Data Masking (DDM)
- **C.** Transparent Data Encryption (TDE)
- **D.** Always Encrypted

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Row-Level Security (RLS) uses security predicates defined at the database layer to automatically filter which rows are returned based on the executing user's identity or tenant context. Dynamic Data Masking (DDM) obfuscates sensitive column values rather than filtering rows, Transparent Data Encryption (TDE) encrypts database files at rest on disk, and Always Encrypted protects sensitive column data in transit and in use via client-side keys.

</details>

---

### Question 12
Which two attributes are characteristics of a transactional data workload?

*Each correct answer presents a complete solution.*
*Choose 2 answers*

- **A.** Highly normalized
- **B.** Optimized for CRUD operations
- **C.** Highly denormalized
- **D.** Optimized for read-only aggregations
- **E.** Uses star schemas

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** A, B

> **Why:** Transactional (OLTP) workloads prioritize data integrity, minimal storage duplication, and low-latency single-row creates, reads, updates, and deletes (CRUD) using highly normalized (3NF) schemas to prevent update anomalies. Highly denormalized structures, read-only aggregations, and star schemas are characteristics of analytical (OLAP) workloads.

</details>

---

### Question 13
Which two attributes are characteristics of an analytical data workload?

*Each correct answer presents a complete solution.*
*Choose 2 answers*

- **A.** Highly denormalized
- **B.** Optimized for read operations
- **C.** Highly normalized
- **D.** Optimized for write-heavy CRUD operations
- **E.** Strict ACID compliance across single records

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** A, B

> **Why:** Analytical (OLAP) workloads process large volumes of historical data for reporting, aggregations, and business intelligence using denormalized schemas (star/snowflake) optimized for fast parallel read scans. Highly normalized schemas, write-heavy CRUD operations, and single-record ACID transactions are characteristics of transactional (OLTP) workloads.

</details>

---

### Question 14
Which two types of applications are used in transactional systems?

*Each correct answer presents a complete solution.*
*Choose 2 answers*

- **A.** Line-of-business (LOB) applications
- **B.** Live applications
- **C.** Data mining applications
- **D.** Business intelligence dashboards
- **E.** Predictive analytics systems

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** A, B

> **Why:** Transactional processing supports real-time, user-facing live applications (e.g., e-commerce checkouts, banking systems, inventory trackers) and core line-of-business (LOB) applications executing daily operational transactions. Data mining applications, business intelligence dashboards, and predictive analytics systems are analytical (OLAP) workloads that query aggregated historical data.

</details>

---

### Question 15
Which job role is responsible for building data models and finding hidden data patterns?

- **A.** Data analyst
- **B.** Data engineer
- **C.** Database administrator (DBA)
- **D.** Cloud solutions architect

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** A data analyst transforms data into meaningful business insights by building semantic data models, discovering hidden trends/patterns, and designing interactive reports and visualizations (e.g., using Power BI). Data engineers build and manage data ingestion pipelines and lakes, DBAs oversee database security, backups, and operational performance, and cloud solutions architects design end-to-end cloud infrastructure.

</details>

---

### Question 16
Which two keys are needed to create a one-to-many relationship between two tables in a relational database?

*Each correct answer presents part of the solution.*
*Choose 2 answers*

- **A.** A primary key
- **B.** A foreign key
- **C.** A candidate key
- **D.** A composite index
- **E.** A unique constraint

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** A, B

> **Why:** In a relational database, a one-to-many relationship is created by defining a primary key on the parent ("one") table to uniquely identify each row and referencing it via a foreign key on the child ("many") table. A candidate key is simply a column eligible to be chosen as a primary key, a composite index speeds up multi-column queries without enforcing relationships, and a unique constraint prevents duplicate values in a column without linking tables.

</details>

---

### Question 17
What are two advantages of using normalization over not using normalization in a relational database?

*Each correct answer presents a complete solution.*
*Choose 2 answers*

- **A.** Optimizes for updates, inserts, and deletes
- **B.** Uses less storage space
- **C.** Optimizes for complex multi-table analytical reads
- **D.** Eliminates the need for indexing
- **E.** Eliminates the need for foreign keys

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** A, B

> **Why:** Normalization eliminates redundant duplicate data across tables, reducing storage footprint and ensuring that updates, inserts, and deletes modify data in only one place (preventing update anomalies). Because normalization splits data across multiple related tables, it requires more table joins during complex analytical reads and relies heavily on indexes and foreign keys rather than eliminating them.

</details>

---

### Question 18
Select the answer that correctly completes the sentence.

`[Answer choice]` is a process to reduce duplicate data in a database and ensure data integrity.

- **A.** Normalization
- **B.** Denormalization
- **C.** Partitioning
- **D.** Sharding

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Normalization is the formal relational database design process of organizing fields and tables to minimize data redundancy and enforce data integrity through relational constraints. Denormalization intentionally introduces redundancy to speed up analytical reads, while partitioning and sharding divide large tables across storage boundaries to improve scalability and manageability.

</details>

---

### Question 19
What should you create to improve the performance of a query accessing a table that contains millions of rows?

- **A.** An index
- **B.** A view
- **C.** A stored procedure
- **D.** A trigger

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** An index creates an auxiliary lookup structure (such as a B-tree) that allows the database engine to locate and retrieve specific rows rapidly without executing an expensive full table scan across millions of rows. A standard view is a saved SQL query (virtual table) that does not speed up underlying table scans, a stored procedure encapsulates reusable SQL logic, and a trigger automatically runs code when data modification events occur.

</details>

---

### Question 20
You need to recommend a solution that encapsulates business logic to rename products and add entries to tables. What should you include in the recommendation?

- **A.** A stored procedure
- **B.** A user-defined scalar function
- **C.** A view
- **D.** An inline table-valued function

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Stored procedures can encapsulate procedural business logic, modify existing rows (`UPDATE`), and insert new records (`INSERT`) across multiple tables in a single transaction. Views and user-defined functions (both scalar and inline table-valued) are restricted to read-only query computations and cannot execute data modification statements against database tables.

</details>

---

## Domain 2: Describe How to Work with Relational Data on Azure (Q21 – Q26)

### Question 21
Which service is managed and serverless, avoids the use of Windows Server licenses, and allows for each workload to have its own instance of the service being used?

- **A.** Azure SQL Database
- **B.** Azure SQL Managed Instance
- **C.** SQL Server on Azure Virtual Machines (Windows)
- **D.** SQL Server on Azure Virtual Machines (Linux)

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Azure SQL Database provides a fully managed, serverless Platform-as-a-Service (PaaS) compute tier that auto-scales per individual database, bills per second without OS licensing management, and isolates individual database workloads. Azure SQL Managed Instance provisions a shared instance for multiple databases rather than a serverless per-database model, and SQL Server on Azure VMs (Windows or Linux) is an IaaS solution requiring OS administration and VM provisioning.

</details>

---

### Question 22
Which data service provides a fully managed relational database with close to 100 percent feature parity with Microsoft SQL Server?

- **A.** Azure SQL Managed Instance
- **B.** Azure SQL Database
- **C.** SQL Server on Azure Virtual Machines
- **D.** Azure Synapse Analytics

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Azure SQL Managed Instance is a fully managed PaaS relational engine providing near-100% compatibility and feature parity with on-premises SQL Server (including SQL Server Agent, cross-database queries, CLR, and Service Broker) for seamless lift-and-shift migrations. Azure SQL Database lacks instance-scoped features like SQL Agent and cross-database joins, SQL Server on Azure VMs is IaaS (not a fully managed PaaS database), and Azure Synapse Analytics is an enterprise analytics/data warehousing service.

</details>

---

### Question 23
Which data service allows you to use every feature of Microsoft SQL Server in the cloud?

- **A.** SQL Server on Azure Virtual Machines running Windows
- **B.** Azure SQL Managed Instance
- **C.** Azure SQL Database
- **D.** SQL Server on Azure Virtual Machines running Linux

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** SQL Server on Azure Virtual Machines running Windows (IaaS) gives full administrative control over the host OS and supports 100% of SQL Server features, including Windows-specific components (like SSRS, SSAS, FileStream, and COM integrations). Azure SQL Managed Instance and Azure SQL Database are PaaS services that abstract the OS and restrict certain host-level features, while SQL Server on Linux VMs does not support Windows-dependent SQL Server services.

</details>

---

### Question 24
Which data service allows you to create a single database that can scale up and down without downtime?

- **A.** Azure SQL Database
- **B.** Azure SQL Managed Instance
- **C.** SQL Server on Azure Virtual Machines
- **D.** Azure Cosmos DB Table API

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Azure SQL Database is designed for cloud-native single databases that dynamically scale vCores, storage, and compute tiers (including auto-scaling serverless compute) online with negligible connection switchover and no downtime. Azure SQL Managed Instance scales at the multi-database instance level and takes longer to resize, SQL Server on Azure VMs requires VM resizing with a reboot (downtime), and Azure Cosmos DB Table API is a non-relational key-value store.

</details>

---

### Question 25
Which SQL engine is optimized for IoT scenarios?

- **A.** Azure SQL Edge
- **B.** SQL Server on Azure Virtual Machines
- **C.** Azure SQL Managed Instance
- **D.** Azure SQL Database

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Azure SQL Edge is a small-footprint, containerized relational engine optimized for IoT and edge gateways (ARM64/x64), featuring built-in streaming time-series processing, data compression, and in-engine ONNX machine learning execution. SQL Server on Azure VMs, Azure SQL Managed Instance, and Azure SQL Database are cloud-hosted relational services not designed to run locally on constrained IoT edge hardware.

</details>

---

### Question 26
Which authentication methods are supported by Azure SQL Database?

- **A.** Microsoft Entra authentication and SQL authentication only
- **B.** Certificate authentication, Microsoft Entra authentication, and SQL authentication
- **C.** Windows Authentication and SQL authentication only
- **D.** Anonymous access and SQL authentication only

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Azure SQL Database supports two authentication mechanisms: Microsoft Entra authentication (centralized cloud identity and token-based access) and SQL Authentication (database-level username and password). Direct certificate-based login authentication, legacy on-premises Windows Authentication without Microsoft Entra ID, and anonymous unauthenticated access are not supported.

</details>

---

## Domain 3: Describe How to Work with Non-Relational Data on Azure (Q27 – Q35)

### Question 27
Which type of Azure Storage is used for VHDs and is optimized for random read and write operations?

- **A.** Page blob
- **B.** Block blob
- **C.** Append blob
- **D.** Azure Files

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Page blobs are collections of 512-byte pages optimized for low-latency random read and write operations, making them the backing storage for Azure Virtual Machine Virtual Hard Disks (VHDs). Block blobs are optimized for storing and streaming large discrete objects (documents, media, backups), append blobs only support appending new blocks to the end of a file (logging), and Azure Files provides SMB/NFS network file shares.

</details>

---

### Question 28
Which type of Azure Storage is used to store key/value pairs grouped in partitions?

- **A.** Azure Table storage
- **B.** Azure Files
- **C.** Azure Data Lake Storage Gen2
- **D.** Page blob

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Azure Table storage is a low-cost, NoSQL key-value store that groups schemaless entities into horizontal partitions indexed by a `PartitionKey` and `RowKey`. Azure Files provides network-mounted file shares, Azure Data Lake Storage Gen2 provides a hierarchical file system for big data analytics, and page blobs provide random-access block storage for virtual disks.

</details>

---

### Question 29
Which Azure Blob storage access tier should you use for data that will be used once per year and can have an access time that takes more than an hour?

- **A.** Archive
- **B.** Cool
- **C.** Hot
- **D.** Premium

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** The Archive access tier offers the lowest storage cost for rarely accessed data (retained at least 180 days) that can tolerate retrieval latency of several hours during the blob rehydration process. The Cool tier (30-day minimum) and Hot tier provide immediate millisecond retrieval at higher storage costs, while the Premium tier uses SSDs for high-transaction, single-digit millisecond workloads.

</details>

---

### Question 30
Which type of blob should you use to store data blocks that are added to a file frequently but cannot be deleted?

- **A.** Append blob
- **B.** Block blob
- **C.** Page blob
- **D.** Premium blob

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Append blobs are optimized exclusively for append-only operations where new blocks are added to the end of the blob; modifying or deleting existing blocks is not supported, making them ideal for audit trails and application logging. Block blobs allow modifying and replacing individual blocks, page blobs support random read/write operations across 512-byte pages, and Premium blob refers to an SSD performance tier rather than a blob resource type.

</details>

---

### Question 31
Which storage solution should you use to store unstructured documents, graph databases, and key/value pairs?

- **A.** Azure Cosmos DB
- **B.** Azure Files
- **C.** Azure Table storage
- **D.** Azure SQL Database

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Azure Cosmos DB is Microsoft's multi-model distributed database that supports schemaless documents (NoSQL/MongoDB), graph models (Apache Gremlin), and key-value tables (Table API) under a single globally distributed engine. Azure Files only provides shared network file storage, Azure Table storage only supports key-value entities (not graph databases), and Azure SQL Database is a relational database engine.

</details>

---

### Question 32
Which Azure Cosmos DB API should you use for data in a graph structure?

- **A.** Apache Gremlin
- **B.** Apache Cassandra
- **C.** MongoDB
- **D.** Table

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** The Apache Gremlin API in Azure Cosmos DB provides graph traversal and query capabilities using vertex (node) and edge (relationship) models. Apache Cassandra is used for wide-column (column-family) data, MongoDB is used for BSON document data, and the Table API is used for key-value data.

</details>

---

### Question 33
Which Azure Cosmos DB API should you use for data in the BSON format?

- **A.** MongoDB
- **B.** Table
- **C.** Apache Cassandra
- **D.** Apache Gremlin

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Azure Cosmos DB for MongoDB implements the MongoDB wire protocol and natively stores and queries documents in BSON (Binary JSON) format. The Table API stores key-value entities, Apache Cassandra stores tabular column-family data, and Apache Gremlin stores graph vertices and edges.

</details>

---

### Question 34
You need to process many JSON files every minute, while keeping the data from the files accessible by using native queries. Which Azure Cosmos DB API should you use?

- **A.** NoSQL
- **B.** Apache Cassandra
- **C.** Table
- **D.** Apache Gremlin

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Azure Cosmos DB for NoSQL (Core SQL API) is the native document API for high-throughput JSON document ingestion and rich querying using familiar SQL syntax. Apache Cassandra uses CQL over column-family tables, the Table API is designed for simple key-value lookups rather than complex JSON queries, and Apache Gremlin is used for graph traversals.

</details>

---

### Question 35
Which Azure Cosmos DB API allows you to work with vertices and edges?

- **A.** Apache Gremlin
- **B.** NoSQL
- **C.** MongoDB
- **D.** Apache Cassandra

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** In graph data modeling, entities are defined as vertices (nodes) and their relationships are modeled as edges, which are queried using the Apache Gremlin API in Azure Cosmos DB. The NoSQL and MongoDB APIs work with JSON/BSON documents, while the Apache Cassandra API works with wide-column tables.

</details>

---

## Domain 4: Describe an Analytics Workload on Azure (Q36 – Q50)

### Question 36
Which type of data store uses star schemas, fact tables, and dimension tables?

- **A.** Data warehouse
- **B.** Relational OLTP database
- **C.** Data lake
- **D.** Key-value store

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Data warehouses (such as dedicated SQL pools in Azure Synapse Analytics) use dimensional modeling with central numeric fact tables linked to descriptive dimension tables in star and snowflake schemas. Relational OLTP databases use normalized (3NF) schemas for transactional integrity, data lakes store raw files in folders using schema-on-read, and key-value stores group simple schemaless attributes by key.

</details>

---

### Question 37
Which data integration service allows you to orchestrate data flow without coding?

- **A.** Azure Data Factory
- **B.** Azure Data Lake
- **C.** Azure Databricks
- **D.** Azure HDInsight

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Azure Data Factory (ADF) is a cloud-based ETL/ELT data integration service with a visual, code-free interface for building, scheduling, and orchestrating data pipelines and Mapping Data Flows. Azure Data Lake is a storage repository rather than an orchestration engine, while Azure Databricks and Azure HDInsight are code-first Apache Spark/Hadoop cluster platforms primarily driven by notebooks and scripts.

</details>

---

### Question 38
Which two services allow you to create a pipeline to process data in response to an event?

*Each correct answer presents a complete solution.*
*Choose 2 answers*

- **A.** Azure Data Factory
- **B.** Azure Synapse Analytics
- **C.** Azure Databricks
- **D.** Azure HDInsight
- **E.** Azure Data Lake Storage Gen2

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** A, B

> **Why:** Both Azure Data Factory and Azure Synapse Analytics share the same pipeline orchestration engine and support event-driven pipeline triggers (e.g., triggering an ingestion pipeline automatically when a blob is created or deleted in storage). Azure Databricks uses job schedules or continuous streaming rather than ADF-style event pipelines, Azure HDInsight is a managed Hadoop/Spark cluster service, and Azure Data Lake Storage Gen2 is a passive storage layer.

</details>

---

### Question 39
What should you create first for an integration process that copies data from Microsoft Excel files to Parquet files by using Azure Data Factory?

- **A.** A linked service
- **B.** A pipeline
- **C.** A dataset
- **D.** An activity

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** In Azure Data Factory, the resource dependency hierarchy requires creating a Linked Service (which defines the connection string and credentials to the source/sink storage account) first, followed by Datasets (which reference the linked service to point to specific Excel/Parquet files), and finally Activities (such as Copy Data) inside a Pipeline.

</details>

---

### Question 40
Which three actions can you perform directly from an Azure Databricks notebook?

*Each correct answer presents a complete solution.*
*Choose 3 answers*

- **A.** Run SQL queries to explore and analyze data
- **B.** Create tables (such as Delta tables) to persist structured data
- **C.** Create databases in the metastore by running SQL commands
- **D.** Provision new Azure Databricks workspaces
- **E.** Configure Azure tenant subscriptions

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** A, B, C

> **Why:** Azure Databricks notebooks are interactive Spark computing environments where you can execute multi-language code (Python, Scala, SQL, R) to run analytical queries, build Delta tables, and define metastore databases. Provisioning new Azure Databricks workspaces and configuring Azure tenant subscriptions are control-plane administrative tasks performed via the Azure portal, CLI, or ARM/Bicep templates.

</details>

---

### Question 41
Which two services can be used as a source for stream processing?

*Each correct answer presents a complete solution.*
*Choose 2 answers*

- **A.** Azure Event Hubs
- **B.** Azure IoT Hub
- **C.** Azure Databricks
- **D.** Azure SQL Database
- **E.** Power BI

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** A, B

> **Why:** Azure Event Hubs (big data event ingestion) and Azure IoT Hub (bi-directional device telemetry messaging) are purpose-built streaming ingestion brokers that act as native input sources for stream processing engines like Azure Stream Analytics. Azure Databricks is a Spark processing engine rather than a streaming broker, while Azure SQL Database and Power BI are typically used as downstream output sinks for processed stream results.

</details>

---

### Question 42
Which three services can be used to ingest data for stream processing?

*Each correct answer presents a complete solution.*
*Choose 3 answers*

- **A.** Azure Data Lake Storage
- **B.** Azure Event Hubs
- **C.** Azure IoT Hub
- **D.** Azure Functions
- **E.** Azure SQL Database

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** A, B, C

> **Why:** In Azure stream processing architectures (such as Azure Stream Analytics), native streaming input sources include message brokers (Azure Event Hubs, Azure IoT Hub) and storage containers (Azure Blob Storage / Azure Data Lake Storage). Azure Functions and Azure SQL Database are used as downstream output sinks to receive processed results rather than native streaming ingestion sources.

</details>

---

### Question 43
Which service allows you to perform on-demand analysis of large volumes of data from text logs, websites and IoT devices by using a common querying language for all the data sources?

- **A.** Azure Data Explorer
- **B.** Azure Data Lake Storage Gen2
- **C.** Azure Stream Analytics
- **D.** Azure Cosmos DB

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Azure Data Explorer (ADX / Kusto) is a fast, highly scalable log analytics and time-series exploration service that uses Kusto Query Language (KQL) for on-demand analysis of telemetry, text logs, and IoT events. Azure Data Lake Storage Gen2 is a storage layer without its own query engine, Azure Stream Analytics is for continuous real-time stream windowing rather than interactive ad-hoc exploration, and Azure Cosmos DB is an operational NoSQL database.

</details>

---

### Question 44
You need to ingest, transform, and visualize data from a continuously generated data source. The solution must minimize latency and administrative effort. Which type of data processing should you use?

- **A.** Stream
- **B.** Batch
- **C.** Microbatching
- **D.** Scheduled polling

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Stream processing processes each event continuously in real time as data arrives (e.g., via Azure Stream Analytics to Power BI), providing near-zero latency for live dashboards without managing batch schedules. Batch processing and scheduled polling group data into periodic intervals (introducing latency of minutes to hours), while microbatching still buffers events into small time windows rather than processing events immediately upon arrival.

</details>

---

### Question 45
Which type of visual in Microsoft Power BI should you use to compare categorized values as the proportions of a total value?

- **A.** Pie chart
- **B.** Line chart
- **C.** Bar chart
- **D.** Scatter plot

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Pie charts (and donut charts) are specifically used to show parts-of-a-whole proportions relative to a 100% total. Line charts display continuous trends over time, bar charts compare quantitative values across discrete categories independently of a total share, and scatter plots examine correlation between two numeric variables.

</details>

---

### Question 46
What should you use to define an analytical model for Microsoft Power BI?

- **A.** Power BI Desktop
- **B.** Power BI Service
- **C.** Power BI Mobile App
- **D.** Azure Data Factory

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Power BI Desktop is the dedicated authoring application used by data analysts to connect to data sources, perform Power Query transformations, define table relationships, write DAX measures, and build semantic analytical models. The Power BI Service is primarily for cloud publishing, collaboration, and dashboard creation; the Power BI Mobile App is for consuming reports on mobile devices; and Azure Data Factory is an ETL pipeline tool rather than a BI modeling tool.

</details>

---

### Question 47
Which two visuals in Microsoft Power BI allow you to visually compare numeric values for discrete categories?

*Each correct answer presents a complete solution.*
*Choose 2 answers*

- **A.** A bar chart
- **B.** A column chart
- **C.** A card visual
- **D.** A scatter plot
- **E.** A gauge visual

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** A, B

> **Why:** Bar charts (horizontal bars) and column charts (vertical columns) are designed to compare discrete categories against quantitative numeric measures. A card visual displays only a single aggregated number, a scatter plot compares two continuous numeric measures to identify correlation clusters, and a gauge visual tracks progress of a single metric toward a target goal.

</details>

---

### Question 48
Which visual in Microsoft Power BI allows you to view trends, such as changes in sales over time?

- **A.** A line chart
- **B.** A scatter plot
- **C.** A pie chart
- **D.** A card visual

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Line charts connect data points along a continuous axis (such as time), making them the standard visual for displaying progression, time-series data, and trend analysis (e.g., monthly sales performance). A scatter plot shows correlation between two numeric variables, a pie chart shows static part-to-whole proportions, and a card visual shows a single summary number without historical progression.

</details>

---

### Question 49
In the Power BI service, what should you create to share a single page with the most important visuals from reports?

- **A.** A dashboard
- **B.** A dataset
- **C.** A dataflow
- **D.** A workspace app

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** In the Power BI Service, a dashboard is a customizable single-page canvas composed of pinned visual tiles from one or more underlying reports, providing a consolidated high-level KPI overview. A dataset (semantic model) holds the underlying data connections and relationships, a dataflow is a cloud-based Power Query data preparation pipeline, and a workspace app bundles multiple dashboards and reports together for broad organizational distribution.

</details>

---

### Question 50
You need to share a report that you created in Microsoft Power BI Desktop with other users. What should you do first?

- **A.** Publish the report to the Power BI service
- **B.** Export the report to PDF and email it
- **C.** Save the PBIX file to a local shared network drive
- **D.** Create an Azure Data Factory pipeline

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** To share interactive reports and semantic models created in Power BI Desktop securely with organizational users, you must first publish the `.pbix` file to a workspace in the cloud-based Power BI Service. Exporting to PDF produces a static non-interactive snapshot, saving raw `.pbix` files to a network drive bypasses cloud governance and scheduled refresh, and Azure Data Factory is an ETL orchestration tool unrelated to sharing Power BI reports.

</details>
