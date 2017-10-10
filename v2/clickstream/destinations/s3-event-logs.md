---
title: S3 Event Logs
sidebar: platform_sidebar
---

Astronomer makes it easy to copy broadcasted events to an [Amazon Simple Storage Service (S3) bucket](https://aws.amazon.com/s3/).  You'll only need to configure the S3 Event Logs connector within your [Astronomer App](https://app.astronomer.io/), and include our bucket policy.

### Step 1: 
Create an [Amazon S3 bucket](https://aws.amazon.com/s3/) within your Amazon Web Services account. 

![s3-event-logs1](/1.0/assets/img/guides/streaming/clickstream/s3-event-logs/s3-event-logs1.png)

### Step 2:

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
![s3-event-logs2](/1.0/assets/img/guides/streaming/clickstream/s3-event-logs/s3-event-logs2.gif)


### Step 3:
Configure a new S3 connection in your Astronomer dashboard and give your new connection a unique name. Click 'Create Destination' and your pipeline will be activated.

**AWS Region (required)**
The region in which your S3 bucket resides. You can find a list of regions for [Amazon S3 under the "Region" column here](http://docs.aws.amazon.com/general/latest/gr/rande.html#s3_region). Enter your region exactly as it's shown (i.e. `us-east-1`).

**S3 Bucket Name (required)**
The exact name of your S3 bucket.

**Server Side Encryption (optional)**
AWS S3 supports [server side encryption](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html). If your bucket policy requires the server side encryption header to be set, you can specify that here. Example values for this field are 'AES256' or 'aws:kms'.

**Path Prefix (optional)**
The file path at which your S3 events will be stored. 

![s3-event-logs3](/1.0/assets/img/guides/streaming/clickstream/s3-event-logs/s3-event-logs3.gif)

