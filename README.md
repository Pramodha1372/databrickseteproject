# databrickseteproject

# Project Title: End-to-End Data Pipeline using Azure Databricks & Medallion Architecture

1. Objective

To design and implement a scalable ETL pipeline in Azure Databricks using Medallion Architecture (Bronze, Silver, Gold) for processing multiple Parquet files stored in Azure Blob Storage, leveraging advanced features like Delta Lake, Auto Loader, Unity Catalog, and Delta Live Tables.

2. Data Sources

Azure Blob Storage (Connected via Access Connector)
  Files Processed:
  1. regions.parquet
  2. orders.parquet
  3. products.parquet
  4. customers.parquet

3. Architecture

Framework: Medallion Architecture
Bronze Layer: Raw data ingestion from source
Silver Layer: Data cleaning, transformation, schema enforcement
Gold Layer: Business-ready tables for analytics and reporting

Architecture Diagram:

4. Implementation Steps

A. Bronze Layer
Regions: Ingested data using batch ingestion into DBFS.
Orders, Products, Customers: Used Auto Loader for incremental loading.
  Implemented Databricks Widgets for parameterized notebooks.
  Utilized checkpointing and RocksDB for state management to avoid duplicates.

B. Silver Layer: Converted Parquet → Delta and created managed tables in Unity Catalog.
Regions: Standard ingestion to Silver schema.
Orders: Implemented OOP concepts (classes, reusable functions) for modular code.
Products: Built SQL UDFs for transformations.
Customers: Applied PySpark operations (filtering, aggregations).

C. Gold Layer
Customers: Implemented SCD Type 1 transformations and stored in Gold schema.
Products: Implemented SCD Type 2 using Delta Live Tables (DLT) and applyChanges() method.
Orders:Designed Star Schema by connecting surrogate keys of customers & products with orders. Created Fact Table capturing dimension keys and metrics.

5. Orchestration

Created a Databricks Workflow connecting:
parameters_task → bronze_layer_task → Silver Layer Tasks → Gold Layer Tasks → Final Orders.
Enabled trigger-based execution for automation.
Verified and queried tables via SQL Editor in Databricks.

6. Tools & Technologies
  Azure Blob Storage (data source)
  Azure Databricks (compute engine)
  Delta Lake (data format)
  Unity Catalog (governance & schema)
  Delta Live Tables (DLT) (streaming and SCD handling)
  Auto Loader (incremental ingestion)

7. Key Features & Highlights

✔ Dynamic ingestion using Auto Loader
✔ Parameterization via Databricks Widgets
✔ OOP-based modular transformations
✔ SCD Type 1 & 2 implementation
✔ Orchestration via Databricks Workflows
✔ End-to-end Medallion Architecture compliance

8. Challenges Faced
  Handling schema evolution in Auto Loader
  Optimizing checkpoint locations for incremental loading
  Implementing SCD Type 2 efficiently

9. Benefits
  Scalable & reusable architecture
  Handles real-time incremental data loads
  Ensures data consistency with Delta Lake ACID transactions

Fully governed with Unity Catalog
