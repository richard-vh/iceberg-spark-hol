# Cloudera Iceberg Spark Hands On Lab Setup Guide

## Create Data Engineering Data Hub

1. In your enviornment create a Data Hub.
2. Give you Data Hub a name.
3. Choose the **Data Engineering Spark3 for AWS** templete
4. We're going to install and run JupyterLab on the Gateway node for use in the HOL. This is nicer than having to SSH to the noode and running on the command line (up to you if you want to do this. If you don't and prefere using the command line then you can skip this step.
   
   Under the Data Hub **Hardware and Storage** tab go to Gateway Nodes and set **Instance Count** to **1** and **Volume Size (GB)** to **300**. 

![alt text](/img/gatewaynode.png)

5. Click **Provision Cluster** button.

## Install JupyterLab on Data Engineering Data Hub Gateway Node

**If you decided to not use JupyterLab in step 4 above then you don't need to do this!**

1. Make sure you have sudo access to the Data Hub.
2. Next we need to create a group in CDP to control access to JupyterLab once it has been installed.
3. In your CDP tenant go to User Management and create a new Group.
4. Give you group a name and ensure Sync Membership is disabled.
5. Create the group.
6. Add members to the group. This will be the userxx1 to userxxx for your HOL participants.

![alt text](/img/jupyterlabgroup.png)
   
8. SSH onto the Data Hub Gateway node.
9. 
