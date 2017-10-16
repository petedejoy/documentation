---
title: Amazon Redshift
sidebar: platform_sidebar
---
# Getting started with Amazon Redshift. 
Redshift is Amazon Web Services' custom take on a traditional Postgres database. As they put it, "[A fully managed petabyte-scale data warehouse service in the cloud.](http://docs.aws.amazon.com/redshift/latest/mgmt/welcome.html)" It's cost-effective at nearly any level, capable of scaling from gigabytes to petabytes without a loss in performance, and uses [columnar storage](http://docs.aws.amazon.com/redshift/latest/dg/c_columnar_storage_disk_mem_mgmnt.html) (among other optimizations) for incredibly fast querying speeds.

This guide will explain how to integrate Redshift into Astronomer's clickstream platform as a destination, allowing you to leverage Amazon's technology to access, store, and query your customer data.

Our connector periodically runs an ETL (Exract - Transform - Load) process that pulls raw event data in S3, processes and transforms those raw events into a structured format, and then inserts structured event data from our bucket into your Redshift cluster. 

---

## Step 1: Pick a cluster that fits your needs. 

*Note: If you already have a Redshift cluster, go ahead to step 3*
 
 Once you've logged into your AWS account and Redshift console, it's time to pick and select your cluster. 
 
 As you do this, remember that the capacity you'll need and utilize depends primarily on the number of unique tables and columns created in the cluster, not the number of events (database records).
 Each unique `.track(_)` event creates a new table, and each property sent creates a new column in that table. For this reason, think about creating a detailed tracking plan to make sure that all events being passed to Astronomer are necessary and consistent.

 There are two kinds of Redshift clusters, Dense Compute and Dense Storage. 

 
 #### Dense Compute Cluster
Dense Compute clusters maximize query speed and performance, but in turn have less capacity for storage. While there is no set process to size a cluster, most customers with less than 20 million monthly events start with a single DC1 cluster and add nodes as needed. A single node cluster includes 200GB of storage and a maximum side of 2.56TB. 

#### Dense Storage Cluster
Dense storage clusters maximize storage capacity and allow customers with hundreds of millions of events to save money on Redshift hosting costs by using disk-based storage, slower CPU's, and less RAM. A single DS2 node cluster includes 2TB of space, with a max size of 16TB.

---

## Step 2. Provision your cluster.

1. Open the Redshift Console 
2. Click on "Launch Cluster"
3. Input cluster details 
4. Choose cluster size
5. Set up your cluster Security Group or VPC and proceed to review

If you're having trouble, check out the configuration steps [here](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-launch-sample-cluster.html).

---

## Step 3. Permission Astronomer to Redshift.

Once you provision your Redshift cluster, you'll need to configure your Redshift cluster to allow Astronomer to access it. 

### Confirm and Insert Credentials

The <i>Username</i> and <i>Password</i> you used to initially create the cluster are the credentials you'll put into your Astronomer account. You should NOT use your master AWS credentials here. If you want to switch clusters in the future, make sure you update your Username and Password as needed.

For Clickstream, having *distinct users* will allow you to (i) isolate queries from one another and (ii) perform audits more easily. 

To create a new user, you'll need to log into the Redshift database directly. Here's the SQL command:

```
-- create a user named "segment" that Segment will use when connecting to your Redshift cluster.
CREATE USER segment PASSWORD "<enter password here>";

-- allows the "segment" user to create new schemas on the specified database. (this is the name you chose when provisioning your cluster)
GRANT CREATE ON DATABASE "<enter database name here>" TO "segment";
```

### Configure Security Groups
Redshift clusters can either be in a EC2 Classic subnet or VPC subnet

If your cluster has a field called `Cluster Security Groups`, go ahead to EC2-Classic.

If your cluster has a field called `VPC Security Groups`, go ahead to EC2 VPC. 

**EC2-Classic**

1. Navigate to your Redshift Cluster settings
```
Redshift Dashboard > Clusters > Select Your Cluster
```

2. Click on the Cluster Security Groups

3. Open the Cluster Security Group

4. Click on "Add Connection Type"

5. Authorize Astronomer to write into your Redshift Port by inputting our IP Address: 52.86.240.182

**EC2-VPC**

1. Navigate to your Redshift Cluster settings
```
Redshift Dashboard > Clusters > Select Your Cluster
```

2. Click on the VPC Security Groups

3. Select the "Inbound" tab and then "Edit"

4. Authorize Astronomer to write into your Redshift Port by inputting our IP Address: 52.86.240.182

5. Navigate back to your Redshift Cluster Settings

6. Select the "Cluster" button and then "Modify"

7. Make sure the "Publicly Accessible" option is set to "Yes"



### Whitelist Astronomer's IP. 
Make sure that you whitelist 52.86.240.182 as an incoming IP Address so we can write to your Redshift instance without you exposing the database to everyone. For more information on, please explore our [Networking Guide](/1.0/guides/network/)

---

## Step 3: Identify Your Host, Port, and Database Name

The Host and Port are found at the top beside the label 'Endpoint,' with Host coming before the ':' and Port coming afterwards. The Database Name is found at the bottom besides a title of the same name.

---

## Step 4: Activate Integration on Astronomer

After you've identified the <b>Username, Password, Host, Port,</b> and <b>Database Name</b>, put all of these credentials into your Astronomer account and give your new connection a unique name. Note that your *Database* and *Schema* are kept separate from your other connection credentials. *Schema* is required but it is up to personal preference on what value to input as it can be thought as a folder to store your clickstream in. Example values include "analytics_ios", "clickstream_web", etc.

Click 'Create Destination' and your pipeline will be activated.

That's it! You'll now be receiving a livestream of data from your app into your private Redshift account.

---

## Things to note. 

### Reserved Words

Redshift limits the number of [reserved words](http://docs.aws.amazon.com/redshift/latest/dg/r_pg_keywords.html) in schema, table, and column names. We'd also encourage you to stay away from naming traits or properties that conflict with top level Clickstream fields (i.e. userID, receivedAt, messageID) 

### Query Speeds
The speed of your queries depends on the capabilities of your hardware, the size of the dataset, and the amount of data utilization in the cluster. For instance, you might see lower query speeds if you find yourself above 75% data utilization.

