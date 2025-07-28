# Cloudera Iceberg Spark Hands On Lab

![alt text](/img/new-ref-arch.png)

## About the Apache Iceberg on Cloudera Data Platform Hands On Lab

This hands-on lab provides a comprehensive exploration of Apache Iceberg's capabilities within the Cloudera Data Platform. The agenda is structured into two main sections.

The first section focuses on core Iceberg functionalities using Spark within Cloudera Data Engineering on Data Hubs. Participants will learn how to create, populate, and manage Iceberg tables, including performing data manipulation (inserts, updates, deletes). The lab will delve into the technical details of Iceberg's metadata, different table types (Copy-on-Write, Merge-on-Read), and powerful features such as schema and partition evolution. Attendees will also get practical experience with advanced capabilities like time travel for querying historical data, rollbacks using snapshots, branching for isolated development, and strategies for migrating traditional Hive tables to the Iceberg format. Finally, essential table maintenance operations like compaction and snapshot expiration will be covered.

The second section demonstrates Iceberg's role as a unified table format across the entire data lifecycle and the Cloudera product stack. Participants will interact with the same Iceberg tables using various Cloudera services. They will use Hive in Cloudera Data Warehouse (CDW) to query data and explore features like time travel and maintenance. In CDE, they will build and schedule PySpark jobs to write data into Iceberg. Subsequently, they will use Impala in CDW to run high-performance queries, analyze execution plans to see the benefits of partition evolution, and explore table metadata. Finally, the lab will extend into Cloudera AI, where attendees will use interactive PySpark sessions to further demonstrate Iceberg's ACID compliance and data management capabilities.

## Agenda & Times

Section 1: Spark on Cloudera Data Engineering Data Hubs
1. Creating Iceberg Tables
    * Creating an Iceberg Table 
    * Validate the HDFS Location
    * Background
    * Understanding the Metadata Files
2. Iceberg Data Manipulation
    * Iceberg Data Insertion and Updates
    * Iceberg Data Deletion
3. Types of Iceberg Tables (COW, MOR and MOW)
    * Iceberg Copy-on-Write (COW) Table
    * Iceberg Merge-on-Read (MOR) Table
    * Iceberg Merge-on-Write (MOW) Table
4. Schema and Partition Evolution
    * Iceberg Schema Evolution
    * Iceberg Partition Evolution
5. Iceberg Time Travel & Rollbacks using Snapshots
    * Understanding Time Travel in Iceberg
6. Iceberg Branching and Merging
    * Creating Branches in Iceberg 
    * Merging Iceberg Branches
7. Iceberg Tagging
    * Iceberg Tagging
8. Migration from Hive to Iceberg
    * “CONVERT” In-Place Migration Vanilla Parquet to Iceberg
    * “Create Table As” (CTAS) Migration from Vanilla Parquet to Iceberg
9. Iceberg Table Maintenance
    * Iceberg Compaction
    * Iceberg Expiring Snapshots
      
Section 2: Demonstrating Iceberg Capabilities across the Data Lifecycle and Cloudera Product Stack
1. Using Iceberg with Cloudera Data Flow
    * blah
3. Using Iceberg with Apache Hive on Cloudera Data Warehouse
    * Iceberg table migration features
    * Iceberg partitioned tables
    * Load historic data
    * Query Iceberg tables
    * Explore partition and schema evolution
    * Explore Iceberg table maintenance features - rollbacks and snapshot expiry
    * Explore Iceberg Time travel capabilities in Hive
4. Using Iceberg in Cloudera Data Engineering
    * Create a PySpark job to insert data into Iceberg
    * Schedule and run a job
5. Using Iceberg with Apache Impala on Cloudera Data Warehouse
    * Query Iceberg tables (CDE job)
    * Run explain plans on Iceberg queries to demonstrate partition evolution benefits
    * Explore Iceberg table snapshot metadata
    * Explore Iceberg Time travel capabilities in Impala
    * Explore Iceberg compatibility with other table types in queries
6. Using Iceberg in Cloudera AI
    * Creating sessions and execute PySpark
    * Create and query Iceberg tables
    * Load data into Iceberg


## Step by Step Instructions

Detailed instructions are provided in the [step_by_step_guides](https://github.com/richard-vh/iceberg-spark-hol/tree/main/step_by_step_guides/english).

* [Link to the English Guide](https://github.com/richard-vh/iceberg-spark-hol/tree/main/step_by_step_guides/english)

## Setup Instructions

The HOL requires data and dependencies to be created before the event. The attached [Setup Guide](https://github.com/richard-vh/iceberg-spark-hol/blob/main/setup/README.md) provides instructions for completing these requirements.

