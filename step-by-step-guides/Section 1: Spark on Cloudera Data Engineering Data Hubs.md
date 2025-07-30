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



### Validate the HDFS Location
### Background
### Understanding the Metadata Files

