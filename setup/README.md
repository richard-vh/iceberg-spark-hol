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
9. Run the following commands invidually at the command prompt
```
sudo -i
wget https://repo.anaconda.com/archive/Anaconda3-2024.02-1-Linux-x86_64.sh
bash Anaconda3-2024.02-1-Linux-x86_64.sh -b -p /opt/anaconda3
/opt/anaconda3/bin/conda init
/opt/anaconda3/bin/conda config --set auto_activate_base false
source .bashrc
conda install -c conda-forge jupyterhub
conda develop /opt/cloudera/parcels/CDH/lib/spark3/python/lib/py4j-*-src.zip
conda develop /opt/cloudera/parcels/CDH/lib/spark3/python
chmod -R 755 /opt/anaconda3/
mkdir /etc/jupyterhub/
/opt/anaconda3/bin/jupyterhub --generate-config -f /etc/jupyterhub/jupyterhub_config.py
```

10. Edit the JupyterHub config file and add the lines below

```
vi /etc/jupyterhub/jupyterhub_config.py
```
Add these line to the config file, replacing the <gateway_node_fqdn> with your Gateway Node FQDN and the <cdp_group_name> with the Group Name you created in step 4 of this section:
```
c.JupyterHub.bind_url = 'http://<gateway_node_fqdn>:9443'
c.ConfigurableHTTPProxy.command = '/opt/anaconda3/bin/configurable-http-proxy'
c.JupyterHub.ssl_cert = '/var/lib/cloudera-scm-agent/agent-cert/cm-auto-host_cert_chain.pem'
c.JupyterHub.ssl_key = '/var/lib/cloudera-scm-agent/agent-cert/cm-auto-host_key.pem'
c.Authenticator.allowed_groups = {"<cdp_group_name>"}
```

10. Get the SSL Key passphrase
```
cat /var/lib/cloudera-scm-agent/agent-cert/cm-auto-host_key.pw
```
11. Create a systemd unit file.
```
vi /etc/systemd/system/jupyterhub.service
```
Paste the text below, replacing the CONFIGPROXY_SSL_KEY_PASSPHRASE with the phassphrase obtained in the step above.

```
[Unit]
Description=Jupyterhub
[Service]
User=root
Environment="PATH=/opt/anaconda3/bin:/opt/anaconda3/condabin:/usr/share/Modules/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin"
Environment="CONFIGPROXY_SSL_KEY_PASSPHRASE=<cm-auto-host_key>"
ExecStart=/opt/anaconda3/bin/jupyterhub -f /etc/jupyterhub/jupyterhub_config.py
[Install]
WantedBy=multi-user.target
```

12. Run the following commands invidually at the command prompt
```
systemctl daemon-reload
systemctl enable jupyterhub
systemctl start jupyterhub
```
You can check the logs:
```
journalctl -u jupyterhub -f
```
13. Open a browser at the URL and test that you can login with your CDP workload username and password.
```
http://<gateway_node_fqdn>:9443
```


