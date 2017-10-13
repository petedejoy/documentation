---
title: Amazon Redshift
sidebar: platform_sidebar
---
# Getting started with Amazon Redshift. 
Redshift is Amazon Web Services' custom take on a traditional Postgres database. As they put it, "[A fully managed petabyte-scale data warehouse service in the cloud.](http://docs.aws.amazon.com/redshift/latest/mgmt/welcome.html)" It's cost-effective at nearly any level, capable of scaling from gigabytes to petabytes without a loss in performance, and uses [columnar storage](http://docs.aws.amazon.com/redshift/latest/dg/c_columnar_storage_disk_mem_mgmnt.html) (among other optimizations) for incredibly fast querying speeds.

This guide will explain how to integrate Redshift into Astronomer's clickstream platform as a destination, allowing you to leverage Amazon's technology to access, store, and query your customer data.

Our connector periodically runs an ETL (Exract - Transform - Load) process that pulls raw event data in S3, processes and transforms those raw events into a structured format, and then inserts structured event data from our bucket into your Redshift cluster. 

---

## Step 1: Pick a cluster that fits your needs and provision it. 
 
 Once you've logged into your AWS account and Redshift console, it's time to pick and select your cluster. 
 
 As you do this, remember that the capacity you'll need and utilize depends primarily on the number of unique tables and columns created in the cluster, not the number of events (database records).
 Each unique `.track(_)` event creates a new table, and each property sent creates a new column in that table. For this reason, think about creating a detailed tracking plan to make sure that all events being passed to Astronomer are necessary and consistent.

 There are two kinds of Redshift clusters, Dense Compute and Dense Storage. 

 ### 1. Pick a cluster

 #### Dense Compute Cluster
Dense Compute clusters maximize query speed and performance, but in turn have less capacity for storage. While there is no set process to size a cluster, most customers with less than 20 million monthly events start with a single DC1 cluster and add nodes as needed. A single node cluster includes 200GB of storage and a maximum side of 2.56TB. 

#### 2. Dense Storage Cluster
Dense storage clusters maximize storage capacity and allow customers with hundreds of millions of events to save money on Redshift hosting costs by using disk-based storage, slower CPU's, and less RAM. A single DS2 node cluster includes 2TB of space, with a max size of 16TB.



### 2. Provision it.

(If you already have a Redshift cluster, go ahead to step 3!)

1. Open the Redshift Console 
2. CLick on "Launch Cluster"
3. Input cluster details 
4. Choose cluster size
5. Set up your cluster Security Group or VPC and proceed to review


## Step 2. Select Your Cluster

Click on the 'Clusters' tab from the left hand menu and into the cluster you wish to send data into from Astronomer. If you have not yet created a cluster on Redshift yet, simply click the 'Launch Cluster' button and [follow the configuration steps](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-launch-sample-cluster.html).

<b>IMPORTANT:</b> <i>Your <b>Username</b> and <b>Password</b> that you put into your Astronomer account are the credentials you used when you initially created the cluster or created a specific user profile for Astronomer. In neither case should you use your master AWS credentials. If you want to switch clusters in the future, make sure you update your Username and Password as needed.</i>

#### Make sure that you whitelist 52.86.240.182 as an incoming IP Address so we can write to your Redshift instance without you exposing the database to everyone. For more information on, please explore our [Networking Guide](/1.0/guides/network/)

<br>

## Step 3: Identify Your Host, Port, and Database Name

The Host and Port are found at the top beside the label 'Endpoint,' with Host coming before the ':' and Port coming afterwards. The Database Name is found at the bottom besides a title of the same name.

![connecting-redshift3](/1.0/assets/img/guides/streaming/clickstream/amazon-redshift/amazon-redshift3.png)


#### Please either create an Inbound Rule to accept data from anywhere (0.0.0.0) or (the safer option) whitelist the following IP address: 52.86.240.182

## Step 4: Activate Integration on Astronomer

After you've identified the <b>Username, Password, Host, Port,</b> and <b>Database Name</b>, put all of these credentials into your Astronomer account and give your new connection a unique name. Note that your *Database* and *Schema* are kept separate from your other connection credentials. *Schema* is required but it is up to personal preference on what value to input as it can be thought as a folder to store your clickstream in. Example values include "analytics_ios", "clickstream_web", etc.

Click 'Create Destination' and your pipeline will be activated.

![connecting-redshift1](/1.0/assets/img/guides/streaming/clickstream/amazon-redshift/amazon-redshift1.gif)
---

That's it! Really simple, wasn't it? You'll now be receiving a livestream of data from your app into your private Redshift account.
