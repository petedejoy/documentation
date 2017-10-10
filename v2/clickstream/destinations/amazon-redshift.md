---
title: Amazon Redshift
sidebar: platform_sidebar
---

Redshift is Amazon Web Service's custom take on a traditional Postgres database or, as they put it, "[A fully managed petabyte-scale data warehouse service in the cloud.](http://docs.aws.amazon.com/redshift/latest/mgmt/welcome.html)" It is cost-effective at nearly any level, capable of scaling from gigabytes to petabytes without a loss in performance, and uses [columnar storage](http://docs.aws.amazon.com/redshift/latest/dg/c_columnar_storage_disk_mem_mgmnt.html) (among other optimizations) for incredibly fast querying speeds.

With Astronomer's Redshift integration, you can now easily leverage this technology to easily query your customer data.

---

## Step 1: Log in to your AWS account and Redshift console.

![connecting-redshift2](/1.0/assets/img/guides/streaming/clickstream/amazon-redshift/amazon-redshift2.png)

## Step 2: Select Your Cluster

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
