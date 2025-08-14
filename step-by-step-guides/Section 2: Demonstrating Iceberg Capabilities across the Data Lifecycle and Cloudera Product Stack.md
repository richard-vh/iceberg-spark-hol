# Section 2: Demonstrating Iceberg Capabilities across the Data Lifecycle and Cloudera Product Stack

![alt text](../img/datalifecycle.png)

Cloudera Open Data Lakehouse powered by Apache Iceberg offers several key benefits that can significantly enhance your data management strategy. First, it provides better **performance and scalability** through innovative metadata management and flexible partitioning. It’s **fully open**, meaning there’s no vendor lock-in—thanks to its open-source foundation, it **supports a diverse ecosystem and community**. The platform also supports **multi-function analytics**, allowing different compute engines to access and process Iceberg tables concurrently and consistently. For those focused on data quality and consistency, it includes advanced capabilities like **ACID-compliant transactions, time travel, rollback, in-place partition evolution, and Iceberg replication**. Finally, Cloudera’s solution stands out with its ability to enable **multi-hybrid cloud deployments**, offering the freedom and portability to deploy wherever you need.

This Hands on lab takes you through the data lifecycle showcasing the ability to work with the same Iceberg tables across multiple engine and analytics types.

## Before Starting the Labs

Your workload user name and password has been provided by the facilitator e.g. user001/hsgdguquuqyququ. Keep it handy as you'll need it for certain configurations.

We're going to create some Iveberg tables to use across the labs in this section.

1. Sign in to the Cloudera Control Plane web interface.
2. On the **Data Warehouse** tile, click on the kebab menu (3 vertical dots) and select **Open Data Warehouse**.

![alt text](../img/icebergcdw1.png)

3. Under the **Virtual Warehouses** tab, locate the **workshop-impala-vw**h virtual warehouse and click on the **Hue** application icon.

![alt text](../img/icebergcdw2.png)

4. In the Hue application that opens in your browser you should see that the Impala engine is selected. Impala is a parallel processing SQL query engine that enables users to execute low latency SQL queries directly against large dataset. Copy and paste the code below into the editor pane. The code uses variables, so enter your user id in the username variable that is displayed at the bottom of the editor pane (e.g. user001).

![alt text](../img/icebergcdw3.png)

```ruby
DROP TABLE IF EXISTS default.${username}_laptop_data;
DROP TABLE IF EXISTS default.${username}_laptop_data_high;
DROP TABLE IF EXISTS default.${username}_laptop_data_scored;

CREATE TABLE default.${username}_laptop_data (
  laptop_id STRING,
  latitude STRING,
  longitude STRING,
  temperature STRING,
  event_ts STRING
) STORED AS iceberg;

CREATE TABLE default.${username}_laptop_data_high (
  laptop_id STRING,
  latitude STRING,
  longitude STRING,
  temperature STRING,
  event_ts STRING
) STORED AS iceberg;

CREATE TABLE default.${username}_laptop_data_scored (
    laptop_id   INT,
    latitude    DOUBLE,
    longitude   DOUBLE,
    temperature DOUBLE,
    event_ts    STRING,
    anomaly     INT
)  STORED AS parquet;

SELECT * FROM default.${username}_laptop_data;
SELECT * FROM default.${username}_laptop_data_high;
SELECT * FROM default.${username}_laptop_data_scored;
```

5. Use your cursor to select and highlight each SQL statement and execute each one by clicking the execute button :arrow_forward:.
   
   After executing all of the SQL statements you should have created 3 Tables: 2 Iceberg and 1 Parquet and ensured that they are not pre-populated.

![alt text](../img/icebergcdw4.png)


   
