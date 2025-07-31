# Section 1: Spark on Cloudera Data Engineering Data Hubs

Working with Spark on Cloudera Data Engineering Data Hubs

Cloudera Data Hub is a cloud service for creating and managing secure, isolated, and elastic workload clusters on AWS, Azure, and GCP. It uses Cloudera Runtime and is managed from the Cloudera Management Console.

The service provides pre-configured templates for common workloads but also allows for extensive customization through reusable resources like cluster definitions, templates, and scripts. This enables agile, on-demand cluster creation and automation via a web interface or CLI, with all clusters linked to a central Data Lake for security and governance.

Typically we would SSH onto the node and execute Spark commands via the command line, but for the purposes of this lab we will use JupyterLab notebooks installed on the Data Hub cluster Gateway node for a better lab experience.

Click on the following link to open JupyterLab on the Gateway node and log on using your workload user name and password provided by the facilitator i.e user001/hsgdguquuqyququ:

```
https://intelos-spark-hol-gateway2.se-sandb.a465-9q4k.cloudera.site:9443/
```

1. In JupyterLb create a new notebook by selecting **File -> New -> Notebook**.
2. Click the **Select** button to acceopt the default kernel **Python3 (ipykernel)**.

![alt text](../img/jupyter1.png)

3. In the first cell of the new notebook paste the code below, substituting you assigned username in the username variable e.g. user003. This is going to create a Spark application on the Data Hub cluster.

```
# Enter your assigned user below
username = "<userxxx>"

from pyspark.sql import SparkSession

spark = SparkSession.builder \
                    .appName("{}_spark_session".format(username)) \
                    .getOrCreate()
```

4. Execute the cell code by clicking the **⏵** button or you can select cmd+enter on your keyboard to do the same.

![alt text](../img/jupyter2.png)

5. Lets check that our Spark session is running in the Data Hub Resource Manager. Navigate to the **CDP Control Plane -> Management Console -> Environments -> Select your environment**.
   
7. Under your enviornment select your Data Engineering Data Hub.

![alt text](../img/datahubselect.png)

7. Under your Data Hub select the **Resource Manager**

![alt text](../img/resourcemanager.png)

8. Go to the **Applications** tab and verify that the Spark session you created for your specific user in Jupyter is running e.g. **user001-spark-session**

![alt text](../img/application.png)

If all is good then we're ready to get on with Iceberg on Spark in our Jupyter Notebook!!!

## Lab 1. Creating Iceberg Tables 

### Creating an Iceberg Table

**What is an Iceberg Table?**
An Iceberg Table is a table where Iceberg manages both the metadata and the data. It’s a fully integrated table that Iceberg can track and manage for you. When you drop an Iceberg Table, Iceberg removes both the metadata and the data itself.

**Use an Iceberg Table when:**
You need Iceberg to fully handle both the data and metadata.
You want to manage the entire lifecycle of the table automatically.
You need atomic operations, such as schema evolution, partition evolution, and time travel.

**Key benefits and limitations**
**Benefits:**
Simplified data management.
Automatic metadata handling.
Built-in features like time travel and schema evolution.
**Limitations:**
Dropping the table deletes all data.

**Note:** By default, when you create an Iceberg table, it will be a Copy-on-Write (COW) table. This means that when you modify data, a new version of the data is written, and old data is not overwritten. You can explicitly specify the table type as Copy-on-Write (COW) or Merge-on-Write (MOR) using table properties.

1. For the remainder of this lab we'll do all of our Spark code in in your existing Jupyter notebook created above. Add a new cell to the notebook and run the code below.
```
spark.sql("DROP TABLE IF EXISTS default.{}_managed_countries".format(username))

# Create an Iceberg table for European countries (COW by default)
spark.sql("""
    CREATE TABLE default.{}_managed_countries (
        country_code STRING,
        country_name STRING,
        population INT,
        area DOUBLE
    )
    USING iceberg TBLPROPERTIES ('format-version' = '2')
""".format(username))

# Insert data into the table
spark.sql("""
    INSERT INTO default.{}_managed_countries VALUES
    ('FR', 'France', 67391582, 643801.0),
    ('DE', 'Germany', 83149300, 357022.0),
    ('IT', 'Italy', 60262770, 301340.0)
""".format(username))
```
![alt text](../img/jupyter2.png)

2.Add a new cell to the notebook and run each code block below to query the table.
```
# Query the table
df = spark.sql("SELECT * FROM default.{}_managed_countries".format(username))
df.show()
```
3.Add a new cell to the notebook and run each code block to look at the properties of the table.
```
# Describe the table
spark.sql("DESCRIBE default.{}_managed_countries".format(username)).show()

# Show the table's CREATE statement
spark.sql("SHOW CREATE TABLE default.{}_managed_countries".format(username)).show(truncate=False)

# Show the table properties
spark.sql("SHOW TBLPROPERTIES default.{}_managed_countries".format(username)).show(truncate=False)
```
Describing the tables shows us the column names, their data types and column comments.

The create table statement give us the the current table DDL, including the storage location (not the S3 storage path, Iceberg current snapshot id, storage file type, format-version which indicates if it's an Iceberg v1 or v2 table and the different write modes  Merge-On-Read (MOR - default) or Copy-On-Write (COW).

> [!NOTE] 
> Iceberg v2 builds upon v1 by adding row-level updates and deletes, enabled through merge-on-read and delete files. This allows for more efficient modification of data within immutable file formats like Parquet, Avro, and ORC, without rewriting entire files. Iceberg v1 primarily focused on supporting large analytic tables with immutable file formats and snapshot-based isolation. _

> [!NOTE] 
> There are pros and cons to choosing which Iceberg Merge-On-Read or Copy-On-Write write mode to use. This table can help you decide which strategies to use for your Iceberg table.

| **Feature** | **Copy-On-Write (COW)** | **Merge-On-Read (MOR)**
| --- | --- | --- | 
| Write Strategy | Rewrites entire affected files	| Creates separate delete/update files
| Read Performance	| Fast, as data is fully compacted	| Slower, as delete files must be applied
| Write Performance	| Slow, due to full file rewrites	| Faster, as only small delete/update files are written
| Storage Impact	| Higher, due to frequent file rewrites	| Lower, as full files are not rewritten
| Use Case Suitability	| Workloads with frequent reads and infrequent updates	| Workloads with frequent updates and fewer reads
| Update Mechanism	| Full file rewrite on update	| Newly updated rows written separately, old data marked as deleted
| Delete Mechanism	| Full file rewrite on delete	| Deletes tracked in separate delete files
| Compaction Requirement	| Not required frequently	| Required periodically to merge delete files
| Best For	| Read-heavy workloads, analytics, bulk updates	| Update-heavy workloads, streaming ingestion, incremental updates

### Validate the HDFS Location
### Background
### Understanding the Metadata Files

