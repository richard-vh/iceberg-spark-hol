# Cloudera Iceberg Spark Hands On Lab Setup Guide

## Create Data Engineering Data Hub

1. In your enviornment create a Data Hub.
2. Give you Data Hub a name.
3. Choose the **Data Engineering Spark3 for AWS** templete
4. We're going to install and run JupyterLab on the Gateway node for use in the HOL. This is nicer than having to SSH to the noode and running on the command line (up to you if you want to do this. If you don't and prefere using the command line then you can skip this step.
   
   Under the Data Hub **Hardware and Storage** tab go to Gateway Nodes and set **Instance Count** to **1** and **Volume Size (GB)** to **300**. 

![alt text](/img/gatewaynode.png)

5. Click **Provision Cluster** button.
