# Cloudera Iceberg Spark Hands On Lab

![alt text](/img/new-ref-arch.png)

## About this Hands On Lab

This hands-on lab provides a comprehensive exploration of Apache Iceberg's capabilities within the Cloudera Data Platform. The agenda is structured into two main sections.

The first section focuses on core Iceberg functionalities using Spark within Cloudera Data Engineering on Data Hubs. Participants will learn how to create, populate, and manage Iceberg tables, including performing data manipulation (inserts, updates, deletes). The lab will delve into the technical details of Iceberg's metadata, different table types (Copy-on-Write, Merge-on-Read), and powerful features such as schema and partition evolution. Attendees will also get practical experience with advanced capabilities like time travel for querying historical data, rollbacks using snapshots, branching for isolated development, and strategies for migrating traditional Hive tables to the Iceberg format. Finally, essential table maintenance operations like compaction and snapshot expiration will be covered.

The second section demonstrates Iceberg's role as a unified table format across the entire data lifecycle and the Cloudera product stack. Participants will interact with the same Iceberg tables using various Cloudera services. They will use Hive in Cloudera Data Warehouse (CDW) to query data and explore features like time travel and maintenance. In CDE, they will build and schedule PySpark jobs to write data into Iceberg. Subsequently, they will use Impala in CDW to run high-performance queries, analyze execution plans to see the benefits of partition evolution, and explore table metadata. Finally, the lab will extend into Cloudera AI, where attendees will use interactive PySpark sessions to further demonstrate Iceberg's ACID compliance and data management capabilities.

## Agenda

### Section 1: Spark on Cloudera Data Engineering Data Hubs
* Before Starting the Labs
* Lab 1. Creating Iceberg Tables
  * Creating an Iceberg Table
  * Explore the Table Storage Location
  * Understanding the Metadata Files
* Lab 2. Iceberg data Manipulation
  * Best Practices for Managing Data
  * Iceberg Data Inserts and Updates
  * Iceberg Data Deletion
* Lab 3: Iceberg Tables Types (COW and MOR)
  * Iceberg Copy-on-Write (COW) Table
  * Iceberg Merge-on-Read (MOR) Table
* Lab 4: Schema and Partition Evolution
  * Iceberg Schema Evolution
  * Iceberg Partition Evolution
* Lab 5: Iceberg Time Travel & Rollbacks using Snapshots
  * Understanding Time Travel in Iceberg
  * Rollback Tables Using Snapshots
* Lab 6: Iceberg Tagging, Branching and Merging
  * Iceberg Tagging
  * Creating Branches in Iceberg
  * Merging Iceberg Branches
* Lab 7: Migrating tables from Hive to Iceberg
  * “CONVERT” In-Place Migration Vanilla Parquet to Iceberg
  * “Create Table As” (CATS) Migration from Vanilla Parquet to Iceberg
* Lab 8: Iceberg Table Maintenance
  * Iceberg Compaction
  * Iceberg Expiring Snapshots
  * Code Example: Compaction and Expiring Snapshots
      
### Section 2: Demonstrating Iceberg Capabilities across the Data Lifecycle and Cloudera Product Stack
* Before Starting the Labs
* Lab 1. Streaming Data Ingestion to Iceberg using Cloudera Data Flow
  * [verview of the Cloudera Data Flow Service
  * Deploy a Custom Data Flow Template
* Lab 2. Machine Learning with Iceberg tables using Cloudera AI
  * Creating and Setting up your Cloudera AI Project
  * Running Interactive Spark Session and Training and Tuning Models
  * Using JupyterLab to review the model output
  * Reviewing Model Run Experiments
  * Scheduling a Job in Cloudera AI
  * Delete CAI Project and Clean up resources
* Lab 3. Data Visualization using Iceberg tables in Cloudera Data Warehouse

## Step by Step Instructions

Detailed instructions are provided in the step_by_step_guides below. The hand-on labs are divided into trwo sections:

* [Section 1: Spark and Iceberg on Cloudera Data Engineering Data Hubs](#section-1-spark-and-iceberg-on-cloudera-data-engineering-data-hubs)
* [Section 2: Demonstrating Iceberg Capabilities across the Data Lifecycle and Cloudera Product Stack](#section-2-demonstrating-iceberg-capabilities-across-the-data-lifecycle-and-cloudera-product-stack)

## Setup Instructions

The HOL requires data and dependencies to be created before the event. The attached [Setup Guide](https://github.com/richard-vh/iceberg-spark-hol/blob/main/setup/README.md) provides instructions for completing these requirements.

