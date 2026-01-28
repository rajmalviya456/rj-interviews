# Data Engineering, BI & Cloud Architecture Interview Handbook

**Target Role:** Principal Data Engineer, BI Architect, Cloud Solutions Architect  
**Focus:** Fundamentals to Advanced Production-Level Concepts

---

## Table of Contents

### Section 1 — Foundations of Data Engineering
- What is Data Engineering
- Data Warehouse vs Data Lake vs Lakehouse
- ACID Properties
- Batch vs Streaming Processing
- ETL vs ELT
- Orchestration vs Scheduling
- Data Quality Dimensions

### Section 2 — SQL Fundamentals
- Types of SQL Keys (Primary, Foreign, Unique, Composite)
- All Join Types (Inner, Left, Right, Full, Cross, Self)
- Clauses (WHERE, GROUP BY, HAVING, ORDER BY)
- Aggregations (SUM, AVG, COUNT, MIN, MAX)
- Window Functions (ROW_NUMBER, RANK, DENSE_RANK, NTILE)
- Running Total & Moving Average Queries
- Lead/Lag Functions
- CTEs (Common Table Expressions)
- Subqueries (Correlated vs Non-Correlated)
- Stored Procedures & Functions
- UDF vs Built-in Functions
- Performance Optimization
- Indexing (Clustered, Non-Clustered)
- Query Tuning & Execution Plans

### Section 3 — Python for Data Engineering
- Core Libraries (pandas, numpy, requests, boto3, sqlalchemy, pyspark)
- Pandas vs SQL Cheat Sheet
- DataFrame Operations
- Memory Management (Chunking, Dtype Optimization)
- Shallow Copy vs Deep Copy
- Python Generators (Lazy Evaluation)
- OOP Concepts (Classes, Objects, Methods, Inheritance)
- Exception Handling in Pipelines
- ACID Properties with Python Context (Delta Lake)
- Using Python in Data Pipelines

### Section 4 — Data Modeling & Warehousing
- What is Data Modeling
- Fact Tables vs Dimension Tables
- Star Schema
- Snowflake Schema
- Galaxy Schema (Fact Constellation)
- When to use Star vs Snowflake
- Database Normalization (1NF, 2NF, 3NF)
- Cardinality Types (1:1, 1:M, M:M)
- Relationship Direction (Single vs Bidirectional)
- Bridge Tables for M:M Relationships
- Slowly Changing Dimensions (SCD Type 0, 1, 2, 3, 4, 6)
- Handling Relationship Loops
- Schema Design Example (Uber)

### Section 5 — Data Pipelines & Big Data Concepts
- Pipeline Architecture (Day in the Life)
- Apache Airflow Components (DAG, Scheduler, Executors, Operators)
- Executor Types (Sequential, Local, Celery, Kubernetes)
- Data Validation in Pipelines (Great Expectations)
- File Formats (CSV, JSON, Parquet, Avro, ORC)
- Why Columnar is Faster
- Pipeline Error Handling Patterns (Retry, DLQ, Idempotency, Circuit Breaker)

### Section 6 — PySpark & Spark SQL
- Spark Architecture (Driver, Executor, Cluster Manager, Task, Stage, Job)
- What is PySpark
- RDD vs DataFrame vs Dataset
- Lazy Evaluation
- Transformations vs Actions
- Narrow vs Wide Transformations
- Anatomy of a Spark Job
- Spark SQL Basics
- Joins in Spark
- Window Functions in Spark
- Partitioning vs Repartition vs Coalesce
- Caching & Persistence (Storage Levels)
- Broadcast Join
- Handling Data Skew (Salting)
- Partition Pruning
- Spark Shuffle Deep Dive
- Performance Optimization Techniques

### Section 7 — GCP Big Data Platform
- GCP Overview for Data Engineering
- BigQuery Architecture
- BigQuery Storage vs Compute
- BigQuery Partitioning and Clustering
- BigQuery Cost Optimization (On-Demand vs Capacity)
- Nested and Repeated Fields

### Section 8 — Databricks Platform
- Databricks Architecture
- Workspace & Notebooks
- Clusters (All-Purpose vs Job Clusters)
- Jobs & Scheduling
- Unity Catalog
- IAM and Access Control
- Delta Lake
- Optimization in Databricks (Z-Order, Vacuum, Optimize)
- Connectivity with AWS, Azure, GCP
- Orchestration

### Section 9 — Azure Data Engineering Stack
- Core Components Overview
- Resource Group
- Azure Data Lake Storage Gen2 (ADLS)
- Storage Account & Tiers (Hot, Cool, Archive)
- Containers & Security (RBAC, ACLs)
- Azure Data Factory (ADF)
- Integration Runtimes (Auto-Resolve, Managed VNet, Self-Hosted)
- ADF Activities (Copy, Lookup, ForEach, If Condition, Web, Execute Pipeline)
- Creating Pipelines
- Parameters and Dynamic Parameters
- Triggers (Schedule, Tumbling Window, Event-Based)
- Notebook Integration
- Security (Azure Key Vault, Managed Identity)
- Azure Synapse Analytics (Dedicated vs Serverless)
- Handling Failed Pipelines (RCA)
- Pipeline Success but Wrong Data (Validation Strategies)
- Data Lineage (Azure Purview)
- End-to-End Medallion Architecture Project

### Section 10 — BI Tools (Power BI + Tableau)
- Power BI Architecture (Desktop, Service, Gateway)
- Tableau Architecture
- Connection Modes (Import, DirectQuery, Live, Composite)
- Handling Multiple Data Sources
- Incremental Refresh
- Dynamic Parameters
- Measures vs Calculated Columns
- DAX Basics
- Common DAX Functions (CALCULATE, FILTER, ALL, SUMX)
- Row Context vs Filter Context
- Context Transition
- DAX Engine Internals (Formula Engine vs Storage Engine)
- Row Level Security (RLS) - Static & Dynamic
- Column Level Security (CLS)
- Object Level Security (OLS)
- Publishing Reports
- Power Query (M Language)
- Query Folding
- Power Apps Integration
- Power Automate Integration
- Python Integration in BI Tools
- Filter Types (Visual, Page, Report Level)
- Data-Driven Alerts
- Semantic Model (Dataset)
- Report Performance Optimization

### Section 11 — Microsoft Fabric
- What is Microsoft Fabric
- Fabric Architecture
- Fabric vs Azure Synapse vs Azure Data Factory
- OneLake (The Heart of Fabric)
- Shortcuts (Virtual Pointers to External Data)
- Fabric Workloads (Data Factory, Engineering, Warehouse, Science, Real-Time, Power BI)
- Lakehouse vs Warehouse in Fabric
- Direct Lake Mode
- Fabric Capacity and SKUs
- When to Use Fabric vs Traditional Azure Stack

### Section 12 — Snowflake Cloud Platform
- What is Snowflake
- Snowflake Architecture (3-Layer: Cloud Services, Virtual Warehouse, Storage)
- Virtual Warehouse Sizing & Scaling
- Micro-Partitioning
- Time Travel
- Zero-Copy Cloning
- Secure Data Sharing
- Snowpipe (Continuous Ingestion)
- Streams & Tasks (CDC + Scheduling)
- Clustering Keys
- Result Caching
- Pricing Model (Storage, Compute, Cloud Services)
- Multi-Cloud Connectivity

### Section 13 — AWS Analytics Stack
- AWS Analytics Services Overview
- Amazon S3 (Storage Classes, Lifecycle Policies)
- AWS Glue (Crawlers, Jobs, Data Catalog)
- Amazon Athena (Serverless SQL on S3, Optimization)
- Amazon Redshift (Architecture, Serverless vs Provisioned, Spectrum)
- Amazon Kinesis (Data Streams, Firehose, Analytics)
- Amazon EMR (Managed Hadoop/Spark)
- AWS Lake Formation (Governance, Fine-Grained Access Control)
- Amazon QuickSight (BI Dashboards)
- IAM for Analytics
- External Tables
- Pipeline Failure Handling (Job Bookmarks, Push Down Predicates)
- End-to-End AWS Architecture Example

---



## Section 1 — Foundations of Data Engineering

### Concept End-to-End: What is Data Engineering?
> **ELI5 (Explain Like I'm 5)**: Think of Data Engineers as the "Plumbers" of data. We build the pipes (pipelines) that carry water (data) from the reservoir (source systems) to the customer's tap (dashboards and reports), filtering out the dirt (cleaning and transforming) along the way. Without good plumbing, the water either doesn't arrive, arrives dirty, or floods the house.

**Definition**: Data Engineering is the practice of designing, building, and maintaining systems for collecting, storing, transforming, and serving data at scale. It focuses on the infrastructure and architecture that enables data science and business intelligence.

**Why it is used**: 
- Raw data from source systems (databases, APIs, logs) is messy, fragmented, and stored in incompatible formats.
- Business users need data that is clean, consistent, integrated, and accessible within seconds.
- Data Engineers bridge this gap by building reliable, scalable data pipelines.

**When NOT to use Data Engineering approaches**:
- For simple, one-off analysis where data fits in a spreadsheet (<100MB).
- When there's no need for automation, scheduling, or repeatability.

**Production Scenario**:
- *Context*: An E-commerce company generates 100GB of clickstream logs daily across 50 servers.
- *Challenge*: The Marketing team needs a "Most Popular Products" report by 9 AM every morning to adjust ad spend.
- *Solution*: The Data Engineer builds an automated pipeline: `Application Logs → S3 (Raw Storage) → Apache Spark (Aggregation & Cleaning) → Snowflake (Data Warehouse) → Tableau (Visualization)`. This pipeline runs at 6 AM daily, triggered by Apache Airflow.

---

### Comparative Study: OLTP vs OLAP

Understanding the difference between OLTP and OLAP is fundamental because it dictates how you design databases, write queries, and choose technologies.

| Feature | OLTP (Online Transaction Processing) | OLAP (Online Analytical Processing) |
| :--- | :--- | :--- |
| **Primary Goal** | Capture and process individual transactions (e.g., a customer placing an order) | Analyze historical data to find trends and patterns (e.g., sales growth over 5 years) |
| **Data Source** | Application databases directly connected to web/mobile apps | Data Warehouses populated by ETL/ELT processes |
| **Read/Write Pattern** | Many small, fast reads and writes. High concurrency. | Few long-running, complex read queries. Low write frequency. |
| **Storage Architecture** | **Row-Oriented** (PostgreSQL, MySQL, Oracle). Optimized for retrieving entire rows quickly. | **Column-Oriented** (Snowflake, BigQuery, Redshift). Optimized for aggregating specific columns across millions of rows. |
| **Schema Design** | Highly **Normalized** (3NF) to eliminate data redundancy and ensure data integrity during transactions. | **Denormalized** (Star/Snowflake Schema) to minimize JOINs and maximize query speed. |
| **Latency Expectation** | Milliseconds (users expect instant feedback) | Seconds to Minutes (acceptable for complex reports) |
| **Example Query** | `SELECT * FROM Orders WHERE order_id = 12345;` | `SELECT product_category, SUM(revenue) FROM Fact_Sales GROUP BY 1 ORDER BY 2 DESC;` |

**Why Row vs Column matters**:
- **Row Storage**: Data is stored contiguously by row. `(Order1: id, customer, product, amount) | (Order2: id, customer, product, amount)`. Reading a full row is one disk seek. Excellent for OLTP.
- **Column Storage**: Data is stored contiguously by column. `(All IDs) | (All Customers) | (All Products) | (All Amounts)`. When you run `SUM(amount)`, the database only reads the `amount` column, skipping everything else. This can be 100x faster for analytics.

---

### Data Warehouse vs Data Lake vs Lakehouse

These three architectures represent the evolution of data storage paradigms. Understanding when to use each is critical for designing modern data platforms.

| Feature | Data Warehouse | Data Lake | Lakehouse |
| :--- | :--- | :--- | :--- |
| **Data Structure** | Structured only (Tables with defined schemas) | Structured, Semi-Structured (JSON, XML), and Unstructured (Images, PDFs) | All data types |
| **Schema Enforcement** | **Schema-on-Write**: Data must conform to a schema *before* being loaded. Strict. | **Schema-on-Read**: Raw data is stored first; schema is applied when queried. Flexible. | Both (Schema-on-Write for curated tables, Schema-on-Read for raw) |
| **Storage Cost** | High (Proprietary, optimized storage engines) | Low (Cheap object storage like S3, ADLS, GCS) | Low (Uses object storage) |
| **ACID Transactions** | Yes (Built-in) | No (Files can be overwritten, leading to corruption) | **Yes** (via Delta Lake, Apache Iceberg, or Apache Hudi) |
| **Query Performance** | Excellent (Optimized for SQL analytics) | Variable (Depends on file format and query engine) | Excellent (Combines open formats with optimizers) |
| **Primary Use Case** | Business Intelligence reporting, financial audits | Data Science/ML training data, log archival, exploration | Unified platform for BI and AI on same data |
| **Example Technologies** | Snowflake, Amazon Redshift, Google BigQuery, Azure Synapse Dedicated SQL Pool | Amazon S3 + AWS Glue Catalog, Azure Data Lake Storage Gen2 | Databricks (Delta Lake), Apache Iceberg on Spark, Microsoft Fabric |

**Deep Dive: Why Lakehouse?**
- Traditional approach: Copy data from Lake → Warehouse. This leads to data duplication, increased cost, and delayed freshness.
- Lakehouse approach: Store data *once* in open formats (Parquet) on cheap storage (S3/ADLS), then add a **Transactional Layer** (Delta Lake) that provides ACID guarantees and a **Metadata Layer** (Unity Catalog) for governance. Both BI dashboards and ML notebooks query the *same* data without costly copies.

---

### Batch Processing vs Streaming Processing

Data can flow through your systems in two fundamentally different ways. Choosing the right approach depends on your latency requirements and complexity budget.

**Batch Processing**:
- **Definition**: Collecting data over a period of time and processing it all at once at a scheduled interval (e.g., every hour, every night).
- **Latency**: High (minutes to hours). The data is always at least as old as the batch interval.
- **Throughput**: High. Processing happens on large chunks of data, which is efficient.
- **Complexity**: Lower. Easier to implement, test, and debug because data is bounded (finite).
- **Use Cases**: Daily sales reports, monthly billing calculations, historical trend analysis.
- **Technologies**: Apache Spark (Batch), AWS Glue, Azure Data Factory.

**Streaming Processing**:
- **Definition**: Processing data continuously as each event arrives, in near real-time.
- **Latency**: Low (milliseconds to seconds). Data is fresh.
- **Throughput**: Variable. Depends on event rate.
- **Complexity**: Higher. Must handle unbounded data, late-arriving events, out-of-order events, and exactly-once semantics.
- **Use Cases**: Fraud detection (must block transaction immediately), live sports score updates, real-time inventory alerts.
- **Technologies**: Apache Kafka, Apache Flink, Spark Structured Streaming, Amazon Kinesis.

**Scenario Question**: "Our e-commerce site needs to show 'Low Stock' warnings when inventory drops below 10. Should we use Batch or Streaming?"
- **Answer**: Streaming. If you use a daily batch, a product might sell out completely before the batch runs, leading to customer frustration. A streaming pipeline updates the flag within seconds of each sale.

---

### ETL vs ELT

These acronyms describe the order of operations in a data pipeline. The choice significantly impacts your architecture.

**ETL (Extract, Transform, Load)**:
- **Flow**: Extract data from source → **Transform** it in a separate processing engine (e.g., Informatica, SSIS, a Python script on a server) → Load the clean, transformed data into the target warehouse.
- **Historical Context**: Popular when data warehouses had limited compute power. Transformation happened "outside" on dedicated ETL servers.
- **Pros**: Transformed data is clean before landing. Good for situations where PII (Personally Identifiable Information) must be masked *before* data enters the destination (compliance reasons).
- **Cons**: ETL tools can become bottlenecks. Added infrastructure to manage.

**ELT (Extract, Load, Transform)**:
- **Flow**: Extract data from source → Load it **raw** into the target warehouse → **Transform** it *inside* the warehouse using SQL.
- **Modern Context**: Cloud warehouses (Snowflake, BigQuery, Databricks) have virtually unlimited compute power. It's faster and cheaper to transform data *inside* these systems.
- **Pros**: No separate ETL server needed. Preserves raw data (you can re-transform if business logic changes). Leverages MPP (Massively Parallel Processing) of the cloud warehouse.
- **Cons**: Raw, potentially messy data lands in the warehouse first. Requires strong governance to ensure raw zones are not queried directly by end-users.

**Industry Trend**: ELT is now the dominant pattern for cloud-native data platforms. Tools like **dbt (Data Build Tool)** are specifically designed for the "T" in ELT, enabling SQL-based transformations inside the warehouse.

---

### Orchestration vs Scheduling

These terms are often confused but represent different levels of pipeline management sophistication.

**Scheduling**:
- **Definition**: Triggering a single job at a specific time. "Run script X at 9 AM."
- **Tool**: Cron (Linux scheduler), Windows Task Scheduler.
- **Limitations**: No awareness of job dependencies. If Job A fails, Cron will still happily start Job B that depends on Job A's output. No easy way to monitor, alert, or backfill.

**Orchestration**:
- **Definition**: Managing the execution of a complex graph of interdependent tasks, including retries, error handling, alerting, and historical backfilling.
- **Tool**: Apache Airflow, Prefect, Dagster, Azure Data Factory.
- **Capabilities**:
    - **DAG (Directed Acyclic Graph)**: Define Task A → Task B → Task C. If A fails, B and C don't run.
    - **Retries**: If Task A fails due to a network blip, retry 3 times with a 5-minute delay.
    - **Alerting**: If retries fail, send an email to oncall@company.com.
    - **Backfilling**: If yesterday's pipeline failed, re-run it for that specific date without affecting today's run.
    - **Monitoring**: Visual UI showing green (success) and red (failure) for each run.

**Scenario Question**: "We have 5 Python scripts that run sequentially every night. Should we use Cron or Airflow?"
- **Answer**: Airflow. The moment script 2 fails, Cron will still run scripts 3, 4, 5 on potentially corrupt data. Airflow will halt the DAG at step 2, alert you, and prevent downstream corruption.

---

### Data Quality Concepts

High-quality data is the foundation of trust in any data platform. Without it, dashboards are wrong, ML models are biased, and business decisions are flawed.

**Dimensions of Data Quality**:
1. **Completeness**: Is all required data present? (e.g., Are there NULL values in the `email` column where it's mandatory?)
2. **Accuracy**: Is the data correct and reflective of reality? (e.g., Does the `price` column match the actual price in the source system?)
3. **Consistency**: Is the data consistent across different systems? (e.g., Is the customer `John Doe` in the CRM the same as `J. Doe` in the billing system?)
4. **Timeliness (Freshness)**: Is the data available when needed? (e.g., Is the sales data ready by 8 AM SLA?)
5. **Uniqueness**: Is each record represented only once? (e.g., are there duplicate `order_id` values?)
6. **Validity (Conformity)**: Does the data conform to the expected format? (e.g., Is the `email` column a valid email format?)

**Tools for Data Quality**: Great Expectations, Soda Core, dbt Tests.

**Production Scenario**: 
- A pipeline loads customer data. The `country_code` column should only contain valid 2-letter ISO codes.
- A Great Expectations test is added: `expect_column_values_to_be_in_set(column='country_code', value_set=['US', 'CA', 'GB', ...])`.
- If a source sends `USA` instead of `US`, the pipeline fails early, and the engineering team is alerted *before* the bad data pollutes the warehouse.

---

### ACID Properties in Analytics Systems

ACID guarantees are essential for transactional databases and are now becoming critical for data lakes (via Lakehouses) to ensure data reliability.

**Atomicity**: 
- **Definition**: A transaction is "all or nothing." Either all operations within the transaction succeed, or none of them do. There is no partial state.
- **Example**: You're writing 100 Parquet files to a Delta Lake table. If the job fails after writing 50, Atomicity ensures those 50 partial files are not visible to readers. The transaction is rolled back.

**Consistency**: 
- **Definition**: A transaction brings the database from one valid state to another valid state, respecting all defined rules (constraints, triggers).
- **Example**: A foreign key constraint ensures you cannot insert an `order` with a `customer_id` that doesn't exist in the `customers` table.

**Isolation**: 
- **Definition**: Concurrent transactions do not interfere with each other. A reader does not see the "in-progress" writes of a writer.
- **Example (Snapshot Isolation in Delta Lake)**: While a Spark job is writing new data to a table, a BI tool can query the table and will see the *old*, complete version. Once the write commits, subsequent queries see the new version.

**Durability**: 
- **Definition**: Once a transaction is committed, the data is permanently saved, even if the system crashes immediately after.
- **Example**: In cloud storage (S3/ADLS), files are replicated across multiple availability zones. A commit to Delta Lake means the data is durable.

**Why ACID in Lakehouses?**
- Traditional Data Lakes (just Parquet files on S3) lack ACID. A failed job could leave partial files, corrupting the dataset.
- Delta Lake, Apache Iceberg, and Apache Hudi add a **Transaction Log** that records all commits. This log is the source of truth, enabling rollback, time travel, and concurrent access.

---

## Section 2 — SQL Fundamentals

### SQL Keys (Prerequisites)
- **Primary Key**: Unique, Not Null identification of a row.
- **Foreign Key**: Enforces referential integrity links to another table's PK.
- **Composite Key**: A PK made of multiple columns (e.g., `Order_ID` + `Line_Item_ID`).
- **Surrogate Key**: System-generated artificial key (e.g., `SEQ_ID: 101`).
  - *Why*: Decouples DB internal ID from volatile business keys (e.g., Employee ID might change if company merges).
  - *When*: Almost always in Data Warehousing Dimensions.
- **Natural Key**: Business identifier (e.g., SSN, Email).

### Join Types
- **Inner Join**: Returns matching rows.
- **Left Join**: All from Left, matches from Right. (Most common in Analytics to keep source rows).
- **Right Join**: All from Right, matches from Left. (Rare, usually rewritten as Left).
- **Full Outer Join**: All rows from both. (Used for comparing two datasets).
- **Cross Join**: Cartesian Product.
  - *Use Case*: Generating a "Date Spine" (All Dates x All Products) to fill gaps in sales data.
  - *Mistake*: Accidentally creating billions of rows by crossing two large tables.
- **Self Join**: Joining a table to itself.
  - *Use Case*: Employee Manager Hierarchy (Manager ID points to Employee ID in same table).

### SQL Clauses Deep Dive
- **WHERE vs HAVING**: 
  - `WHERE`: Filters rows *before* aggregation. (Cannot use aliases usually).
  - `HAVING`: Filters groups *after* aggregation.
- **GROUP BY Extensions**: `ROLLUP` (Subtotals), `CUBE` (All combinations), `GROUPING SETS`.
- **ORDER BY**: Performance killer on large datasets. Use `LIMIT`.

### Aggregations & Expressions
- **Aggregations**: `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`. `COUNT(DISTINCT x)` is expensive.
- **CASE WHEN**: Conditional logic.
  ```sql
  CASE WHEN amount > 1000 THEN 'High' ELSE 'Low' END
  ```
- **Coalesce**: Returns first non-null value. `COALESCE(address, 'Unknown')`.

### Window Functions (Critical)
- **Concept**: Perform calculations across a set of table rows related to the current row. Does NOT collapse rows like Group By.
- **Syntax**: `FUNCTION() OVER (PARTITION BY ... ORDER BY ... [FRAME])`
- **Ranking**:
  - `ROW_NUMBER()`: Unique 1, 2, 3, 4. (Used for de-duplication).
  - `RANK()`: 1, 2, 2, 4. (Skips on tie).
  - `DENSE_RANK()`: 1, 2, 2, 3. (No skip).
- **Value**:
  - `LEAD(col)`: Next row's value.
  - `LAG(col)`: Previous row's value. (YoY calculation).
- **Running Total**:
  ```sql
  SUM(sales) OVER (PARTITION BY region ORDER BY date ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
  ```

### CTE vs Subqueries
- **CTE (Common Table Expression)**: `WITH` clause.
  - *Pros*: Readable, reusable within query.
- **Subquery**: Nested `SELECT`.
  - *Cons*: Hard to read "inside-out".

### Stored Procedures vs Functions vs UDF
- **Stored Procedure**:
  - *Use*: Administrative tasks, complex logic using control flow (IF/ELSE), Transactions.
  - *Call*: `CALL my_proc()`.
- **User Defined Function (UDF)**:
  - *Use*: Encapsulate logic used in `SELECT`. Returns a value.
  - *Performance*: **Scalar UDFs** are often performance killers (run row-by-row). Prefer native SQL functions.
- **Table Valued Function (TVF)**: Returns a table.

### Query Optimization & Performance Tuning
- **Execution Plan Analysis**:
  - Look for **Table Scans** on large tables (index missing?).
  - Look for **Nested Loop Joins** on heavy datasets (should be Hash Join).
  - Look for **Spill to Disk** (Sort memory insufficient).
- **Techniques**:
  1. **Filter Early**: Reduce data volume before joining.
  2. **Index**: Add Clustered/Non-Clustered indexes on Join/Filter keys.
  3. **Partition Pruning**: Filter on partition column (e.g., `date`).
  4. **Avoid `SELECT *`**: Columnar storage must read all columns.
  5. **Statistics**: Ensure stats are up to date so optimizer chooses right plan.

---

## Section 3 — Python for Data Engineering

### Python Basics & Core Libraries

Python is the lingua franca of data engineering due to its readability, vast library ecosystem, and strong community support.

**Core Libraries for Data Engineers**:
| Library | Purpose | Example Use Case |
| :--- | :--- | :--- |
| `pandas` | In-memory tabular data manipulation | Cleaning a CSV, joining datasets |
| `numpy` | Numerical computing, array operations | Matrix math, efficient calculations |
| `requests` | HTTP requests to APIs | Fetching data from a REST API |
| `boto3` | AWS SDK for Python | Reading/writing files to S3 |
| `sqlalchemy` | Database abstraction / ORM | Connecting to PostgreSQL, executing SQL |
| `pyspark` | Distributed data processing | Processing terabytes of data on a Spark cluster |

**Key Python Data Structures**:
- **List**: Ordered, mutable collection. `my_list = [1, 2, 3]`. Use for sequences where you need to add/remove items.
- **Tuple**: Ordered, immutable collection. `my_tuple = (1, 2, 3)`. Use for fixed data like coordinates or database rows.
- **Dictionary**: Key-value pairs. `my_dict = {'name': 'Alice', 'age': 30}`. Use for fast lookups by key (O(1) average).
- **Set**: Unordered, unique elements. `my_set = {1, 2, 3}`. Use for membership testing and removing duplicates.

---

### Pandas vs SQL Translation Table (Cheat Sheet)

For anyone coming from a SQL background, this table shows the direct equivalents in Pandas.

| Operation | SQL Syntax | Pandas Syntax |
| :--- | :--- | :--- |
| **Select Columns** | `SELECT colA, colB FROM table` | `df[['colA', 'colB']]` |
| **Filter Rows** | `WHERE amount > 50` | `df[df['amount'] > 50]` |
| **Group By & Aggregate** | `SELECT region, SUM(sales) FROM t GROUP BY region` | `df.groupby('region')['sales'].sum()` |
| **Inner Join** | `SELECT * FROM A INNER JOIN B ON A.id = B.id` | `pd.merge(dfA, dfB, on='id', how='inner')` |
| **Left Join** | `SELECT * FROM A LEFT JOIN B ON A.id = B.id` | `pd.merge(dfA, dfB, on='id', how='left')` |
| **Union All** | `SELECT * FROM A UNION ALL SELECT * FROM B` | `pd.concat([dfA, dfB], ignore_index=True)` |
| **Distinct Values** | `SELECT DISTINCT col FROM table` | `df['col'].unique()` or `df.drop_duplicates(subset=['col'])` |
| **Order By** | `ORDER BY col DESC` | `df.sort_values(by='col', ascending=False)` |
| **Limit** | `LIMIT 10` | `df.head(10)` |

---

### Memory Management Deep Dive

Understanding how Pandas uses memory is critical for avoiding crashes when processing large datasets.

**The Problem**:
- Pandas loads the *entire* dataset into RAM before any processing.
- A 2GB CSV file on disk can easily consume 10GB+ of RAM when loaded, because:
    - Python objects have overhead (a single Python integer is ~28 bytes).
    - Strings are stored as Python objects, not as compact byte arrays.
- If your machine has 16GB RAM and you try to load a 10GB CSV, your script will crash with `MemoryError`.

**Optimization Strategies**:

1. **Chunking (Batch Processing)**:
   - Instead of loading the entire file, process it in smaller pieces.
   ```python
   import pandas as pd
   
   results = []
   for chunk in pd.read_csv('huge_file.csv', chunksize=100000):
       # Process each chunk (e.g., filter, aggregate)
       processed = chunk[chunk['status'] == 'active']
       results.append(processed)
   
   # Combine all processed chunks
   final_df = pd.concat(results, ignore_index=True)
   ```
   - **When to use**: When you cannot fit the entire file in memory, or when you only need a subset of the data.

2. **Data Type Optimization**:
   - By default, Pandas uses `int64` and `float64` which consume 8 bytes per value.
   - If your values are small (e.g., ages 0-120), downcast to `int8` (1 byte).
   - For string columns with low cardinality (e.g., `status` with values 'active'/'inactive'), use `category` dtype.
   ```python
   df['age'] = df['age'].astype('int8')
   df['status'] = df['status'].astype('category')
   # Memory reduction can be 10x or more
   ```

---

### Shallow Copy vs Deep Copy (Interview Favorite)

This is a classic Python interview question that tests understanding of how objects are stored in memory.

**Assignment (`=`)**:
- Does NOT create a copy. Just creates a new reference (pointer) to the *same* object in memory.
- Modifying the new variable modifies the original.
```python
list1 = [1, 2, [3, 4]]
list2 = list1  # list2 points to the SAME object as list1
list2[0] = 99
print(list1)  # Output: [99, 2, [3, 4]] - list1 is also changed!
```

**Shallow Copy (`copy.copy()` or `.copy()`)**:
- Creates a *new* outer object, but the *nested* objects inside are still references to the original.
- Modifying top-level elements in the copy is safe. Modifying nested elements affects both.
```python
import copy
list1 = [1, 2, [3, 4]]
list2 = copy.copy(list1)  # or list1.copy()
list2[0] = 99             # Safe: list1[0] is still 1
list2[2][0] = 999         # Danger! list1[2] is also changed
print(list1)              # Output: [1, 2, [999, 4]]
```

**Deep Copy (`copy.deepcopy()`)**:
- Recursively creates copies of *all* nested objects. Completely independent.
- Safe to modify at any level.
```python
import copy
list1 = [1, 2, [3, 4]]
list2 = copy.deepcopy(list1)
list2[2][0] = 999
print(list1)  # Output: [1, 2, [3, 4]] - list1 is unchanged!
```

**When to use which?**:
- Use `=` when you *want* changes to reflect in both places (rare).
- Use **shallow copy** when you have a flat structure (no nested lists/dicts).
- Use **deep copy** when you have nested structures and need full independence.

---

### Python Generator (Lazy Evaluation)

Generators are a powerful Python feature for processing large sequences without loading them all into memory.

**The Problem with Lists**:
- A list comprehension creates the *entire* list in memory before you can iterate over it.
- `[i*i for i in range(10_000_000)]` creates a list of 10 million integers (~80MB).

**The Generator Solution**:
- A generator yields one item at a time. It only computes the next value when asked.
- `(i*i for i in range(10_000_000))` uses almost no memory regardless of range size.

```python
# List (Eager Evaluation) - High Memory Usage
def get_squares_list(n):
    return [i*i for i in range(n)]

# Generator (Lazy Evaluation) - Low Memory Usage
def get_squares_generator(n):
    for i in range(n):
        yield i*i

# Usage
for square in get_squares_generator(10_000_000):
    if square > 100:
        break  # We only iterated a few times, didn't compute 10 million values!
```

**Use Cases in Data Engineering**:
- Reading and processing a large file line by line without loading the whole file.
- Streaming data from an API response.

---

### OOP (Object Oriented Programming) in Data Engineering

While DE often favors functional programming for transformations, OOP is essential for building reusable, testable pipeline components.

**Core Concepts**:

1. **Class**: A blueprint for creating objects. Defines attributes (data) and methods (functions).
2. **Object**: An instance of a class.
3. **`__init__` (Constructor)**: A special method called when an object is created, used to initialize attributes.
4. **Encapsulation**: Bundling data and methods that operate on that data, and hiding internal details. Prefixing an attribute with `_` signals it's private.
5. **Inheritance**: Creating a new class that "inherits" attributes and methods from a parent class.

**Real-World Example: A Reusable Pipeline Class**

```python
class DataPipeline:
    """A reusable base class for data pipelines."""
    
    def __init__(self, source_path: str, destination_table: str, env: str = 'dev'):
        self.source_path = source_path
        self.destination_table = destination_table
        self.env = env
        self._connection = None  # Private attribute
        
    def connect(self):
        """Establish connection to the data warehouse."""
        print(f"Connecting to {self.env} environment...")
        # self._connection = create_connection(...)
        
    def extract(self):
        """Read data from source."""
        print(f"Reading from {self.source_path}")
        # return spark.read.parquet(self.source_path)
        
    def transform(self, df):
        """Apply transformations. Override in child classes."""
        raise NotImplementedError("Subclasses must implement transform()")
        
    def load(self, df):
        """Write data to destination."""
        print(f"Writing to {self.destination_table}")
        # df.write.mode('overwrite').saveAsTable(self.destination_table)
        
    def run(self):
        """Execute the full pipeline."""
        self.connect()
        raw_df = self.extract()
        transformed_df = self.transform(raw_df)
        self.load(transformed_df)
        print("Pipeline complete!")


class SalesDataPipeline(DataPipeline):
    """Specific pipeline for sales data."""
    
    def transform(self, df):
        """Implement specific sales transformations."""
        # return df.filter(df['amount'] > 0).dropDuplicates(['order_id'])
        print("Applying sales-specific transformations...")
        return df

# Usage
pipeline = SalesDataPipeline(
    source_path='s3://bucket/raw/sales/',
    destination_table='curated.fact_sales',
    env='prod'
)
pipeline.run()
```

---

### Exception Handling in Pipelines

Robust pipelines must handle errors gracefully without crashing unexpectedly.

**Best Practices**:
1. **Catch Specific Exceptions**: Avoid bare `except:` clauses. They hide bugs.
2. **Log Errors with Context**: Include the error message, timestamp, and relevant variables.
3. **Implement Retries for Transient Failures**: Network issues, temporary API outages.
4. **Fail Fast for Unrecoverable Errors**: Don't retry if the problem is bad data or logic errors.

```python
import time
import logging
import requests

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

def fetch_data_with_retry(api_url: str, max_retries: int = 3, backoff_factor: float = 2.0):
    """Fetches data from an API with exponential backoff retry logic."""
    
    for attempt in range(1, max_retries + 1):
        try:
            logger.info(f"Attempt {attempt}: Fetching data from {api_url}")
            response = requests.get(api_url, timeout=30)
            response.raise_for_status()  # Raises HTTPError for 4xx/5xx status codes
            return response.json()
            
        except requests.exceptions.Timeout as e:
            logger.warning(f"Timeout on attempt {attempt}. Retrying...")
            time.sleep(backoff_factor ** attempt)  # Exponential backoff: 2, 4, 8 seconds
            
        except requests.exceptions.HTTPError as e:
            if response.status_code == 429:  # Rate limited
                logger.warning("Rate limited. Backing off...")
                time.sleep(60)
            elif response.status_code >= 500:  # Server error, may be transient
                logger.warning(f"Server error {response.status_code}. Retrying...")
                time.sleep(backoff_factor ** attempt)
            else:
                logger.error(f"Non-retryable HTTP error: {e}")
                raise  # Re-raise for non-retryable client errors (4xx)
                
        except requests.exceptions.ConnectionError as e:
            logger.warning(f"Connection error: {e}. Retrying...")
            time.sleep(backoff_factor ** attempt)
    
    raise Exception(f"Failed to fetch data after {max_retries} attempts")
```

---

### ACID Concepts with Python Context

While Python itself doesn't provide ACID guarantees (it's a programming language, not a database), Python libraries *implement* ACID when writing to data lakes.

**How Delta Lake Provides ACID in Python (PySpark)**:

1. **Atomicity**: When you run `df.write.format("delta").save(...)`, the write is atomic. If the Spark job fails midway, the partial Parquet files are NOT visible to readers. The `_delta_log` folder tracks committed transactions.

2. **Consistency**: Delta Lake enforces schema consistency. If you try to write a DataFrame with a different schema, the write fails (unless you explicitly enable schema evolution).

3. **Isolation (Snapshot Isolation)**: While a write is in progress, readers see the *previous* version of the table. After commit, new readers see the new version. This is called `Serializable Snapshot Isolation`.

4. **Durability**: Once a commit is written to the `_delta_log`, the data is durable. Delta Lake uses cloud object storage (S3, ADLS) which provides multi-AZ replication.

```python
# Example: ACID Write with Delta Lake
from delta.tables import DeltaTable

# This write is ATOMIC
df.write \
    .format("delta") \
    .mode("append") \
    .save("s3://my-bucket/delta/sales/")

# Even if the job fails after writing 50 out of 100 files,
# readers will NOT see those 50 partial files.
```

---


## Section 4 — Data Modeling & Warehousing

Data Modeling is the process of designing the structure of your data to optimize for storage, querying, and understanding. It's a critical skill for anyone working with data warehouses or BI tools.

---

### What is Data Modeling?

**Definition**: Data modeling is the process of creating a visual representation of a data system, defining how data is connected, stored, and accessed. It's like creating a blueprint before building a house.

**Why it matters**:
- A good data model makes queries fast and intuitive.
- A bad data model leads to slow reports, confusing metrics, and maintenance nightmares.

---

### Fact Tables vs Dimension Tables

This is the most fundamental concept in dimensional modeling (the basis of Data Warehousing).

**Fact Table**:
- **Contains**: Quantitative, measurable data (metrics). The "numbers" you want to analyze.
- **Shape**: Tall and narrow (millions/billions of rows, fewer columns).
- **Grain**: Defined by the level of detail. "One row per order" vs "One row per order line item" are different grains.
- **Keys**: Contains foreign keys pointing to dimension tables.
- **Examples**: `Fact_Sales` (columns: `Sale_Amount`, `Quantity_Sold`, `Discount`), `Fact_Clicks` (columns: `Click_Count`, `Session_Duration`).

**Dimension Table**:
- **Contains**: Descriptive, contextual data (attributes). The "Who, What, Where, When" of your metrics.
- **Shape**: Short and wide (fewer rows, many columns for attributes).
- **Keys**: Contains a primary key (usually a Surrogate Key) that the Fact table references.
- **Examples**: `Dim_Customer` (columns: `Customer_Name`, `Email`, `City`, `Signup_Date`), `Dim_Product` (columns: `Product_Name`, `Category`, `Brand`, `Price`).

**Analogy**:
- **Fact Table**: The verb (what happened). "A sale occurred."
- **Dimension Table**: The adjectives/nouns (who, what, when). "Alice bought a Red Jacket in New York on Tuesday."

---

### Star Schema vs Snowflake Schema

These are the two primary patterns for organizing Fact and Dimension tables.

**Star Schema**:
- **Structure**: A central Fact table connected directly to multiple Dimension tables. The diagram looks like a star.
- **Characteristics**: Dimensions are **denormalized**. All attributes for a dimension are in a single table.
- **Example**:
  ```
             [Dim_Customer]
                   │
                   ▼
  [Dim_Product]──►[Fact_Sales]◄──[Dim_Date]
                   ▲
                   │
             [Dim_Store]
  ```
- **Pros**:
    - **Simpler Queries**: Fewer JOINs needed.
    - **Faster Performance**: BI tools (Power BI, Tableau) are optimized for Star Schemas.
    - **Easier to Understand**: Business users can navigate the model easily.
- **Cons**:
    - **Data Redundancy**: `Dim_Customer` might repeat "USA" for every American customer.
    - **Larger Storage**: Denormalization means more disk space.
- **Verdict**: **Use Star Schema by default** for BI/Analytics. It's the industry standard.

**Snowflake Schema**:
- **Structure**: Dimensions are **normalized** into sub-dimensions. A dimension table links to another dimension table.
- **Example**:
  ```
  ┌──────────────────────────────────────────────────────────────┐
  │                                                              │
  │   [Dim_Country]◄──[Dim_State]◄──[Dim_Customer]               │
  │                                        │                     │
  │                                        ▼                     │
  │   [Dim_Category]◄──[Dim_Product]──►[Fact_Sales]◄──[Dim_Date] │
  │                                                              │
  └──────────────────────────────────────────────────────────────┘
  ```
  **Reading the diagram**: Notice how dimensions are "snowflaked" (normalized):
  - `Dim_Customer` → `Dim_State` → `Dim_Country` (3-level hierarchy)
  - `Dim_Product` → `Dim_Category` (2-level hierarchy)
  - The Fact table (`Fact_Sales`) connects to normalized dimension chains
- **Pros**:
    - **Less Data Redundancy**: "USA" is stored once in `Dim_Country`.
    - **Smaller Storage Footprint**.
    - **Easier Attribute Updates**: Change "United States" to "USA" in one place.
- **Cons**:
    - **Complex Queries**: More JOINs required.
    - **Slower Performance**: Complex JOINs are expensive.
    - **Harder for Business Users**: The model is less intuitive.
- **When to use**: When storage cost is a major concern, or when dimension updates are frequent and must be atomic.

---

### Galaxy Schema (Fact Constellation)

- **Definition**: Multiple Fact tables sharing common Dimension tables (called **Conformed Dimensions**).
- **Example**: An enterprise might have `Fact_Sales` and `Fact_Inventory` both using `Dim_Product` and `Dim_Date`.
- **Benefit**: Enables cross-functional analysis (e.g., "Show me products where Sales are high but Inventory is low").

---

### Database Normalization (1NF to 3NF)

Normalization is the process of organizing data to reduce redundancy. It's essential for OLTP systems but often **reversed (denormalized)** in OLAP systems.

**1NF (First Normal Form)**:
- Rule: Each cell contains a **single, atomic value**. No repeating groups or arrays.
- **Bad**: A `Books` table with an `Authors` column containing "J.K. Rowling, Stephen King".
- **Good**: Separate `Books` and `Authors` tables with a linking `Book_Authors` table.

**2NF (Second Normal Form)**:
- Rule: Must be in 1NF, AND all non-key columns must depend on the **entire primary key** (no partial dependency).
- **Applies to**: Tables with composite primary keys.
- **Example**: If PK is (`Order_ID`, `Product_ID`), then `Product_Name` depends only on `Product_ID` (partial dependency). Move `Product_Name` to a separate `Products` table.

**3NF (Third Normal Form)**:
- Rule: Must be in 2NF, AND no non-key column should depend on another non-key column (no transitive dependency).
- **Example**: `Customer_City` depends on `Customer_ID`, but `Customer_State` depends on `Customer_City`. Move `City-State` mapping to a separate table.

**Why 3NF for OLTP but not OLAP?**
- **OLTP**: High frequency of updates. If "USA" is stored 1 million times and you need to change it to "United States", you have 1 million updates. 3NF stores it once.
- **OLAP**: Read-heavy, write-rare. JOINing 5 normalized tables for every dashboard is slow. Denormalize into a Star Schema for speed.

---

### Cardinality & Relationships

Cardinality describes the numerical relationship between two tables.

**Types**:
| Type | Description | Example | Common? |
| :--- | :--- | :--- | :--- |
| **One-to-One (1:1)** | Each row in Table A matches exactly one row in Table B. | `Person` ↔ `Passport` (one person, one passport) | Rare |
| **One-to-Many (1:M)** | Each row in Table A can match multiple rows in Table B. | `Customer` → `Orders` (one customer, many orders) | **Most Common** |
| **Many-to-Many (M:M)** | Rows in Table A can match multiple rows in Table B, and vice versa. | `Student` ↔ `Class` (many students, many classes) | Problematic |

**Why is Many-to-Many (M:M) Problematic?**
- BI tools (Power BI, Tableau) struggle with M:M relationships. They can cause:
    - **Row Proliferation (Cartesian Explosion)**: Joining a M:M directly produces NxM rows.
    - **Ambiguous Totals**: `SUM(Sales)` might be double-counted or incorrect.

**Solution: Bridge Table (Junction Table)**:
- Resolve M:M into two 1:M relationships using a "bridge" table.
- **Example**: `Student` (1) → `Student_Class` ← (M) `Class`. Each row in `Student_Class` represents one student enrolled in one class.

---

### Relationship Direction (Single vs Bidirectional)

In BI tools, filters propagate along relationships. The direction matters.

**Single Direction (One-way)**:
- Filters flow from the "One" side (Dimension) to the "Many" side (Fact).
- **Example**: Selecting "2024" in `Dim_Date` filters `Fact_Sales` to show only 2024 sales. This is expected.
- **Performance**: Fast. Efficient.
- **Default Recommendation**: **Always use Single Direction** unless strictly necessary.

**Bidirectional (Both ways)**:
- Filters flow in *both* directions. Selecting a Product also filters Customers who bought that product.
- **Problem**:
    - **Performance Cost**: The engine must calculate filters in multiple directions.
    - **Ambiguity**: Can create circular filter paths, leading to errors or incorrect results.
- **When to use**: Limited scenarios like M:M bridge tables where you need to filter both sides.

---

### The 6 Types of Slowly Changing Dimensions (SCD)

Dimension data changes over time (e.g., a customer moves to a new city). SCDs define how to handle these changes.

| Type | Name | Logic | History Preserved? | Complexity | Use Case |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Type 0** | Fixed / Retain Original | Ignore all changes. Keep the original value forever. | No | Very Low | Date of Birth, SSN (immutable data) |
| **Type 1** | Overwrite | Update the record directly. The old value is lost. | No | Low | Correcting data entry errors, non-critical attributes |
| **Type 2** | Add New Row | Close the old row (set `End_Date`, `Is_Current = False`), insert a new row. | **Yes (Full)** | High | Customer Address (for accurate historical reporting: "Sales by City in 2020") |
| **Type 3** | Add New Column | Add a `Previous_Value` column to store the last value. | Partial (1 history) | Medium | When you only need to compare "current vs previous" (e.g., current salary vs previous salary) |
| **Type 4** | History Table (Mini-Dimension) | Store current values in the main dimension table. Store *all* historical values in a separate history table. | Yes (separate table) | High | When history is rarely queried but must be retained for audit |
| **Type 6** | Hybrid (1+2+3) | Combines Type 1, 2, and 3. Add a new row (Type 2), but also update a `Current_Value` column on all historical rows (Type 1), and store `Previous_Value` (Type 3). | Yes (Rich) | Very High | When you need both historical accuracy *and* easy access to the current value from any row |

**Deep Dive: SCD Type 2 Implementation (Most Common for Analytics)**

You need extra columns in the dimension table:
- `Surrogate_Key`: A unique, auto-incrementing ID for each row version.
- `Effective_Start_Date`: When this version of the record became active.
- `Effective_End_Date`: When this version was superseded (NULL or '9999-12-31' for current).
- `Is_Current`: A boolean flag (`TRUE` for the active record).

| Surrogate_Key | Customer_ID | Customer_Name | City | Effective_Start | Effective_End | Is_Current |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 101 | C001 | Alice | New York | 2020-01-01 | 2023-06-15 | FALSE |
| 102 | C001 | Alice | Los Angeles | 2023-06-16 | 9999-12-31 | TRUE |

Now, when reporting "Sales in New York for 2022", the JOIN uses `Fact_Sales.Customer_SK = 101` (the old record).

---

### Handling Relationship Loops (Ambiguity in BI Models)

A model can accidentally create a loop where filters propagate in a circle, causing errors.

**Scenario**:
- `Fact_Sales` → `Dim_Product` → `Dim_Category`
- `Dim_Category` → `Dim_Sales_Target` → `Fact_Sales`
- This creates a loop.

**Problem**: The BI tool cannot determine which path filters should take. It throws an "ambiguous path" error or produces wrong results.

**Solutions**:
1. **Deactivate One Relationship**: In Power BI, set one relationship to "Inactive". Use `USERELATIONSHIP()` DAX function only when needed for a specific calculation.
2. **Role-Playing Dimension**: Create copies of the dimension table for each purpose (e.g., `Dim_Ship_Date`, `Dim_Order_Date` instead of a single `Dim_Date`).

---

### Designing a Schema for Uber (Conceptual Example)

**The Ask**: "Design a fact/dimension model for Uber's ride data."

**Step 1: Identify the Grain (Level of Detail)**
- Grain: **One row per completed trip**. This is our Fact table.

**Step 2: Identify the Metrics (What we measure)**
- `Fare_Amount`, `Tip_Amount`, `Distance_Miles`, `Duration_Minutes`, `Surge_Multiplier`.

**Step 3: Identify the Dimensions (Context for the metrics)**
- **Dim_Driver**: `Driver_ID`, `Name`, `Rating`, `Car_Type`, `Signup_Date`.
- **Dim_Rider**: `Rider_ID`, `Name`, `Account_Type` (Regular/Premium), `City`.
- **Dim_Location**: `Location_ID`, `Latitude`, `Longitude`, `City`, `Zip_Code`, `Neighborhood`. (Could be SCD Type 2 if neighborhood boundaries change).
- **Dim_Date**: `Date_ID`, `Date`, `Day_of_Week`, `Month`, `Quarter`, `Year`, `Is_Holiday`.
- **Dim_Time**: `Time_ID`, `Hour`, `Minute`, `Is_Rush_Hour`.

**Step 4: Design the Fact Table**
- `Fact_Trip`: Contains Foreign Keys (`Driver_SK`, `Rider_SK`, `Pickup_Location_SK`, `Dropoff_Location_SK`, `Date_SK`, `Time_SK`) and Metrics.

**Star Schema Diagram**:
```
┌────────────────────────────────────────────────────────────────────┐
│                                                                    │
│     [Dim_Driver]                              [Dim_Rider]          │
│           │                                        │               │
│           └──────────────┐    ┌───────────────────┘                │
│                          ▼    ▼                                    │
│     [Dim_Date]────►[   Fact_Trip   ]◄────[Dim_Time]                │
│                          ▲    ▲                                    │
│           ┌──────────────┘    └───────────────────┐                │
│           │                                        │               │
│   [Dim_Pickup_Loc]                        [Dim_Dropoff_Loc]        │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```
**Reading the diagram**: This is a classic Star Schema where:
- **Center**: `Fact_Trip` is the central fact table containing trip metrics (fare, distance, duration)
- **6 Dimensions** radiate outward like a star: Driver, Rider, Date, Time, Pickup Location, Dropoff Location
- **Role-Playing Dimension**: `Dim_Location` is used twice (Pickup & Dropoff) - same structure, different context
- **All dimensions connect directly to Fact** - no intermediate tables (unlike Snowflake)

---


## Section 5 — Data Pipelines & Big Data Concepts

Data pipelines are the backbone of any data platform. They move data from sources to destinations, transforming it along the way. Understanding pipeline architecture, orchestration, and failure handling is critical for data engineers.

---

### Pipeline Architecture: Day in the Life of a Data Engineer

Let's walk through a realistic production pipeline to understand how all the pieces fit together.

**Scenario**: A retail company needs daily sales reporting.

**Step-by-Step Flow**:
1. **Ingestion (6:00 AM)**: A 100GB CSV file is uploaded to Amazon S3 by the vendor's SFTP job. An S3 Event Notification triggers an AWS Lambda function, which in turn triggers an Apache Airflow DAG via the Airflow REST API.

2. **Validation (6:05 AM)**: The first task in the DAG runs a **Great Expectations** suite:
   - Check: "Is `order_id` unique?" (No duplicates)
   - Check: "Is `order_date` within the last 7 days?" (Data freshness)
   - Check: "Are all `country_code` values in the allowed list?"
   - If any check fails → Send Slack alert, mark DAG as failed. **Do not proceed.**

3. **Processing (6:15 AM)**: A Spark cluster (Databricks or EMR) spins up:
   - Reads the raw CSV from S3.
   - Converts to Parquet format (10x smaller, 100x faster to query).
   - Joins with reference data (`Dim_Product`, `Dim_Store`) from Delta Lake.
   - Applies business logic (e.g., calculate discount percentages).
   - Writes clean data to the `Silver` layer in Delta Lake.

4. **Loading (6:45 AM)**: A Snowflake `COPY INTO` command loads the Parquet files from S3 into a staging table. A `MERGE` statement upserts into the production `Fact_Sales` table.

5. **Serving (7:00 AM)**: Tableau's scheduled extract refresh pulls the latest data from Snowflake. Dashboards are automatically updated before the business day starts.

---

### Apache Airflow Components (Deep Dive)

> **ELI5**: Airflow is like a super-powered to-do list for your data jobs. Instead of just saying "do X at 9 AM", it says "do A, then B if A worked, then C, and if anything breaks, text me."

**Core Components**:

| Component | Role | Analogy |
| :--- | :--- | :--- |
| **DAG (Directed Acyclic Graph)** | Defines the workflow structure: which tasks exist and their dependencies. | The recipe (steps 1, 2, 3...) |
| **Scheduler** | Continuously monitors all DAGs and triggers task instances when their dependencies are met and the schedule time has arrived. | The kitchen timer |
| **Executor** | Determines *how* and *where* tasks are run. | The kitchen staff |
| **Worker** | The actual machine/process that executes a task. | The individual chef |
| **Metadata Database** | PostgreSQL/MySQL database storing DAG definitions, task states, run history, connections. | The recipe book + kitchen log |
| **Webserver** | The UI for monitoring DAGs, viewing logs, triggering runs, managing connections. | The security camera in the kitchen |

**Executor Types**:
| Executor | How it Works | Use Case |
| :--- | :--- | :--- |
| **SequentialExecutor** | Runs one task at a time. Single process. | Local testing only. Never production. |
| **LocalExecutor** | Runs tasks in parallel on the Airflow host machine using multiprocessing. | Small production setups. |
| **CeleryExecutor** | Distributes tasks to a pool of Celery workers across multiple machines. Requires Redis/RabbitMQ. | Medium-to-large scale production. |
| **KubernetesExecutor** | Spins up a new Kubernetes Pod for each task. Fully isolated. | Cloud-native, auto-scaling workloads. |

**Key Operators (Task Templates)**:
| Operator | Purpose | Example |
| :--- | :--- | :--- |
| `BashOperator` | Runs a shell command. | `bash_command="python my_script.py"` |
| `PythonOperator` | Runs a Python function. | `python_callable=my_function` |
| `SparkSubmitOperator` | Submits a Spark job (PySpark/Scala). | `application="s3://bucket/my_spark_job.py"` |
| `S3KeySensor` | **Waits** until a file appears in S3. | Waits for vendor file before proceeding. |
| `EmailOperator` | Sends an email. | Alert on completion. |
| `SlackWebhookOperator` | Sends a Slack message. | Alert team on failure. |

---

### Comparison: File Formats (The Definitive Guide)

Choosing the right file format can make your pipelines 10-100x faster. This is one of the most impactful decisions in data engineering.

| Feature | CSV | JSON | Parquet | Avro | ORC |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Storage Type** | Row | Row | **Columnar** | Row | **Columnar** |
| **Human Readable?** | Yes | Yes | No (Binary) | No (Binary) | No (Binary) |
| **Schema Embedded?** | No (Inferred) | Partial | Yes (Footer) | Yes (Header) | Yes (Footer) |
| **Compression** | Poor | Poor | **Excellent** (Snappy, Gzip, Zstd) | Good | **Excellent** |
| **Splittable?** | Sometimes (if uncompressed) | No | **Yes** (Row Groups) | **Yes** (Blocks) | **Yes** (Stripes) |
| **Schema Evolution** | None | Weak | Moderate | **Strong** | Moderate |
| **Best Use Case** | Excel interchange, small data | APIs, configs | **OLAP Analytics (Read Heavy)** | **Streaming (Kafka)** | Legacy Hadoop/Hive |
| **Query Speed (Analytics)** | Slow | Very Slow | **Fast** | Slow | **Fast** |

**Why Columnar is Faster for Analytics (ELI5)**:
Imagine a spreadsheet with 100 columns and 1 million rows. You run `SELECT AVG(price) FROM sales`. 
- **Row-based (CSV)**: The engine reads ALL 100 columns for ALL 1 million rows, even though you only need 1 column. Wasteful.
- **Columnar (Parquet)**: The engine reads ONLY the `price` column (1 column, 1 million values). 99% less data read = 99% faster.

**Why Parquet is King for Data Lakes**:
1. **Compression**: Columnar data compresses extremely well (similar values are adjacent). A 10GB CSV might become a 1GB Parquet.
2. **Predicate Pushdown**: Parquet stores min/max stats per column per row group. If you filter `WHERE date = '2024-01-01'`, the engine can skip row groups where `max(date) < '2024-01-01'` without reading them.
3. **Splittability**: A single 10GB Parquet file can be read by 100 Spark tasks in parallel (each reads a "Row Group").

---

### Pipeline Error Handling (Production Patterns)

Robust pipelines don't just run—they fail gracefully, recover automatically, and alert humans when intervention is needed.

**Pattern 1: Retry with Exponential Backoff**
- **Problem**: Transient failures (network blip, temporary API rate limit).
- **Solution**: Retry the task, but wait longer between each attempt.
- **Implementation (Airflow)**:
  ```python
  from airflow.decorators import task
  from datetime import timedelta
  
  @task(retries=3, retry_delay=timedelta(minutes=5), retry_exponential_backoff=True, max_retry_delay=timedelta(hours=1))
  def call_flaky_api():
      # Attempt 1: Wait 5 mins. Attempt 2: Wait 10 mins. Attempt 3: Wait 20 mins (capped at 1hr).
      pass
  ```

**Pattern 2: Dead Letter Queue (DLQ)**
- **Problem**: Some records are "poison pills" (malformed, schema mismatch) that will always fail.
- **Solution**: Don't let one bad record stop the entire pipeline. Route bad records to a `_errors` table for manual review.
- **Implementation (Spark)**:
  ```python
  from pyspark.sql.functions import col
  
  df = spark.read.json("s3://bucket/raw/")
  
  good_records = df.filter(col("order_id").isNotNull())
  bad_records = df.filter(col("order_id").isNull())
  
  good_records.write.mode("append").saveAsTable("curated.orders")
  bad_records.write.mode("append").saveAsTable("errors.orders_dlq")
  ```

**Pattern 3: Idempotency**
- **Problem**: If a pipeline runs twice (due to manual re-run or Airflow hiccup), it shouldn't duplicate data.
- **Solution**: Design pipelines so running them N times produces the same result as running once.
- **Techniques**:
    - Use `MERGE` / `UPSERT` instead of `INSERT`.
    - Overwrite partitions (`df.write.mode("overwrite").partitionBy("date")`) instead of appending.
    - Add unique constraints / primary keys.

**Pattern 4: Circuit Breaker**
- **Problem**: A downstream system (e.g., an API you call) is having a major outage. Retrying endlessly wastes resources and delays other jobs.
- **Solution**: After N consecutive failures, "open the circuit" and stop trying. Alert humans. Try again later.

---

## Section 6 — PySpark & Spark SQL

Apache Spark is the de facto standard for large-scale data processing. Understanding its architecture is crucial for debugging, optimizing, and designing pipelines.

---

### Spark Architecture Components (ELI5 + Deep Dive)

> **ELI5**: Imagine you need to sort 1 million books in a massive library. You (the **Driver**) create a plan: "Team A sorts fiction, Team B sorts non-fiction." You give instructions to teams (**Executors**). They do the work, and you combine the results.

**Components**:

| Component | Role | Runs Where? | Key Point |
| :--- | :--- | :--- | :--- |
| **Driver** | The "brain." Parses your code, creates the execution plan (DAG), schedules tasks, collects results. | A single node (your laptop, a master node). | If the Driver crashes, the entire job fails. |
| **Cluster Manager** | Allocates resources (CPU, RAM) to the Spark application. | YARN, Kubernetes, Mesos, or Standalone. | Tells Executors how much memory they get. |
| **Executors** | The "workers." Run the actual data transformations (map, filter, join). Store cached data. | Worker nodes in the cluster. | If an Executor fails, Spark automatically re-runs its tasks elsewhere. |
| **Task** | The smallest unit of work. One task processes one partition of data. | Inside an Executor. | More tasks = more parallelism. |
| **Stage** | A group of tasks that can be done without shuffling data. | Logical grouping. | Stage boundaries are created by "wide" operations (like `groupBy`). |
| **Job** | All the work triggered by a single Action (e.g., `.count()`, `.collect()`, `.write()`). | Logical grouping. | One Action = One Job. |

**Visual Diagram**:
```
                      +-------------------+
                      |      DRIVER       |
                      | (SparkContext)    |
                      | - Parses Code     |
                      | - Creates DAG     |
                      | - Schedules Tasks |
                      +---------+---------+
                                |
        +-----------------------+-----------------------+
        |                       |                       |
+-------v-------+       +-------v-------+       +-------v-------+
|   EXECUTOR 1  |       |   EXECUTOR 2  |       |   EXECUTOR 3  |
| (Worker Node) |       | (Worker Node) |       | (Worker Node) |
| - Runs Tasks  |       | - Runs Tasks  |       | - Runs Tasks  |
| - Caches Data |       | - Caches Data |       | - Caches Data |
+---------------+       +---------------+       +---------------+
```

---

### RDD vs DataFrame vs Dataset

These are three generations of Spark's data abstraction. Understanding their differences helps you choose the right one (and answer interview questions).

| Feature | RDD (Resilient Distributed Dataset) | DataFrame | Dataset |
| :--- | :--- | :--- | :--- |
| **Level of Abstraction** | Low-Level (Close to JVM) | High-Level (Tabular) | High-Level (Tabular + Type-Safe) |
| **Schema Awareness** | No (Objects are opaque) | **Yes** (Column names, types) | **Yes** |
| **Optimization** | **None** (You write the logic, Spark runs it literally) | **Catalyst Optimizer** (Spark rewrites your logic for efficiency) | **Catalyst Optimizer** |
| **Language Support** | Scala, Java, Python, R | Scala, Java, Python, R | **Scala, Java only** |
| **Type Safety** | Compile-time (Scala/Java) | **Runtime only** (Errors at execution) | **Compile-time** (Errors at compile) |
| **Ease of Use** | Low (Functional programming: `map`, `filter`) | **High** (SQL-like API: `select`, `where`) | High |
| **When to Use** | Legacy code, very low-level control over partitioning | **Default for 99% of use cases** | When you need compile-time safety in Scala |

**ELI5**:
- **RDD**: You're given a bag of random objects. You can do anything with them, but you have to figure out how yourself.
- **DataFrame**: You're given a spreadsheet. Spark knows the column names and types, so it can help you query efficiently.
- **Dataset**: Like a DataFrame, but Spark also knows the *exact* Java/Scala class of each row, catching errors before you even run the job.

**Code Comparison (Scala)**:
```scala
// RDD: Low-level. No optimization.
rdd.filter(row => row(2).asInstanceOf[Int] > 100)

// DataFrame: High-level. Optimized.
df.filter($"age" > 100)

// Dataset: High-level. Type-safe. Optimized.
ds.filter(person => person.age > 100)
```

---

### Anatomy of a Spark Job

When you call an **Action** (like `.count()`), Spark triggers a **Job**. Understanding the hierarchy helps with debugging.

```
+----------------------+
|        JOB           |  <-- Triggered by ONE Action (e.g., df.count())
| +------------------+ |
| |      STAGE 1     | |  <-- Stage boundary at Shuffle
| | +------+ +------+| |
| | |Task 1| |Task 2|| |  <-- Tasks run in parallel
| | +------+ +------+| |      One Task = One Partition
| +------------------+ |
| +------------------+ |
| |      STAGE 2     | |  <-- After the Shuffle
| | +------+ +------+| |
| | |Task 1| |Task 2|| |
| | +------+ +------+| |
| +------------------+ |
+----------------------+
```

**Key Terms**:
- **Transformation (Lazy)**: Defines a computation but doesn't execute it. e.g., `df.filter(...)`, `df.groupBy(...)`. Spark just remembers the recipe.
- **Action (Eager)**: Triggers execution and returns a result. e.g., `.count()`, `.collect()`, `.write()`. Spark actually runs the job.
- **Narrow Transformation**: Each input partition contributes to only one output partition. e.g., `filter`, `map`. No shuffle needed. Fast.
- **Wide Transformation**: Each input partition can contribute to multiple output partitions. e.g., `groupBy`, `join`, `repartition`. **Requires Shuffle.** Slow.

---

### Optimization Techniques (Critical for Interviews)

These are the techniques interviewers expect you to know when asked "How would you optimize this Spark job?"

#### 1. Caching & Persistence

> **ELI5**: If you're going to read the same book three times, photocopy it once and keep it on your desk instead of walking to the library each time.

**When to Use**:
- When the same DataFrame is used multiple times in your code (e.g., for multiple aggregations, or for iterative ML algorithms).

**How it Works**:
- `df.cache()`: Stores the DataFrame in memory (RAM) across Executors.
- `df.persist(StorageLevel.MEMORY_AND_DISK)`: Stores in RAM, spills to disk if RAM is full.

**Code**:
```python
df = spark.read.parquet("s3://bucket/large_table/")

# Without caching: Reads from S3 TWICE (once per action).
count1 = df.filter(df.status == 'active').count()
count2 = df.filter(df.status == 'inactive').count()

# With caching: Reads from S3 ONCE, stores in RAM.
df.cache()
count1 = df.filter(df.status == 'active').count()  # Reads from RAM
count2 = df.filter(df.status == 'inactive').count() # Reads from RAM

# IMPORTANT: Unpersist when done to free memory!
df.unpersist()
```

**Storage Levels**:
| Level | Where | Serialized? | Replicated? |
| :--- | :--- | :--- | :--- |
| `MEMORY_ONLY` | RAM only | No | No |
| `MEMORY_AND_DISK` | RAM, spills to disk | No | No |
| `MEMORY_ONLY_SER` | RAM only | Yes (smaller, slower) | No |
| `DISK_ONLY` | Disk only | Yes | No |
| `MEMORY_ONLY_2` | RAM only | No | Yes (2 copies) |

---

#### 2. Broadcast Join

> **ELI5**: Instead of shipping 1 million packages to a warehouse to meet a small letter, just photocopy the letter and put one copy in every delivery truck.

**When to Use**:
- Joining a LARGE table (billions of rows) with a SMALL table (<100MB by default, configurable).

**How it Works**:
- Spark serializes the small table.
- Sends a copy of it to **every Executor** in the cluster.
- Each Executor joins its chunk of the large table with the local copy of the small table.
- **No Shuffle required!** (Normally, a join requires shuffling both tables.)

**Code**:
```python
from pyspark.sql.functions import broadcast

large_df = spark.read.parquet("s3://bucket/fact_sales/")  # 1B rows
small_df = spark.read.parquet("s3://bucket/dim_product/")  # 10k rows

# Spark will automatically broadcast small_df if it's small enough.
# But you can explicitly hint:
result = large_df.join(broadcast(small_df), "product_id")
```

**Tuning**: `spark.sql.autoBroadcastJoinThreshold` (default 10MB). Increase if your small table is larger but still fits in memory.

---

#### 3. Handling Data Skew (Salting)

> **ELI5**: If one checkout line at the grocery store has 1000 people and the others have 10, redistribute people by adding random lane assignments.

**What is Skew?**:
- When data for a join or aggregation is unevenly distributed across partitions.
- Example: You `groupBy("customer_id")`. One customer has 10 million orders, others have 10. The task processing that one customer takes 1000x longer.

**Symptoms**:
- Most tasks finish quickly, but 1-2 tasks run for hours.
- Spark UI shows uneven task durations within a stage.
- `OutOfMemoryError` on specific Executors.

**Solution: Salting (Step-by-Step)**:
1. **Add a Salt Column**: Add a random number (0-9) to the key in the large table.
2. **Explode the Small Table**: Replicate each row 10 times (once for each salt value).
3. **Join on Key + Salt**: Now the skewed key is distributed across 10 partitions.
4. **Aggregate Results**: Remove the salt and re-aggregate if necessary.

**Full Code Example**:
```python
from pyspark.sql.functions import rand, floor, explode, array, lit, col

# Configuration
NUM_SALT_BUCKETS = 10

# Large Table (Skewed)
df_large = spark.read.parquet("s3://bucket/transactions/") # Has skewed customer_id

# Small Table (Lookup)
df_small = spark.read.parquet("s3://bucket/customers/")

# Step 1: Add Salt to Large Table (Random 0-9)
df_large_salted = df_large.withColumn("salt", floor(rand() * NUM_SALT_BUCKETS).cast("int"))

# Step 2: Explode Small Table (Replicate rows 10 times)
salt_values = array([lit(i) for i in range(NUM_SALT_BUCKETS)])
df_small_exploded = df_small.withColumn("salt", explode(salt_values))

# Step 3: Join on Original Key + Salt
df_joined = df_large_salted.join(df_small_exploded, on=["customer_id", "salt"], how="inner")

# Step 4: Drop the Salt Column (No longer needed)
df_result = df_joined.drop("salt")
```

---

#### 4. Partition Pruning

> **ELI5**: If you're looking for January's mail, go directly to the "January" folder. Don't open February, March, April...

**What is Partition Pruning?**:
- When your data is stored **partitioned by a column** (e.g., `year`/`month`/`day`), and you filter by that column, Spark skips reading files in irrelevant partitions entirely.

**Example**:
```
s3://bucket/sales/
├── year=2022/
│   └── month=01/ ... many files
│   └── month=02/ ...
├── year=2023/
├── year=2024/
```

```python
# BAD: Reads ALL files, then filters in memory. Slow!
df = spark.read.parquet("s3://bucket/sales/")
df_2024 = df.filter(col("year") == 2024)

# GOOD: Spark reads ONLY files under year=2024/. 10-100x faster.
df = spark.read.parquet("s3://bucket/sales/")
df_2024 = df.filter(col("year") == 2024)

# Both look the same! The key is that the FILTER is on the PARTITION COLUMN.
# Spark Catalyst optimizer automatically pushes the predicate down to file listing.
```

**Check**: Look at the Spark UI (SQL Tab -> Details). You should see "PartitionFilters" in the FileScan operator.

---

### Spark Shuffle: Deep Dive

> **ELI5** (Recap): Shuffling is like asking everyone at a party to find all other people with the same birthday. Everyone has to talk to everyone else.

**Why is Shuffle Expensive?**:
1. **Disk I/O**: Shuffle data is written to disk (Shuffle Write) by map tasks.
2. **Network I/O**: Shuffle data is sent over the network to reduce tasks (Shuffle Read).
3. **Serialization**: Data must be serialized to bytes for transfer.
4. **Deserialization**: Data must be deserialized back to objects for processing.

**Operations that Cause Shuffle**:
- `groupBy()`, `reduceByKey()`
- `join()`, `cogroup()`
- `repartition()`, `coalesce()` (increasing partitions)
- `sortBy()`
- `distinct()`

**How to Reduce Shuffle**:
1. **Filter early**: Reduce data volume *before* the shuffle-causing operation.
2. **Broadcast Joins**: Avoid shuffle entirely for small table joins.
3. **Pre-partition data**: If you join on `user_id` often, store your Parquet files partitioned by `user_id`.
4. **Use `reduceByKey` instead of `groupByKey`**: (RDD API) `reduceByKey` does partial aggregation locally before shuffle.

---


## Section 7 — GCP Big Data Platform

### BigQuery Architecture
- **Concept**: Serverless Data Warehouse.
- **Separation of Compute & Storage**:
  - **Storage**: Colossus (Global file system). Cheap.
  - **Compute**: Dremel (Massively parallel query engine). Fast.
  - **Network**: Petabit network (Jupiter) connects them.
- **Why it matters**: You can scale storage to PBs without paying for extra compute, and vice versa.

### BigQuery Pricing Models
- **On-Demand**: $5 per TB scanned.
  - *Best for**: Ad-hoc, unpredictable workloads.
  - *Risk**: One bad query (`SELECT *`) can cost $1000s.
- **Capacity (Editions)**: Pay for "Slots" (Virtual CPUs). Autoscaling.
  - *Best for**: Predictable enterprise workloads (ETL + Dashboarding).

### Performance Optimization (GCP)
1. **Partitioning**: Splits table physically by Date/Timestamp/Int Range.
   - *Result**: Scanning `WHERE date = '2024-01-01'` reads only 1/365th of the data.
2. **Clustering**: Sorts data within partitions by high-cardinality columns (e.g., `user_id`).
   - *Result**: "Block Pruning" skips blocks that don't match the filter.
3. **Denormalization**: BigQuery loves `NESTED` and `REPEATED` fields (Arrays/Structs).
   - *Why*: Reduces Joins. Joins are expensive (Shuffle). Nested data is local.

---

## Section 8 — Databricks Platform

### Architecture
- **Control Plane**: Managed by Databricks (Cloud Account). Contains UI, Notebooks, Job Scheduler, Driver metadata.
- **Data Plane**: Your AWS/Azure VPC. Contains Clusters (VMs) and Data (S3/ADLS).
  - *Security*: Data never leaves your account (in Classic mode).

### Delta Lake
- **Definition**: An open-source storage layer that brings ACID transactions to Apache Spark and big data workloads.
- **Under the Hood**:
  - **Parquet Files**: Store actual data.
  - **_delta_log**: Folder containing JSON files (Transaction Log).
- **Features**:
  - **Time Travel**: `SELECT * FROM table VERSION AS OF 5`.
  - **Schema Enforcement**: Rejects writes that don't match schema.
  - **Merger (Upsert)**:
    ```python
    deltaTable.alias("target").merge(
        source = updates.alias("source"),
        condition = "target.id = source.id"
    ).whenMatchedUpdate(set = { "target.val": "source.val" }) \
     .whenNotMatchedInsertAll() \
     .execute()
    ```

### Optimization Techniques
- **OPTIMIZE**: Compacts small files (Small File Problem) into larger 1GB files.
- **Z-ORDER**: Co-locates related information in the same set of files (Multi-dimensional clustering).
- **Photon Engine**: C++ rewritten engine for faster SQL execution.

### Unity Catalog (Governance)
- **Problem**: Hive Metastore was workspace-local. Hard to share data across Dev/Prod workspaces.
- **Solution (Unity)**: Centralized Metadata Layer.
  - **3-Level Namespace**: `Catalog.Schema.Table`.
  - **Single Source of Truth**: Define Access Control (ACLs) once, apply everywhere.
  - **Data Lineage**: Auto-captures column-level lineage.

### Connectivity
- **Multi-Cloud**: Databricks runs on AWS, Azure, GCP with same API.
- **Connectivity**: Uses JDBC/ODBC to connect Tableau/Power BI to Databricks SQL Warehouse.


---

## Section 9 — Azure Data Engineering Stack

Azure provides a comprehensive suite of services for building enterprise-grade data platforms. Understanding how these services connect and when to use each is critical for Azure Data Engineers.

---

### Core Components Overview

| Service | Role | Analogy |
| :--- | :--- | :--- |
| **Azure Data Lake Storage Gen2 (ADLS)** | Scalable storage for data lakes (Parquet, CSV, JSON) | The warehouse where all raw materials are stored |
| **Azure Data Factory (ADF)** | Orchestration and data movement | The logistics company moving goods between warehouses |
| **Azure Databricks** | Data processing (Spark) | The factory that transforms raw materials into products |
| **Azure Synapse Analytics** | Unified analytics platform (Warehouse + Spark + Pipelines) | An all-in-one factory, warehouse, and logistics company |
| **Azure Key Vault** | Secrets management (passwords, keys) | The company safe |
| **Azure Purview / Microsoft Purview** | Data governance, cataloging, lineage | The inventory tracking and compliance department |

---

### Azure Data Lake Storage Gen2 (ADLS) Deep Dive

> **ELI5**: ADLS is like a giant cloud-based hard drive designed for storing massive amounts of files (terabytes to petabytes). It's optimized for analytics workloads.

**Key Features**:
- **Hierarchical Namespace (HNS)**: Unlike flat Blob storage, ADLS Gen2 has true folders. Operations like "rename folder" or "delete folder" are atomic and instant.
- **Storage Tiers**:
  | Tier | Use Case | Cost (Storage) | Cost (Access) |
  | :--- | :--- | :--- | :--- |
  | **Hot** | Frequently accessed data (last 30 days) | High | Low |
  | **Cool** | Infrequently accessed (30-90 days) | Lower | Higher |
  | **Archive** | Rarely accessed (compliance, years) | Lowest | Highest (hours to rehydrate) |
  
- **Security**:
    - **RBAC (Role-Based Access Control)**: Azure AD-based. "User X has 'Storage Blob Data Contributor' role on Container Y."
    - **ACLs (Access Control Lists)**: POSIX-style permissions on folders/files. Read/Write/Execute for Owner/Group/Others.

---

### Azure Data Factory (ADF) Deep Dive

> **ELI5**: ADF is like a robot that moves data from one place to another. You tell it "Pick up this file from S3, transform it, and put it in Snowflake." It handles the scheduling, retries, and monitoring.

#### Integration Runtimes (IR)

The "compute engine" that executes ADF activities.

| IR Type | Where it Runs | Use Case |
| :--- | :--- | :--- |
| **Azure IR (Auto-Resolve)** | Microsoft-managed cloud VMs | Connecting to public endpoints (S3, public SQL, APIs) |
| **Azure IR (Managed VNet)** | Microsoft-managed, inside a VNet | Connecting to Azure resources via Private Endpoints securely |
| **Self-Hosted IR** | Your own VM (on-prem or in Azure) | Connecting to on-premises data sources (SQL Server behind firewall) |

---

#### ADF Activities Deep Dive

| Activity | Purpose | Key Parameters | When to Use |
| :--- | :--- | :--- | :--- |
| **Copy Activity** | Moves data from Source to Sink | `Source`, `Sink`, `Translator` (column mapping),`parallelCopies` | Bulk data movement (S3 → ADLS, SQL → Parquet) |
| **Data Flow (Mapping)** | Visually designed Spark-based transformations | Transformations (Filter, Agg, Join, Pivot), Clusters | Complex transformations without writing Spark code |
| **Lookup** | Reads a small dataset (config table, control table) | `Source`, `firstRowOnly` | Get list of tables to copy, get max watermark |
| **ForEach** | Iterates over a list and runs inner activities | `items`, `isSequential`, `batchCount` | Copy 100 tables by iterating over a list from Lookup |
| **If Condition** | Branches logic based on expression result | `expression`, `ifTrueActivities`, `ifFalseActivities` | Skip loading if source file is empty |
| **Until** | Loops until a condition is met | `expression`, `timeout` | Poll an API until status = 'complete' |
| **Wait** | Pauses pipeline for a specified time | `waitTimeInSeconds` | Delay before retrying a failed API call |
| **Web Activity** | Makes HTTP requests (REST APIs) | `url`, `method`, `headers`, `body` | Trigger a Databricks job, call an external API |
| **Get Metadata** | Retrieves file/folder properties | `dataset`, `fieldList` (exists, size, lastModified) | Check if source file exists before copying |
| **Execute Pipeline** | Calls another pipeline | `pipeline`, `parameters`, `waitOnCompletion` | Modular design: Master pipeline calls child pipelines |
| **Set Variable / Append Variable** | Sets/appends values to pipeline variables | `variableName`, `value` | Build a dynamic list of files to process |

---

#### ADF Triggers Deep Dive

Triggers control *when* a pipeline runs.

| Trigger Type | How it Works | Use Case |
| :--- | :--- | :--- |
| **Schedule Trigger** | Runs at fixed times (like Cron). `@hourly`, `@daily`, or complex recurrence. | "Run every day at 6 AM." |
| **Tumbling Window Trigger** | Runs for fixed, non-overlapping time slices. Supports **dependency chaining** and **backfill**. | "Process data for Jan 1, then Jan 2, then Jan 3..." If Jan 2 fails, Jan 3 waits. |
| **Event-Based Trigger (Storage)** | Fires when a file is created, modified, or deleted in a Blob/ADLS container. | "Start pipeline as soon as the vendor drops the daily file." |
| **Custom Event Trigger (Event Grid)** | Fires based on custom events from Azure Event Grid. | Integrate with microservices, IoT, or other event-driven architectures. |

**Tumbling Window vs Schedule (Key Difference)**:
- **Schedule**: Fires at time T. Doesn't know or care about previous runs.
- **Tumbling Window**: Fires for time *slice* [T, T+1hr]. If the slice for T-1hr failed, it can wait or retry. Supports dependencies: "Slice 2 only runs after Slice 1 succeeds."

---

### Security Best Practices (Azure)

#### Azure Key Vault Deep Dive

> **ELI5**: Instead of writing your password on a sticky note on your monitor, you put it in a locked safe. The safe (Key Vault) gives you a key that only *your* application can use.

**What Key Vault Stores**:
- **Secrets**: Passwords, connection strings, API keys.
- **Keys**: Encryption keys (for encrypting data at rest).
- **Certificates**: SSL/TLS certificates.

**How ADF Uses Key Vault**:
1. Create a **Linked Service** to Key Vault in ADF.
2. In your SQL Linked Service, instead of hardcoding the password, reference the key vault secret:
   ```json
   "password": {
       "type": "AzureKeyVaultSecret",
       "store": { "referenceName": "my_keyvault_linkedservice" },
       "secretName": "sql-password"
   }
   ```
3. ADF fetches the password from Key Vault at runtime. The password is never stored in ADF.

---

#### Managed Identity (MSI) Deep Dive

> **ELI5**: Instead of giving your app a username/password to access a database, you give the *app itself* an identity (like a badge). The database recognizes the badge and lets the app in.

**Types**:
| Type | Created | Lifecycle | Use Case |
| :--- | :--- | :--- | :--- |
| **System-Assigned** | Automatically when you enable it on a resource | Tied to the resource. Deleted when resource is deleted. | ADF accessing ADLS. |
| **User-Assigned** | Created manually as a standalone resource | Independent. Can be assigned to multiple resources. | Multiple Databricks workspaces accessing the same Key Vault. |

**Best Practice**:
1. Enable **Managed Identity** on your ADF instance.
2. Go to your ADLS account → Access Control (IAM) → Add Role Assignment.
3. Assign the **Storage Blob Data Contributor** role to the ADF Managed Identity.
4. In ADF, create an ADLS Linked Service using "Managed Identity" authentication. **No passwords stored anywhere!**

---

### Azure Synapse Analytics Deep Dive

> **ELI5**: Synapse is like a "supermarket" where you can find a Data Warehouse, a Spark cluster, a Data Factory, and a Power BI workspace all under one roof.

**Key Components**:
| Component | What it Does | Underlying Tech |
| :--- | :--- | :--- |
| **Dedicated SQL Pool** | Provisioned data warehouse. Pay for reserved capacity. Best for predictable heavy workloads. | Based on MPP (Massively Parallel Processing) SQL |
| **Serverless SQL Pool** | Query data in place (ADLS) without loading. Pay per query. | Distributed SQL query engine |
| **Spark Pool** | Apache Spark clusters for data engineering and ML. | PySpark, Scala Spark, SparkR |
| **Synapse Pipelines** | Data orchestration (Copy, Dataflows). 95% identical to ADF. | Azure Data Factory codebase |
| **Synapse Link** | Real-time, no-ETL connection to Cosmos DB, Dataverse. | Change feed integration |

**Dedicated vs Serverless SQL Pool**:
| Feature | Dedicated SQL Pool | Serverless SQL Pool |
| :--- | :--- | :--- |
| **Data Storage** | Data is loaded into Synapse-managed storage | Data stays in ADLS (queried in-place) |
| **Pricing** | Per DWU (Data Warehouse Unit) provisioned | Per TB of data scanned |
| **Performance** | Predictable, fast for complex queries | Depends on data format (Parquet = fast, CSV = slow) |
| **Use Case** | Core enterprise warehouse | Ad-hoc exploration, data lakehouse |

---

### Data Lineage (Azure Purview / Microsoft Purview)

> **ELI5**: Lineage is like a family tree for your data. It shows you where a piece of data came from (its parents), what transformations it went through, and where it ended up (its children).

**Why Lineage Matters**:
1. **Impact Analysis**: "If I change this source column, which reports will break?"
2. **Root Cause Analysis**: "This dashboard is showing wrong numbers. Which transformation introduced the bug?"
3. **Compliance**: "Show the auditor exactly where personal data flows."

**How Purview Captures Lineage**:
- **Automatic Scanning**: Purview scans sources like ADF, Synapse, Databricks, Power BI.
- **Lineage Captured**: When ADF Copy Activity runs, Purview records: `Source Table (SQL)` → `Copy Activity` → `Sink File (ADLS)`.

**Viewing Lineage**:
In the Purview portal, you can search for a table (e.g., `Fact_Sales`) and see a visual graph showing all upstream sources and downstream consumers.

---

### End-to-End Azure Architecture Project (Medallion)

A common production architecture using the **Bronze / Silver / Gold (Medallion)** pattern.

**Layer Definitions**:
| Layer | Contents | Format | Purpose |
| :--- | :--- | :--- | :--- |
| **Bronze (Raw)** | Exact copy of source data | Original format (JSON, CSV, or converted Parquet) | Preserve source of truth. No transformations. |
| **Silver (Cleansed)** | Cleaned, deduplicated, conformed data | Delta Lake (Parquet + Transaction Log) | Apply business rules, fix data quality issues. |
| **Gold (Curated)** | Aggregated, business-ready data (Fact/Dim tables) | Delta Lake | Direct consumption by BI tools, ML models. |

**Step-by-Step Flow**:
1. **Ingest (ADF)**: Copy data from on-prem SQL Server → ADLS `bronze/sales/` (Raw Parquet).
2. **Cleanse (Databricks)**: Read `bronze/`, apply deduplication, handle nulls, conform data types. Write to `silver/sales/` as Delta Lake.
3. **Aggregate (Databricks)**: Read `silver/`, build Star Schema (`fact_sales`, `dim_customer`). Write to `gold/`.
4. **Serve (Synapse Serverless)**: Create external tables pointing to `gold/` Delta Lake files. Power BI connects to Synapse Serverless via DirectQuery.
5. **Govern (Purview)**: Scans all layers. Captures lineage: `SQL Server → Bronze → Silver → Gold → Power BI Report`.

```
+------------------+      +------------------+      +------------------+
|  On-Prem SQL     |----->|  ADLS Bronze     |----->|  ADLS Silver     |
|  (Source)        | ADF  |  (Raw)           | DBX  |  (Cleansed)      |
+------------------+      +------------------+      +------------------+
                                                             |
                                                             | Databricks
                                                             v
                           +------------------+      +------------------+
                           |  Power BI        |<-----|  ADLS Gold       |
                           |  (Consumption)   | SYN  |  (Curated)       |
                           +------------------+      +------------------+
                                    ^
                                    | Purview (Lineage & Catalog)
```

---


## Section 10 — BI Tools (Power BI + Tableau)

Power BI is Microsoft's flagship Business Intelligence tool. Understanding its architecture, DAX engine, security model, and integration with the Power Platform is essential for BI professionals.

---

### Power BI Architecture Deep Dive

> **ELI5**: Power BI is like a super-smart spreadsheet that can connect to almost any data source, let you build reports with drag-and-drop, and share them with thousands of people in your company.

**Key Components**:
| Component | What it Does | Where it Runs |
| :--- | :--- | :--- |
| **Power BI Desktop** | Authoring tool. Create data models, reports, visuals. | Your local machine (Windows app) |
| **Power BI Service** | Cloud platform for publishing, sharing, collaboration. | app.powerbi.com (SaaS) |
| **Power BI Report Server** | On-premises version of Power BI Service. | Your own servers (for regulated industries) |
| **Power BI Gateway** | Secure bridge between on-prem data sources and Power BI Service. | Your on-prem server or Azure VM |
| **Power BI Mobile** | View and interact with reports on iOS/Android. | Mobile devices |

**Gateway Types**:
| Type | Use Case | Scalability |
| :--- | :--- | :--- |
| **On-premises Data Gateway (Standard)** | Shared by multiple users and datasets. Org-wide. | Multi-node cluster support |
| **On-premises Data Gateway (Personal)** | For one user only. Testing/dev. Not for production. | Single machine |

---

### Connection Modes Deep Dive

Choosing the right connection mode is one of the most critical decisions in Power BI.

| Feature | Import Mode | DirectQuery Mode | Live Connection | Composite Model |
| :--- | :--- | :--- | :--- | :--- |
| **Data Location** | Loaded into Power BI's in-memory engine (VertiPaq) | Query sent to source DB at runtime | Connects to SSAS / Power BI Dataset | Mix of Import and DirectQuery |
| **Performance** | **Fastest** (RAM compressed data) | Slower (Network + DB query time) | Fast (reuses SSAS optimization) | Varies |
| **Freshness** | Stale until scheduled refresh | **Real-time** | **Real-time** | Varies by table |
| **DAX Support** | **Full** | Limited (some Time Intel fails) | **Full** | **Full** |
| **Model Size Limit (Pro)** | 1 GB | None (data stays in source) | None | 1 GB for Import portion |
| **When to Use** | Most common. Best performance. | Huge data (PB). Strict real-time need. | Re-using enterprise SSAS models. | Aggregation tables over DirectQuery detail. |

**Composite Models (Advanced)**:
- Combine Import tables (fast aggregations) with DirectQuery tables (detail drill-through).
- Example: `Agg_Sales_Monthly` is Import (small, fast). `Detail_Sales` is DirectQuery (huge, but only queried on drill-through).

---

### Power BI Data Modeling Best Practices

> **ELI5**: A good data model is like a well-organized library. Books are grouped by topic (tables), each book has a unique ID (primary key), and there are clear signs showing how sections connect (relationships).

**Best Practices**:
1. **Use Star Schema**: One central Fact table surrounded by Dimension tables.
2. **Avoid Bi-Directional Relationships**: They cause ambiguity and performance issues. Use only when absolutely necessary (e.g., M:M bridge tables).
3. **Hide Columns Not Needed in Reporting**: Cluttered models confuse report builders.
4. **Create a Date Table**: Mark it as a "Date Table" for Time Intelligence to work correctly.
5. **Avoid Calculated Columns for Large Tables**: They increase model size. Prefer Measures.

---

### DAX Deep Dive

DAX (Data Analysis Expressions) is the formula language for Power BI, SSAS, and Power Pivot.

#### Core Concepts

**1. Row Context vs Filter Context**:
| Context | What it Is | Created By |
| :--- | :--- | :--- |
| **Row Context** | "The current row I'm looking at." Used in Calculated Columns and inside iterators. | Calculated Column, `SUMX`, `AVERAGEX`, `FILTER` |
| **Filter Context** | "The filters currently active on the report." Comes from slicers, visual interactions, and `CALCULATE`. | Slicers, Visual filters, `CALCULATE` |

**2. Context Transition** (Advanced):
- When you use `CALCULATE()` inside a row context (e.g., inside `SUMX`), the row context is converted to filter context.
- This is powerful but can be confusing.

**ELI5**:
- **Row Context**: "I'm on page 5 of this book."
- **Filter Context**: "I'm only looking at books in the 'History' section."
- **Context Transition**: "Wait, let me take the book I'm holding and filter the whole library to only books by this author."

#### DAX Engine Internals (How it Actually Works)

> **Interview Q**: "Why is my DAX query slow?"

**Two Engines**:
1. **Storage Engine (SE)**: Multi-threaded. Scans the compressed VertiPaq data. Very fast for simple filters and aggregations.
2. **Formula Engine (FE)**: Single-threaded. Handles complex DAX logic (iterators, complex expressions, row-by-row calculations).

**Performance Rule**: Push as much work as possible to the Storage Engine. Avoid complex iterators in the Formula Engine.

| Fast (SE) | Slow (FE) |
| :--- | :--- |
| `SUM(Sales[Amount])` | `SUMX(Sales, Sales[Price] * Sales[Qty])` |
| `FILTER(Table, Column = "X")` | `FILTER(Table, [Measure] > 100)` (Measure evaluated row-by-row) |
| Simple `CALCULATE` | Nested `CALCULATE` with complex conditions |

**Optimization Tips**:
1. Use `FILTER(ALL(Table), ...)` sparingly. It materializes the entire table.
2. Pre-calculate complex logic in Power Query (M) instead of DAX.
3. Use variables (`VAR`) to store intermediate results and avoid recalculation.

#### Common DAX Patterns (Interview Favorites)

**Year-to-Date (YTD)**:
```dax
Sales YTD = TOTALYTD(SUM(Sales[Amount]), 'Date'[Date])
```

**Same Period Last Year**:
```dax
Sales LY = CALCULATE(SUM(Sales[Amount]), SAMEPERIODLASTYEAR('Date'[Date]))

YoY Growth % = DIVIDE([Sales] - [Sales LY], [Sales LY])
```

**Running Total**:
```dax
Running Total = 
CALCULATE(
    SUM(Sales[Amount]),
    FILTER(
        ALL('Date'[Date]),
        'Date'[Date] <= MAX('Date'[Date])
    )
)
```

---

### Security: RLS, CLS, OLS

Power BI offers multiple layers of security to control who sees what.

#### Row-Level Security (RLS)

> **ELI5**: RLS is like giving each user a different pair of glasses. When they look at the same report, they see different rows based on their identity.

**Static RLS**:
- Hardcoded filter in the role definition.
- Example: Role "USA Sales Team" has filter `[Region] = "USA"`.

**Dynamic RLS**:
- Filter based on the logged-in user's email.
- Requires a `Users` table in the model.

**Implementation Steps**:
1. Create a `Dim_Users` table: `| Email | Region |`
2. Create a relationship: `Dim_Users[Region]` → `Dim_Sales_Region[Region]` (Single direction, Dim to Fact).
3. Create a Role in Desktop: "Sales Role".
4. Add DAX filter on `Dim_Users`: `[Email] = USERPRINCIPALNAME()`.
5. When user `alice@company.com` logs in, Power BI filters `Dim_Users` to Alice's row, which propagates to Sales data.

---

#### Column-Level Security (CLS) & Object-Level Security (OLS)

> **ELI5**: CLS is like redacting parts of a document. Some users see the full report; others see certain columns blacked out.

**OLS (Object-Level Security)**:
- Hides entire **tables** or **columns** from specific roles.
- Users in the restricted role cannot see the table/column in the field list, and DAX queries referencing it fail.
- **Requirement**: Requires **Tabular Editor** (external tool) to define. Cannot be configured in Power BI Desktop UI directly.

**Use Case**: Hide the `Employee_Salary` column from the "Manager" role but show it to the "HR" role.

---

### Power Platform Integration

Power BI is part of the **Power Platform**: Power BI + Power Apps + Power Automate + Power Virtual Agents.

#### Power Apps Integration

> **ELI5**: Power Apps lets you build mini-applications (like forms) without coding. You can embed these apps *inside* a Power BI report.

**Use Cases**:
1. **Write-Back**: User sees low inventory in a report → Clicks a button → A Power App form pops up → User enters a new order quantity → Data writes back to a SQL table → Report refreshes.
2. **What-If Analysis**: User enters a parameter in a Power App embedded in the report → The parameter feeds into a Power BI measure.

**How to Embed**:
1. Create a Power App (Canvas App).
2. In Power BI, add the "Power Apps" visual from AppSource.
3. Select the app to embed.
4. Pass data context (e.g., the selected `Product_ID` from the report) to the app.

---

#### Power Automate Integration

> **ELI5**: Power Automate is like setting up a chain of dominoes. "When this happens, do that." You can trigger these automations from a Power BI report.

**Use Cases**:
1. **Data-Driven Alerts**: "When total sales exceed $1M, send me an email."
2. **Report Actions**: "When I click this button in the report, create a ticket in ServiceNow."

**How to Add**:
1. Add the "Power Automate" visual to your report.
2. Create a Flow that is triggered "When a Power BI button is clicked".
3. In the flow, add actions (Send email, Create record, Call API, etc.).
4. In the report, clicking the button triggers the flow, passing context like `Product_ID` or `Customer_Name`.

**Example Flow**:
- Trigger: "Power BI Button Clicked"
- Action 1: Get `Customer_Name` from the data context.
- Action 2: Create a record in CRM with `Customer_Name`.
- Action 3: Send an email confirmation to the user.

---

### Advanced Power Query (M Language)

Power Query is the ETL engine inside Power BI. It uses a functional language called M.

#### Query Folding

> **ELI5**: Instead of downloading 100GB of data and *then* filtering it, Query Folding tells the source database to filter it *first*, so you only download 1GB.

**How to Check**:
- Right-click on a step in Power Query.
- If "View Native Query" is clickable, folding is happening.
- If grayed out, folding broke at this step.

**Steps that Break Folding**:
- Adding a Custom Column with complex M logic.
- Using `Table.Buffer`.
- Referencing parameters that aren't pushed to the source.

**Why it Matters**:
- Essential for **Incremental Refresh** (only fetch new data).
- Massively improves refresh times.

---

### Report Performance Troubleshooting

**Scenario**: "My report is slow. How do I debug it?"

**Step 1: Identify the Bottleneck**:
| Symptom | Likely Cause |
| :--- | :--- |
| Initial load is slow, refresh is slow | Data model too large / Inefficient Power Query |
| Interacting with visuals is slow | Slow DAX measures or too many visuals |
| One specific visual is slow | That visual's DAX is complex or data is aggregated poorly |

**Step 2: Use Performance Analyzer**:
1. In Power BI Desktop, go to View → Performance Analyzer.
2. Start Recording.
3. Interact with the report (click slicers, change pages).
4. Analyze the results: "DAX query" time vs "Visual display" time.

**Step 3: Optimize**:
- Reduce the number of visuals per page (each generates DAX queries).
- Simplify complex DAX measures.
- Pre-aggregate data in Power Query or the source.
- Use Aggregation tables for large datasets.

---


## Section 11 — Microsoft Fabric

Microsoft Fabric is Microsoft's newest unified analytics platform, combining data engineering, data science, real-time analytics, and business intelligence into a single SaaS offering.

---

### What is Microsoft Fabric?

> **ELI5**: Imagine you had to build a house, and you had to buy bricks from one store, cement from another, hire plumbers from a third, and electricians from a fourth. Now imagine someone builds a "housing factory" where everything is already assembled. You just walk in, customize, and your house is ready. That's Fabric compared to Azure's individual services.

**Definition**: Microsoft Fabric is a unified, SaaS-based analytics platform that brings together Power BI, Azure Data Factory, Azure Synapse Analytics, and new capabilities like Real-Time Analytics and Data Science, all built on a shared data lake called **OneLake**.

**Key Differentiator**: **OneLake** - A single, unified data lake for the entire organization, automatically used by all Fabric workloads without manual configuration.

---

### Fabric vs Azure Synapse vs Azure Data Factory

| Feature | Azure Data Factory | Azure Synapse Analytics | Microsoft Fabric |
| :--- | :--- | :--- | :--- |
| **Deployment Model** | PaaS (Provision resources yourself) | PaaS (Provision Pools, Pipelines) | **SaaS (Fully managed)** |
| **Data Lake** | You create ADLS, configure access | You create ADLS, link to Synapse | **OneLake (Built-in, auto-configured)** |
| **Networking** | Private Endpoints, VNets | Private Endpoints, Managed VNet | Limited VNet support (improving) |
| **Pricing** | Per activity run, IR hours | Per DWU, Pool hours | **Capacity Units (CU)** - Single pool for all workloads |
| **Governance** | Separate Purview integration | Separate Purview integration | **Built-in Governance** (Lineage, Cataloging) |
| **Target User** | Platform engineers | Data engineers, BI devs | **All analytics users** (Citizen to Pro) |

**When to Choose Fabric**:
- You want a unified, low-friction experience.
- Your organization is primarily Microsoft-centric (Power BI, M365).
- You don't have complex network isolation requirements (yet).

**When to Stick with Synapse/ADF**:
- You need Private Endpoints and strict VNet integration.
- You have heavy investments in existing PaaS infrastructure.

---

### OneLake (The Heart of Fabric)

> **ELI5**: OneLake is like OneDrive, but for your company's data. Just like OneDrive syncs your documents wherever you go, OneLake makes your data accessible to Power BI, Spark, Pipelines, and SQL—all without copying it.

**Key Concepts**:
| Concept | Definition |
| :--- | :--- |
| **OneLake** | A single, organizational-wide data lake (Delta Parquet format, stored on Azure). |
| **Lakehouse** | A workspace item that combines the best of Data Lake (cheap storage, all file types) and Data Warehouse (SQL queries, ACID). |
| **Warehouse** | A traditional SQL data warehouse experience within Fabric (T-SQL endpoint). |
| **Shortcuts** | Virtual pointers to external data (S3, ADLS, Dataverse) that appear *as if* they are in OneLake. **No data is copied.** |

**Shortcuts (Game Changer)**:
- **Use Case**: Your ML team has data in S3. Your BI team needs it in Power BI. Instead of copying S3 → ADLS → Power BI, you create a Shortcut. Power BI reads directly from S3 via OneLake.
- **Supported Sources**: ADLS Gen2, Amazon S3, Google Cloud Storage, Dataverse.

---

### Fabric Workloads

Fabric provides multiple "experiences" (workloads) tailored to different personas.

| Workload | What it Does | Persona |
| :--- | :--- | :--- |
| **Data Factory** | Data pipelines (Copy, Dataflows Gen2). Same UI as ADF. | Data Engineer |
| **Data Engineering** | Spark notebooks, Spark job definitions, Lakehouses. | Data Engineer |
| **Data Warehouse** | T-SQL based warehouse. Create tables, views, stored procedures. | Data Analyst / Warehouse Dev |
| **Data Science** | Jupyter notebooks, MLflow integration, model training. | Data Scientist |
| **Real-Time Analytics** | Ingest and query streaming data (based on Azure Data Explorer/Kusto). | Streaming Engineer |
| **Power BI** | Reports, Dashboards, Semantic Models (formerly Datasets). Deeply integrated. | BI Developer / Analyst |

---

### Lakehouse vs Warehouse in Fabric

| Feature | Lakehouse | Warehouse |
| :--- | :--- | :--- |
| **Data Format** | Open formats (Delta Parquet) | Proprietary managed storage |
| **Query Language** | Spark SQL, T-SQL (read-only via SQL Endpoint) | T-SQL (Full DML) |
| **Best For** | Data Engineering (ingestion, transformation, ML) | Reporting (Semantic layer, complex SQL, stored procs) |
| **Schema** | Schema-on-Read or Schema-on-Write (your choice) | Schema-on-Write (strict) |
| **Data Access** | Direct file access (Parquet) + SQL Endpoint | SQL Endpoint only |

**Pattern**: Use **Lakehouse** for Bronze/Silver layers (raw ingestion, Spark transformations). Use **Warehouse** for Gold layer (curated, SQL-based views for reporting).

---

### Direct Lake Mode (Power BI Innovation)

> **ELI5**: Normally, Power BI either copies data into its memory (Import) or asks the database every time (DirectQuery). Direct Lake is a new mode: Power BI reads directly from OneLake's Parquet files, but with Import-like speed. Best of both worlds.

**How it Works**:
1. Your Lakehouse stores data as Delta Parquet in OneLake.
2. Power BI creates a Semantic Model in "Direct Lake" mode.
3. When users interact with the report, Power BI reads compressed columns directly from OneLake.
4. No VertiPaq cache needed (less memory), no DirectQuery latency (Parquet is local).

**Comparison**:
| Mode | Data Size Limit | Latency | Freshness |
| :--- | :--- | :--- | :--- |
| **Import** | 1GB (Pro) / 400GB (Premium) | Fastest | Stale until refresh |
| **DirectQuery** | Unlimited | Slowest | Real-time |
| **Direct Lake** | Limited by OneLake table size (10M+ rows OK) | Fast | Automatic (reads latest Parquet) |

---

### Fabric Capacity and Licensing

**Capacity Units (CU)**:
- Fabric uses a unified capacity model.
- All workloads (Spark, Pipelines, Warehouse, Power BI) draw from the same CU pool.
- Example: Running a Spark job consumes CUs. Running a Power BI refresh consumes CUs.

**SKUs**:
| SKU | CUs | Typical Use |
| :--- | :--- | :--- |
| **F2** | 2 | Trial, small PoC |
| **F64** | 64 | Medium production workloads |
| **F128** | 128 | Large enterprise |
| **F1024** | 1024 | Massive scale |

---

## Section 12 — Snowflake Cloud Platform

Snowflake is a cloud-native data warehouse known for its unique architecture, ease of use, and ability to run on any major cloud (AWS, Azure, GCP) with a consistent experience.

---

### What is Snowflake?

> **ELI5**: Snowflake is like a self-driving car for data warehousing. You don't have to tune the engine, change tires, or worry about fuel efficiency. You just tell it where to go (run a query), and it figures out how to get there optimally.

**Key Selling Points**:
1. **True Multi-Cloud**: Same experience on AWS, Azure, GCP. Data sharing across clouds.
2. **Separation of Storage and Compute**: Store petabytes cheaply. Spin up compute only when needed.
3. **Zero Management**: No indexes, no partitions, no vacuuming. Snowflake handles it all.
4. **Data Sharing**: Share live data with other Snowflake accounts securely, without copying.

---

### Snowflake Architecture (Deep Dive)

Snowflake's architecture is unique and consists of three independently scalable layers.

```
┌────────────────────────────────────────────────────────────────────┐
│                       CLOUD SERVICES LAYER                         │
│  (Authentication, Metadata, Query Optimizer, Infrastructure Mgmt)  │
└────────────────────────────────────────────────────────────────────┘
                                    │
        ┌───────────────────────────┴───────────────────────────┐
        ▼                                                       ▼
┌──────────────────────────────────┐  ┌──────────────────────────────────┐
│       VIRTUAL WAREHOUSE 1        │  │       VIRTUAL WAREHOUSE 2        │
│   (Loading_WH - XS, 1 node)      │  │  (Reporting_WH - XL, 8 nodes)    │
└──────────────────────────────────┘  └──────────────────────────────────┘
        │                                                       │
        └───────────────────────────┬───────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────┐
│                      CENTRALIZED STORAGE LAYER                     │
│   (S3 / Azure Blob / GCS - Micro-partitions, Columnar, Compressed) │
└────────────────────────────────────────────────────────────────────┘
```

**Layer 1: Cloud Services (Brain)**:
- **Query Optimizer**: Analyzes your SQL, generates execution plan.
- **Metadata Management**: Tracks micro-partition statistics.
- **Authentication / Security**: RBAC, MFA, Network Policies.
- **Cost Implication**: Always running, but uses minimal credits.

**Layer 2: Virtual Warehouses (Muscle)**:
- **What**: Compute clusters (1-128+ nodes).
- **Scaling**: T-shirt sizes (XS, S, M, L, XL, 2XL, 3XL, 4XL). Each size doubles the nodes.
- **Key Property**: **Complete Isolation**. `Loading_WH` and `Reporting_WH` don't compete for resources.
- **Auto-Suspend/Auto-Resume**: Warehouse can automatically stop after N minutes of inactivity and restart on query.
- **Multi-Cluster Warehouses**: For highly concurrent workloads, a single logical warehouse can spin up multiple clusters.

**Layer 3: Centralized Storage (Vault)**:
- **Format**: Data is stored as **micro-partitions** (50-500MB compressed Columnar).
- **Immutability**: Data is never updated in place. Inserts/Updates create new micro-partitions.
- **Pruning**: The optimizer uses min/max stats per micro-partition to skip irrelevant partitions.

---

### Key Snowflake Features (Interview Critical)

#### 1. Time Travel
- **Definition**: Query data as it existed at a point in the past.
- **Retention**: Standard: 1 day. Enterprise: Up to 90 days.
- **Use Cases**: Undo accidental deletes. Audit historical state.

```sql
-- Query data from 1 hour ago
SELECT * FROM sales AT(OFFSET => -3600);

-- Query data as of a specific timestamp
SELECT * FROM sales AT(TIMESTAMP => '2024-01-15 10:00:00'::timestamp);

-- Restore a dropped table
UNDROP TABLE sales;
```

#### 2. Zero-Copy Cloning
- **Definition**: Create an instant copy of a database, schema, or table without duplicating data.
- **Mechanism**: Clone points to the same underlying micro-partitions. Only new/changed data creates new partitions.
- **Use Cases**: Create Dev/Test environments from Prod in seconds. Sandbox for testing schema changes.

```sql
CREATE DATABASE dev_sales CLONE prod_sales;
-- dev_sales is now a full copy, but uses 0 extra storage initially.
```

#### 3. Data Sharing (Secure Data Sharing)
- **Definition**: Share live, read-only data with other Snowflake accounts without copying data.
- **How it Works**: Provider creates a "Share" object. Consumer mounts it as a database.
- **Use Cases**: Vendors sharing product catalogs with customers. Data marketplaces.

```sql
-- Provider Account
CREATE SHARE sales_share;
GRANT USAGE ON DATABASE my_db TO SHARE sales_share;
GRANT SELECT ON TABLE my_db.public.sales TO SHARE sales_share;
ALTER SHARE sales_share ADD ACCOUNTS = 'consumer_account_id';

-- Consumer Account
CREATE DATABASE sales_from_vendor FROM SHARE provider_account.sales_share;
SELECT * FROM sales_from_vendor.public.sales;
```

#### 4. Snowpipe (Continuous Ingestion)
- **Definition**: Serverless, event-driven data loading.
- **Trigger**: S3 Event Notification → SQS → Snowpipe.
- **Cost**: Pay only for compute time used to load files (per-second).
- **Latency**: Near real-time (typically <1 minute from file landing).

```sql
CREATE PIPE my_pipe AS
COPY INTO my_table
FROM @my_s3_stage
FILE_FORMAT = (TYPE = 'PARQUET');
```

#### 5. Streams & Tasks (Change Data Capture + Scheduling)
- **Streams**: Track changes (INSERT, UPDATE, DELETE) on a table. Like a CDC log.
- **Tasks**: Scheduled SQL execution. Like a simple cron job inside Snowflake.
- **Pattern**: Use Streams to capture incremental changes, Tasks to process them periodically.

```sql
-- Create a Stream to track changes on source_table
CREATE STREAM my_stream ON TABLE source_table;

-- Create a Task to merge changes into target_table every 10 minutes
CREATE TASK my_task
  WAREHOUSE = my_wh
  SCHEDULE = '10 MINUTE'
AS
  MERGE INTO target_table t
  USING my_stream s ON t.id = s.id
  WHEN MATCHED AND s.metadata$action = 'DELETE' THEN DELETE
  WHEN MATCHED THEN UPDATE SET t.value = s.value
  WHEN NOT MATCHED THEN INSERT (id, value) VALUES (s.id, s.value);

ALTER TASK my_task RESUME;
```

#### 6. Clustering

- **Default Behavior**: Snowflake naturally clusters data by insertion order.
- **Problem**: If you query by a different column frequently, queries are slow.
- **Solution**: Define a **Clustering Key** to tell Snowflake how to re-organize data.

```sql
ALTER TABLE sales CLUSTER BY (sale_date, region);
-- Snowflake will automatically re-cluster data in the background.
```

---

### Snowflake Pricing Model

| Billing Component | What it Measures | How to Optimize |
| :--- | :--- | :--- |
| **Storage** | Size of data (micro-partitions) + Time Travel + Fail-safe | Use transient tables for staging (no Fail-safe). Reduce Time Travel retention. |
| **Compute (Credits)** | Warehouse runtime (per second, 60s minimum) | Use Auto-Suspend. Right-size warehouses. |
| **Cloud Services** | Metadata operations (usually free, billed if > 10% of compute) | Avoid excessive DDL/DML on small tables. |
| **Data Transfer** | Egress to other regions/clouds | Keep data and compute in the same region. |

---

## Section 13 — AWS Analytics Stack

AWS offers a comprehensive suite of analytics services. Understanding which service to use for which task is critical for building scalable, cost-effective data platforms on AWS.

---

### AWS Analytics Services Overview

> **ELI5**: AWS is like a massive hardware store. Need a hammer (Athena)? Aisle 5. Need a full construction crew (EMR)? Aisle 10. You pick only the tools you need and pay per use.

| Service | Purpose | Analogy |
| :--- | :--- | :--- |
| **Amazon S3** | Object storage (Data Lake) | The giant warehouse where you store everything |
| **AWS Glue** | ETL (Spark) + Data Catalog | The inventory system + factory robots |
| **Amazon Athena** | Serverless SQL queries on S3 | Ask questions about inventory without moving it |
| **Amazon Redshift** | Cloud Data Warehouse | The executive reporting room |
| **Amazon Kinesis** | Real-time streaming | The conveyor belt for live data |
| **Amazon EMR** | Managed Hadoop/Spark clusters | The heavy machinery for big jobs |
| **AWS Lake Formation** | Governance & Security for Data Lakes | The security guards and access control |
| **Amazon QuickSight** | BI Dashboards | The presentation slides for the CEO |

---

### Amazon S3 (The Foundation)

Everything in AWS analytics starts and ends with S3.

**Storage Classes**:
| Class | Use Case | Retrieval Time | Cost |
| :--- | :--- | :--- | :--- |
| **S3 Standard** | Frequently accessed data (hot) | Milliseconds | Highest |
| **S3 Intelligent-Tiering** | Unknown access patterns. AWS auto-tiers. | Milliseconds | Variable |
| **S3 Standard-IA** | Infrequently accessed (30+ days) | Milliseconds | Lower storage, higher retrieval |
| **S3 Glacier Instant Retrieval** | Archive with immediate access | Milliseconds | Lower storage |
| **S3 Glacier Flexible Retrieval** | Long-term archive | Minutes to hours | Lower |
| **S3 Glacier Deep Archive** | Compliance archives (7+ years) | Up to 12 hours | Lowest |

**Best Practice**: Use **Lifecycle Policies** to automatically move data between tiers.

```json
{
  "Rules": [
    {
      "ID": "MoveToIAAfter30Days",
      "Status": "Enabled",
      "Transitions": [
        { "Days": 30, "StorageClass": "STANDARD_IA" },
        { "Days": 365, "StorageClass": "GLACIER" }
      ]
    }
  ]
}
```

---

### AWS Glue (Deep Dive)

AWS Glue is a serverless ETL service that also provides a centralized metadata catalog.

#### Glue Crawlers
> **ELI5**: A Crawler is like a librarian that walks through your warehouse (S3), looks at the boxes (files), figures out what's inside (schema), and writes it all down in a catalog.

**How it Works**:
1. You configure a Crawler to scan an S3 path (e.g., `s3://my-bucket/sales/`).
2. The Crawler samples files, infers the schema (columns, data types).
3. It creates/updates tables in the **Glue Data Catalog**.
4. Athena, Redshift Spectrum, and EMR can now query these tables by name.

#### Glue Jobs (ETL)
- **Spark-based**: Write PySpark or Scala.
- **Serverless**: No cluster management. Specify DPUs (Data Processing Units).
- **Job Bookmarks**: Track which files have been processed. On re-run, skip them.

**Code Example (PySpark in Glue)**:
```python
from awsglue.context import GlueContext
from pyspark.context import SparkContext

sc = SparkContext()
glueContext = GlueContext(sc)
spark = glueContext.spark_session

# Read from Catalog
df = glueContext.create_dynamic_frame.from_catalog(
    database="sales_db",
    table_name="raw_sales"
)

# Transform
df_filtered = df.filter(df['amount'] > 0)

# Write to S3 as Parquet
glueContext.write_dynamic_frame.from_options(
    frame=df_filtered,
    connection_type="s3",
    connection_options={"path": "s3://my-bucket/processed/sales/"},
    format="parquet"
)
```

#### Glue Data Catalog
- **Centralized Metadata Store**: Tables, databases, schemas, partitions.
- **Hive Compatible**: Works with any tool expecting a Hive Metastore (Spark, Presto, Athena).

---

### Amazon Athena (Deep Dive)

> **ELI5**: Athena lets you run SQL queries directly on files sitting in S3. No loading, no database to manage. Just point, query, pay.

**How it Works**:
1. Athena uses the Glue Data Catalog to know table schemas.
2. When you run a query, Athena's distributed Presto/Trino engine scans S3 files.
3. You pay **$5 per TB scanned**.

**Optimization Tips**:
| Tip | Why | Impact |
| :--- | :--- | :--- |
| **Use Parquet/ORC** | Columnar, compressed. Only scan needed columns. | 10-100x cost reduction |
| **Partition your data** | `s3://bucket/data/year=2024/month=01/`. Query adds `WHERE year=2024`. | Skip scanning irrelevant partitions |
| **Use LIMIT** | Scans stop early if query is `SELECT * ... LIMIT 10` | Reduce cost for exploration |
| **Compress files** | Gzip, Snappy, Zstd. Less data = less cost. | 50-80% cost reduction |

**Example**:
```sql
-- Query partitioned Parquet data
SELECT customer_id, SUM(amount) as total_sales
FROM sales_db.processed_sales
WHERE year = '2024' AND month = '01'
GROUP BY customer_id;
```

---

### Amazon Redshift (Deep Dive)

> **ELI5**: Redshift is a traditional data warehouse, but in the cloud. If S3 is the warehouse of raw materials and Athena is for quick checks, Redshift is the assembly line where you build finished products (reports).

**Architecture**:
| Component | Role |
| :--- | :--- |
| **Leader Node** | Parses queries, creates execution plan, coordinates Compute Nodes |
| **Compute Nodes** | Store data (slices), execute queries in parallel |
| **Node Slices** | Partitions of a node. Data is distributed across slices. |

**Redshift Serverless vs Provisioned**:
| Feature | Provisioned | Serverless |
| :--- | :--- | :--- |
| **Cluster Management** | You choose node type/count | AWS manages capacity |
| **Pricing** | Per hour (always on) | Per RPU (Redshift Processing Unit) - pay per query |
| **Scaling** | Manual resize or Elastic Resize | Auto-scales based on demand |
| **Use Case** | Predictable, steady workloads | Spiky, variable workloads |

**Redshift Spectrum**:
- Query data *directly in S3* from within Redshift.
- Combines S3 data with Redshift data in a single query.
- Enables the **Lakehouse** pattern on AWS.

```sql
-- Create an external schema pointing to Glue Catalog
CREATE EXTERNAL SCHEMA s3_data
FROM DATA CATALOG
DATABASE 'sales_db'
IAM_ROLE 'arn:aws:iam::123456789012:role/MySpectrumRole';

-- Join Redshift table with S3 data
SELECT r.customer_name, s.total_amount
FROM local_customers r
JOIN s3_data.processed_sales s ON r.customer_id = s.customer_id;
```

---

### Amazon Kinesis (Real-Time Streaming)

Kinesis is AWS's suite for real-time data streaming and processing.

| Service | Purpose | Use Case |
| :--- | :--- | :--- |
| **Kinesis Data Streams** | Low-latency streaming ingestion. You manage shards. | Real-time clickstream, IoT telemetry |
| **Kinesis Data Firehose** | Near real-time delivery to S3, Redshift, OpenSearch. Fully managed. | Log aggregation, easy ETL landing |
| **Kinesis Data Analytics** | SQL/Flink on streaming data. | Real-time anomaly detection |

**Pattern: Log Aggregation**:
1. Application servers send logs to **Kinesis Firehose**.
2. Firehose buffers (1 min or 5MB) and writes Parquet to S3.
3. Glue Crawler updates the Catalog.
4. Athena queries the logs.

---

### End-to-End AWS Architecture (Production Example)

**Scenario**: E-commerce platform needs analytics on clickstream and sales data.

**Architecture**:
```
                                   +-------------------+
                                   |    QuickSight     |
                                   |   (Dashboards)    |
                                   +--------^----------+
                                            | (JDBC)
                                   +--------+----------+
                                   |      Athena       |  <-- Ad-hoc SQL
                                   +--------^----------+
                                            | (Catalog)
+----------------+        +-----------------+------------------+
| App Servers    |------->|             S3 Data Lake           |
| (Clickstream)  | Fhose  |  /raw/clicks/  |  /processed/      |
+----------------+        +-----------------+-----^------------+
                                                  |
                          +-----------------------+----------------+
                          |                 AWS Glue               |
                          |  (Crawlers -> Catalog | ETL Jobs -> S3)|
                          +------------------------^---------------+
                                                   |
+----------------+        +------------------------+---------------+
| Transactional  |------->|             Kinesis Firehose           |
| DB (RDS/Dynamo)| DMS    |              or Glue ETL               |
+----------------+        +----------------------------------------+
```

**Flow**:
1. **Clickstream**: App servers → Kinesis Firehose → S3 `/raw/clicks/` (Parquet).
2. **Transactional**: RDS/DynamoDB → AWS DMS → S3 `/raw/transactions/`.
3. **Catalog**: Glue Crawlers scan `/raw/`, create tables.
4. **Transform**: Glue ETL Jobs clean data → write to `/processed/` (Parquet, partitioned).
5. **Serve**: Athena for ad-hoc queries. QuickSight for dashboards.
6. **Optional**: Redshift for complex joins and aggregations on Gold data.

---

### AWS Lake Formation (Governance)

> **ELI5**: Lake Formation is the security guard for your data lake. It controls who can see which tables, rows, and columns, and keeps a log of everything.

**Key Features**:
| Feature | What it Does |
| :--- | :--- |
| **Fine-Grained Access Control** | Grant permissions at table, column, row, and cell level |
| **Tag-Based Access Control** | Assign tags to data (e.g., `PII=true`). Grant access based on tags. |
| **Centralized Permissions** | One place to manage access for Athena, Glue, Redshift Spectrum, EMR. |
| **Auditing** | Logs who accessed what data when. |

---
