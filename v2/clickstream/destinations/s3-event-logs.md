---
title: S3 Event Logs
sidebar: platform_sidebar
---

Astronomer Clickstream makes it easy to send your data to an Amazon S3 bucket. Once you follow the steps below, your data will be routed through our platform and pushed to Amazon S3 in the appropriate format. 

## Why Amazon S3?

Amazon Simple Storage Service (S3) is a scalable, high-speed, low-cost, web-based cloud storage service designed to allow you to store and retrieve any amount of data, at any time, from anywhere on the web. 

Amazon S3 has unmatched durability, provides comprehensive security and compliance capabilities, and offers an extremely flexible set of storage management and administration capabilities. It supports (i) SSL transfers and automatic encryptions for guaranteed data security (ii) network-optimized, physical disk-based, or third-party connector methods for easy data imports and exports, and (iii) object tagging for easy category customization. 


## Why send data to Amazon S3 using Astronomer Clickstream?

Getting raw analytics to Amazon S3 takes heavy development work and ultimately leaves you with data that was designed to power reports within an analytics tool, not the raw data you need for custom analysis. 

When you enable the Amazon S3 integration, raw data from Astronomer Clickstream automatically gets copied into your Amazon S3 bucket. Everything is stored as line-separated JSON objects, which each contains data from a single API called made to our platform. 

In short, save yourself the headache of manually getting your data into an S3 bucket. We'll take care of that, you get to insights. 


## Getting Started with Amazon S3 and Astronomer Clickstream

Astronomer makes it easy to copy broadcasted events to an [Amazon Simple Storage Service (S3) bucket](https://aws.amazon.com/s3/).  You'll only need to configure the S3 Event Logs connector within your [Astronomer App](https://app.astronomer.io/), and include our bucket policy.

### Amazon S3 Side

#### Create an [Amazon S3 bucket](https://aws.amazon.com/s3/) within your AWS account. 

![s3-event-logs1](https://docs.astronomer.io/docs//1.0/assets/img/guides/streaming/clickstream/s3-event-logs/s3-event-logs1.png)

*Note:* See below to confirm your region. 

Once you create the bucket, create a folder labeled `Astronomer-logs` inside of it.  

#### Add our S3 Bucket Policy

Add the following S3 bucket policy, which will grant Astronomer permission to copy events into your S3 bucket using `s3:PutObject`.  In the `Resource:` line of the policy, swap out `YOUR_BUCKET_NAME` for the exact name of your S3 bucket, but keep the `/*` on the end.

```
{
    "Version": "2012-10-17",
    "Id": "Policy1475027027703",
    "Statement": [
        {
            "Sid": "Stmt1475027024994",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::213824691356:user/s3-copy"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
        }
    ]
}

```
![s3-event-logs2](https://docs.astronomer.io/docs//1.0/assets/img/guides/streaming/clickstream/s3-event-logs/s3-event-logs2.gif)


### Astronomer Side 

Configure a new S3 connection in your Astronomer dashboard and give your new connection a unique name. Click `Create Destination` to activate your pipeline.

### Things to Note:

1. *AWS Region (required)*
The region in which your S3 bucket resides. You can find a list of regions for [Amazon S3 under the "Region" column here](http://docs.aws.amazon.com/general/latest/gr/rande.html#s3_region). Enter your region exactly as it's shown (i.e. `us-east-1`).

2. *Server Side Encryption (optional)*
AWS S3 supports [server side encryption](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html). If your bucket policy requires the server side encryption header to be set, you can specify that here. Example values for this field are 'AES256' or 'aws:kms'.

3. *Path Prefix (optional)*
The file path at which your S3 events will be stored. 

![s3-event-logs3](https://docs.astronomer.io/docs//1.0/assets/img/guides/streaming/clickstream/s3-event-logs/s3-event-logs3.gif)


That's it! You're done and ready for insights. 

