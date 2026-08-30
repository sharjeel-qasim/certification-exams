# DP-900: Microsoft Azure Data Fundamentals — Question Bank

[![Azure](https://img.shields.io/badge/Microsoft_Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Exam](https://img.shields.io/badge/Exam-DP--900-blue?style=for-the-badge)](#table-of-contents)
[![Questions](https://img.shields.io/badge/Questions-50%20MCQs-success?style=for-the-badge)](#table-of-contents)
[![Cheat Sheet](https://img.shields.io/badge/Study_Guide-Cheat_Sheet-orange?style=for-the-badge)](CHEAT_SHEET.md)

Complete Multiple Choice Question (MCQ) Practice Bank for the **Microsoft Certified: Azure Data Fundamentals (DP-900)** exam. Verified against official Microsoft Learn exam objectives with answer keys and concise technical explanations.

> [!TIP]
> Need a quick review before taking the practice exam? Check out the [DP-900 Last-Minute Cram Sheet](CHEAT_SHEET.md) for comparison matrices on Cosmos DB APIs, Azure SQL tiers, and Storage options.

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

**Correct answer:** A

> **Why:** Azure Cosmos DB is a multi-model NoSQL database service that natively supports document (NoSQL, MongoDB), graph (Apache Gremlin), key-value (Table API), and column-family (Apache Cassandra) models. Azure SQL Database is relational, Table storage is key-value only, and HBase does not support graph databases.

---

### Question 2
You have data stored in two tables in a database. You create a relationship between the tables. Which type of data do you have?

- **A.** structured
- **B.** semi-structured
- **C.** unstructured
- **D.** streaming

**Correct answer:** A

> **Why:** Structured data adheres to a rigid, predefined tabular schema consisting of rows and columns with explicit relational integrity and keys between tables.

---

### Question 3
You have data that describes products and is stored in JSON documents. The product structure changes over time as new attributes are added. Which type of data do you have?

- **A.** structured
- **B.** semi-structured
- **C.** unstructured
- **D.** binary

**Correct answer:** B

> **Why:** Semi-structured data contains organizational tags, markers, or hierarchical key-value pairs (e.g., JSON, XML) without requiring a rigid tabular schema, enabling entity structures and fields to vary over time.

---

### Question 4
Which type of data should be sent from video cameras in a native binary format?

- **A.** structured
- **B.** semi-structured
- **C.** unstructured
- **D.** relational

**Correct answer:** C

> **Why:** Unstructured data contains data such as documents, images, audio recordings, video streams, and raw binary files that do not conform to a predefined schema.

---

### Question 5
You need to aggregate and store multiple JSON files that contain records for sales transactions. The solution must minimize the development effort. Which storage solution should you implement?

- **A.** Azure Cosmos DB
- **B.** Azure Files
- **C.** Azure Blob storage
- **D.** Azure SQL Database

**Correct answer:** A

> **Why:** Azure Cosmos DB for NoSQL natively stores JSON documents and allows querying, filtering, and aggregating records directly using SQL syntax without custom ETL transformations. Azure Files and Blob storage lack built-in query engines, and Azure SQL Database requires schema mapping.

---

### Question 6
Which type of database should you use to store sequential data in the fastest way possible?

- **A.** Time series database
- **B.** Graph database
- **C.** Azure Table storage
- **D.** Azure SQL Database

**Correct answer:** A

> **Why:** Time series databases (such as Azure Data Explorer) are specifically engineered and indexed for high-throughput append-only ingestion and rapid retrieval of sequential, timestamped telemetry, IoT, or log records.

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

**Correct answer:** A

> **Why:** OLAP (Online Analytical Processing) databases and data warehouses are designed for multi-source historical reporting using denormalized star or snowflake schemas (fact and dimension tables). OLTP databases are optimized for low-latency CRUD operations on normalized schemas.

---

### Question 8
Which type of database can be used for semi-structured data that will be processed by an Apache Spark pool in Azure Synapse Analytics?

- **A.** column-family
- **B.** relational
- **C.** graph
- **D.** object

**Correct answer:** A

> **Why:** Column-family databases organize tabular, semi-structured data into rows with dynamic column sets that are natively supported and processed by Apache Spark pools in Azure Synapse Analytics.

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

**Correct answers:** A, B

> **Why:** Parquet and ORC (Optimized Row Columnar) store data organized by columns rather than rows, enabling high compression ratios and efficient analytical query scanning by reading only required columns. Avro and CSV are row-based formats.

---

### Question 10
Which Azure Cosmos DB API allows you to implement a non-relational database and model nodes that have relationships between them?

- **A.** Apache Gremlin
- **B.** NoSQL
- **C.** MongoDB
- **D.** Apache Cassandra
- **E.** Table

**Correct answer:** A

> **Why:** Azure Cosmos DB for Apache Gremlin is a graph database engine designed for modeling entities as vertices (nodes) and their relationships as edges.

---

### Question 11
Which Azure SQL Database feature ensures that users can see only their own rows when multiple customers share the same tables?

- **A.** Row-Level Security (RLS)
- **B.** Dynamic Data Masking (DDM)
- **C.** Transparent Data Encryption (TDE)
- **D.** Always Encrypted

**Correct answer:** A

> **Why:** Row-Level Security (RLS) uses security predicates defined at the database layer to automatically filter which rows are returned based on the executing user's identity or tenant context. Dynamic Data Masking obfuscates column values, while TDE and Always Encrypted protect against unauthorized data-at-rest or in-transit access.

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

**Correct answers:** A, B

> **Why:** Transactional (OLTP) workloads prioritize data integrity, minimal storage duplication, and low-latency single-row inserts, updates, and deletes (CRUD). They use highly normalized (3NF) schemas to prevent update anomalies.

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

**Correct answers:** A, B

> **Why:** Analytical (OLAP) workloads process large volumes of historical data for reporting, aggregations, and business intelligence. They use denormalized schemas (star/snowflake) optimized for fast parallel read scans across millions of rows.

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

**Correct answers:** A, B

> **Why:** Transactional processing supports real-time, user-facing live applications (e.g. e-commerce checkouts, banking systems, inventory trackers) and core line-of-business (LOB) applications executing daily business transactions.

---

### Question 15
Which job role is responsible for building data models and finding hidden data patterns?

- **A.** Data analyst
- **B.** Data engineer
- **C.** Database administrator (DBA)
- **D.** Cloud solutions architect

**Correct answer:** A

> **Why:** A data analyst transforms data into meaningful insights by building semantic data models, discovering trends/hidden patterns, and designing interactive reports and visualizations (e.g., using Power BI). Data engineers manage ingestion pipelines and storage, while DBAs oversee security, backups, and server performance.

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

**Correct answers:** A, B

> **Why:** In a relational database, a one-to-many relationship is created by defining a Primary Key on the parent table (uniquely identifying each parent row) and referencing it via a Foreign Key in the child table.

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

**Correct answers:** A, B

> **Why:** Normalization eliminates redundant duplicate data across tables, reducing storage footprint and ensuring that updates, inserts, and deletes modify data in exactly one place (preventing update anomalies). It introduces joins, which can slow down complex analytical reads compared to denormalized tables.

---

### Question 18
Select the answer that correctly completes the sentence.

`[Answer choice]` is a process to reduce duplicate data in a database and ensure data integrity.

- **A.** Normalization
- **B.** Denormalization
- **C.** Partitioning
- **D.** Sharding

**Correct answer:** A

> **Why:** Normalization is the formal relational database design process of organizing fields and tables to minimize data redundancy and enforce data integrity through relational constraints.

---

### Question 19
What should you create to improve the performance of a query accessing a table that contains millions of rows?

- **A.** An index
- **B.** A view
- **C.** A stored procedure
- **D.** A trigger

**Correct answer:** A

> **Why:** An index creates an auxiliary search data structure (e.g. B-tree) that allows the database engine to locate and retrieve specific rows efficiently without executing an expensive full table scan across millions of rows.

---

### Question 20
You need to recommend a solution that encapsulates business logic to rename products and add entries to tables. What should you include in the recommendation?

- **A.** A stored procedure
- **B.** A user-defined scalar function
- **C.** A view
- **D.** An inline table-valued function

**Correct answer:** A

> **Why:** Stored procedures can encapsulate complex procedural business logic, modify existing rows (`UPDATE`), and insert new records (`INSERT`) across multiple tables in a single transaction. Views and user-defined functions are restricted to read operations and cannot execute data modification statements.

---

## Domain 2: Describe How to Work with Relational Data on Azure (Q21 – Q26)

### Question 21
Which service is managed and serverless, avoids the use of Windows Server licenses, and allows for each workload to have its own instance of the service being used?

- **A.** Azure SQL Database
- **B.** Azure SQL Managed Instance
- **C.** SQL Server on Azure Virtual Machines (Windows)
- **D.** SQL Server on Azure Virtual Machines (Linux)

**Correct answer:** A

> **Why:** Azure SQL Database provides a fully managed, serverless Platform-as-a-Service (PaaS) tier that auto-scales compute per database, bills per second without OS licensing management, and isolates individual database workloads.

---

### Question 22
Which data service provides a fully managed relational database with close to 100 percent feature parity with Microsoft SQL Server?

- **A.** Azure SQL Managed Instance
- **B.** Azure SQL Database
- **C.** SQL Server on Azure Virtual Machines
- **D.** Azure Synapse Analytics

**Correct answer:** A

> **Why:** Azure SQL Managed Instance is a fully managed PaaS relational engine providing ~100% compatibility and feature parity with on-premises SQL Server (including SQL Agent, Cross-database queries, CLR, Service Broker), enabling seamless lift-and-shift migrations.

---

### Question 23
Which data service allows you to use every feature of Microsoft SQL Server in the cloud?

- **A.** SQL Server on Azure Virtual Machines running Windows
- **B.** Azure SQL Managed Instance
- **C.** Azure SQL Database
- **D.** SQL Server on Azure Virtual Machines running Linux

**Correct answer:** A

> **Why:** SQL Server on Azure Windows Virtual Machines (IaaS) gives full administrative access to the underlying OS and 100% capability to install and configure all SQL Server versions, custom drivers, third-party agents, and legacy features.

---

### Question 24
Which data service allows you to create a single database that can scale up and down without downtime?

- **A.** Azure SQL Database
- **B.** Azure SQL Managed Instance
- **C.** SQL Server on Azure Virtual Machines
- **D.** Azure Cosmos DB Table API

**Correct answer:** A

> **Why:** Azure SQL Database allows on-demand dynamic scaling of vCores, storage, and compute tiers (including auto-scaling serverless compute) with negligible latency and zero downtime.

---

### Question 25
Which SQL engine is optimized for IoT scenarios?

- **A.** Azure SQL Edge
- **B.** SQL Server on Azure Virtual Machines
- **C.** Azure SQL Managed Instance
- **D.** Azure SQL Database

**Correct answer:** A

> **Why:** Azure SQL Edge is a small-footprint, containerized relational engine optimized for IoT and edge gateways, featuring built-in streaming time-series processing, data compression, and in-engine machine learning execution.

---

### Question 26
Which authentication methods are supported by Azure SQL Database?

- **A.** Microsoft Entra authentication and SQL authentication only
- **B.** Certificate authentication, Microsoft Entra authentication, and SQL authentication
- **C.** Windows Authentication and SQL authentication only
- **D.** Anonymous access and SQL authentication only

**Correct answer:** A

> **Why:** Azure SQL Database supports Microsoft Entra ID (centralized identity and token-based access) and SQL Authentication (database username and password). Certificate-based authentication is not supported.

---

## Domain 3: Describe How to Work with Non-Relational Data on Azure (Q27 – Q35)

### Question 27
Which type of Azure Storage is used for VHDs and is optimized for random read and write operations?

- **A.** Page blob
- **B.** Block blob
- **C.** Append blob
- **D.** Azure Files

**Correct answer:** A

> **Why:** Page blobs are collections of 512-byte pages optimized for random read and write operations, making them the backing storage for Azure Virtual Machine Virtual Hard Disks (VHDs).

---

### Question 28
Which type of Azure Storage is used to store key/value pairs grouped in partitions?

- **A.** Azure Table storage
- **B.** Azure Files
- **C.** Azure Data Lake Storage Gen2
- **D.** Page blob

**Correct answer:** A

> **Why:** Azure Table storage is a low-cost, NoSQL key-value store that groups schemaless entities into partitions indexed by a `PartitionKey` and `RowKey`.

---

### Question 29
Which Azure Blob storage access tier should you use for data that will be used once per year and can have an access time that takes more than an hour?

- **A.** Archive
- **B.** Cool
- **C.** Hot
- **D.** Premium

**Correct answer:** A

> **Why:** The Archive access tier offers the lowest storage cost for rarely accessed data (retained at least 180 days) with retrieval latency of several hours (rehydration process).

---

### Question 30
Which type of blob should you use to store data blocks that are added to a file frequently but cannot be deleted?

- **A.** Append blob
- **B.** Block blob
- **C.** Page blob
- **D.** Premium blob

**Correct answer:** A

> **Why:** Append blobs are optimized for append-only operations where new blocks are added to the end of the blob. Modifying or deleting existing blocks is not supported, making them ideal for logging scenarios.

---

### Question 31
Which storage solution should you use to store unstructured documents, graph databases, and key/value pairs?

- **A.** Azure Cosmos DB
- **B.** Azure Files
- **C.** Azure Table storage
- **D.** Azure SQL Database

**Correct answer:** A

> **Why:** Azure Cosmos DB is Microsoft's multi-model distributed database that supports documents (NoSQL/MongoDB), graph models (Gremlin), and key-value tables (Table API) under a single globally distributed engine.

---

### Question 32
Which Azure Cosmos DB API should you use for data in a graph structure?

- **A.** Apache Gremlin
- **B.** Apache Cassandra
- **C.** MongoDB
- **D.** Table

**Correct answer:** A

> **Why:** The Apache Gremlin API in Azure Cosmos DB provides graph traversal and query capabilities using vertex and edge models.

---

### Question 33
Which Azure Cosmos DB API should you use for data in the BSON format?

- **A.** MongoDB
- **B.** Table
- **C.** Apache Cassandra
- **D.** Apache Gremlin

**Correct answer:** A

> **Why:** Azure Cosmos DB for MongoDB implements the MongoDB wire protocol and natively stores documents in BSON (Binary JSON) format.

---

### Question 34
You need to process many JSON files every minute, while keeping the data from the files accessible by using native queries. Which Azure Cosmos DB API should you use?

- **A.** NoSQL
- **B.** Apache Cassandra
- **C.** Table
- **D.** Apache Gremlin

**Correct answer:** A

> **Why:** Azure Cosmos DB for NoSQL (Core SQL API) is the native API for managing JSON documents with high-throughput ingestion and rich SQL-style querying.

---

### Question 35
Which Azure Cosmos DB API allows you to work with vertices and edges?

- **A.** Apache Gremlin
- **B.** NoSQL
- **C.** MongoDB
- **D.** Apache Cassandra

**Correct answer:** A

> **Why:** In graph data modeling, entities are defined as vertices (nodes) and their relationships are modeled as edges. Apache Gremlin is the graph traversal API for this data structure.

---

## Domain 4: Describe an Analytics Workload on Azure (Q36 – Q50)

### Question 36
Which type of data store uses star schemas, fact tables, and dimension tables?

- **A.** Data warehouse
- **B.** Relational OLTP database
- **C.** Data lake
- **D.** Key-value store

**Correct answer:** A

> **Why:** Data warehouses (such as dedicated SQL pools in Azure Synapse Analytics) use dimensional modeling with central numeric fact tables linked to descriptive dimension tables in star and snowflake schemas.

---

### Question 37
Which data integration service allows you to orchestrate data flow without coding?

- **A.** Azure Data Factory
- **B.** Azure Data Lake
- **C.** Azure Databricks
- **D.** Azure HDInsight

**Correct answer:** A

> **Why:** Azure Data Factory (ADF) is a cloud-based ETL/ELT data integration service with a visual, code-free interface for building, scheduling, and orchestrating complex data pipelines.

---

### Question 38
Which two services allow you to create a pipeline to process data in response to an event?

*Each correct answer presents a complete solution.*
*Choose 2 answers*

- **A.** Azure Data Factory
- **B.** Azure Synapse Analytics
- **C.** Azure Databricks
- **D.** Azure HDInsight
- **E.** Azure Event Grid (storage only)

**Correct answers:** A, B

> **Why:** Both Azure Data Factory and Azure Synapse Analytics support event-driven pipeline triggers (e.g. triggering an ingestion pipeline automatically when a blob is created or deleted in storage).

---

### Question 39
What should you create first for an integration process that copies data from Microsoft Excel files to Parquet files by using Azure Data Factory?

- **A.** A linked service
- **B.** A pipeline
- **C.** A dataset
- **D.** An activity

**Correct answer:** A

> **Why:** In Azure Data Factory, the resource dependency hierarchy requires creating Linked Services (connection strings to source/sink datastores) first, followed by Datasets (specific data structures/files pointing to linked services), and finally Activities within a Pipeline.

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

**Correct answers:** A, B, C

> **Why:** Azure Databricks notebooks are interactive computing environments where you can execute multi-language code (Python, Scala, SQL, R) to run queries, build Delta tables, and define metastore databases. Workspace and subscription provisioning are administrative tasks performed via the Azure portal/CLI.

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

**Correct answers:** A, B

> **Why:** Azure Event Hubs (big data event ingestion) and Azure IoT Hub (bi-directional device messaging) are purpose-built streaming ingestion brokers that feed streaming consumers like Azure Stream Analytics and Apache Spark Streaming.

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

**Correct answers:** A, B, C

> **Why:** In Azure stream processing architectures, streaming ingestion sources include message brokers (Azure Event Hubs, Azure IoT Hub) and streaming storage buckets (Azure Data Lake Storage). Azure Functions and Azure SQL Database act as downstream outputs/sinks.

---

### Question 43
Which service allows you to perform on-demand analysis of large volumes of data from text logs, websites and IoT devices by using a common querying language for all the data sources?

- **A.** Azure Data Explorer
- **B.** Azure Data Lake Storage Gen2
- **C.** Azure Stream Analytics
- **D.** Azure Cosmos DB

**Correct answer:** A

> **Why:** Azure Data Explorer (ADX / Kusto) is a fast, highly scalable log analytics and time-series search service that uses Kusto Query Language (KQL) to query telemetry, structured logs, and streaming events in real time.

---

### Question 44
You need to ingest, transform, and visualize data from a continuously generated data source. The solution must minimize latency and administrative effort. Which type of data processing should you use?

- **A.** Stream
- **B.** Batch
- **C.** Microbatching
- **D.** Scheduled polling

**Correct answer:** A

> **Why:** Stream processing processes each event or small window in real time as data arrives, providing near-zero latency for dashboards and alerts without waiting for batch intervals.

---

### Question 45
Which type of visual in Microsoft Power BI should you use to compare categorized values as the proportions of a total value?

- **A.** Pie chart
- **B.** Line chart
- **C.** Bar chart
- **D.** Scatter plot

**Correct answer:** A

> **Why:** Pie charts and donut charts are specifically used to show parts-of-a-whole proportions relative to a 100% total. Line charts display trends over time, bar charts compare discrete categories, and scatter plots examine correlation.

---

### Question 46
What should you use to define an analytical model for Microsoft Power BI?

- **A.** Power BI Desktop
- **B.** Power BI Service
- **C.** Power BI Mobile App
- **D.** Azure Data Factory

**Correct answer:** A

> **Why:** Power BI Desktop is the dedicated authoring application used by data analysts to connect to data sources, perform Power Query transformations, define data relationships, write DAX measures, and build semantic analytical models.

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

**Correct answers:** A, B

> **Why:** Bar charts (horizontal) and column charts (vertical) are designed to compare discrete categories against quantitative numeric measures.

---

### Question 48
Which visual in Microsoft Power BI allows you to view trends, such as changes in sales over time?

- **A.** A line chart
- **B.** A scatter plot
- **C.** A pie chart
- **D.** A card visual

**Correct answer:** A

> **Why:** Line charts are the standard visual for displaying continuous progression, time-series data, and trend analysis (e.g., monthly sales performance).

---

### Question 49
In the Power BI service, what should you create to share a single page with the most important visuals from reports?

- **A.** A dashboard
- **B.** A dataset
- **C.** A dataflow
- **D.** A workspace app

**Correct answer:** A

> **Why:** In the Power BI Service, a dashboard is a customizable single-page canvas composed of pinned tiles from multiple reports, providing a consolidated high-level KPI overview.

---

### Question 50
You need to share a report that you created in Microsoft Power BI Desktop with other users. What should you do first?

- **A.** Publish the report to the Power BI service
- **B.** Export the report to PDF and email it
- **C.** Save the PBIX file to a local shared network drive
- **D.** Create an Azure Data Factory pipeline

**Correct answer:** A

> **Why:** To share interactive reports and data models created in Power BI Desktop securely with organizational users, you must first Publish the `.pbix` file to a workspace in the cloud-based Power BI Service.
