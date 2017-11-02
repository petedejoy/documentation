---
title: Overview
sidebar: platform_sidebar
---

# Overview

The key to delighting customers is understanding them. Since identifying what they do-or don't do-is crucial to understanding their actions, thousands of tools exist to help marketers and product managers analyze user engagement with a website or app. As if selecting the right tools isn't challenging enough, accessing the fast-accumulating data for internal analysis is often a struggle, and the cost of switching to a better tool down the road can result in a major loss of data.

The Astronomer Clickstream module allows you to capture every user event from web, mobile, and server side sources. Once those events are ingested into our platform, we can push them to a data warehouse, CRM, or analytics tool of your choice. Implementing our Clickstream module in your current infrastructure allows you to better understand how exactly users are interacting with your web and mobile apps so that you can tailor marketing and product focus accordingly.

# Getting Started

Once you've [signed up](https://app.astronomer.io/signup) for an account, it only takes a few minutes to start collecting valuable behavior data with Astronomer. 

Use one of our library sources to record user data from your website, mobile app, or servers. We'll transform and route that data to all of the destinations you've enabled.

## Sources

Collecting customer data from your website, mobile app, or servers is easy, and we've built an integration with each of the following platforms. 

Check it out:

* [Analytics.js](/v2/clickstream/sources/analyticsjs.html)
* [Android](/v2/clickstream/sources/android.html)
* [HTTP API](/v2/clickstream/sources/httpapi.html)
* [iOS](/v2/clickstream/sources/ios.html)
* [MeteorJS](/v2/clickstream/sources/meteorjs.html)
* [.NET](/v2/clickstream/sources/net.html)
* [Node.js](/v2/clickstream/sources/nodejs.html)
* [PHP](/v2/clickstream/sources/php.html)
* [Python](/v2/clickstream/sources/python.html)
* [Ruby](/v2/clickstream/sources/ruby.html)

## Destinations
Check out the list below to explore all of the destinations available with Astronomer Clickstream. From there, make your way to each destination's docs and setup guide to see how to use them!

* [Acquisio](/v2/clickstream/destinations/acquisio.html)
* [Amazon Redshift](/v2/clickstream/destinations/amazon-redshift.html)
* [Amplitude](/v2/clickstream/destinations/amplitude.html)
* [Calq](/v2/clickstream/destinations/calq.html)
* [Clicky](/v2/clickstream/destinations/clicky.html)
* [Criteo](/v2/clickstream/destinations/criteo.html)
* [Customer.io](/v2/clickstream/destinations/customerio.html)
* [DoubleClick Floodlight](/v2/clickstream/destinations/doubleclick-floodlight.html)
* [Heap Analytics](/v2/clickstream/destinations/heap-analytics.html)
* [Hubspot](/v2/clickstream/destinations/hubspot.html)
* [Intercom](/v2/clickstream/destinations/intercom.html)
* [Keen IO](/v2/clickstream/destinations/keen-io.html)
* [KISSmetrics](/v2/clickstream/destinations/kissmetrics.html)
* [Lytics](/v2/clickstream/destinations/lytics.html)
* [Mixpanel](/v2/clickstream/destinations/mixpanel.html)
* [Optimizely](/v2/clickstream/destinations/optimizely.html)
* [Pinterest](/v2/clickstream/destinations/pinterest.html)
* [Resonate](/v2/clickstream/destinations/resonate.html)
* [Retention Science](/v2/clickstream/destinations/retention-science.html)
* [Rubicon](/v2/clickstream/destinations/rubicon.html)
* [S3 Event Logs](/v2/clickstream/destinations/s3-event-logs.html)
* [Taboola](/v2/clickstream/destinations/taboola.html)
* [Twitter Ads](/v2/clickstream/destinations/twitter-ads.html)
* [Webhooks](/v2/clickstream/destinations/webhooks.html)
* [Woopra](/v2/clickstream/destinations/woopra.html)

## Calls
[Here](/documentation/v2/clickstream/calls.html), we outline the different types of customer data we capture and how to implement them for your business.

## Segment | Clickstream Merge

Made the switch from Segment to Astronomer Clickstream but want to have all of your data in one place? It's an easy process - we'll walk you through it. 

Check out this [blog post](https://www.astronomer.io/blog/switch-from-segment-to-astronomer-in-four-simple-st/) and follow the steps below:  

### Initial Column Audit

To start, we'd recommend that you take a few minutes to review your existing Segment tables with the tables created by Astronomer's Clickstream platform. Create a spreadsheet with tables from both platforms side by side to easily identify datatype conflicts. 

Here's the SQL to view that information:

```
SELECT * FROM information_schema.columns
WHERE table_schema = 'example_schema_name'
AND table_name = 'example_table_name'
```

### Datatype Conflicts

If you do identify some datatype conflicts, it's likely that your destination column will be able to accomodate the previous datatype (e.g. varchar(256) or varchar(512) or timestamp with timezone. Check out the following example:

![clickstream-merge1](../../../images/clickstream-merge1.png)

### Non-Existent Destination Columns

If you have some columns that don't exist in the destination tables, they'll need to either be dropped from the source (Segment) tables or added manually to the destination tables. 

You can do the latter manually via the [Alter Table Add Command](http://docs.aws.amazon.com/redshift/latest/dg/r_ALTER_TABLE.html).

### Differing Ordinal Positions

If the ordinal position differs between the two tables, a Bulk Insert ((e.g. `INSERT INTO {DESTINATION_TABLE} (SELECT * FROM SOURCE_TABLE}`) is slightly more complicated.

From here, you'll have 2 options: 

**A) Bulk Insert**

Here, use the specific column order as the destination tables rather than`SELECT` (see below)

![clickstream-merge2](../../../images/clickstream-merge2.png)

**B) Unload to S3 and then Copy**

This has a few more steps, but will likely be less taxing on your db depending on your row count. 

1. [Unload each source table to S3](http://docs.aws.amazon.com/redshift/latest/dg/r_UNLOAD.html)

2. [COPY each file from S3 into the corresponding destination table](http://docs.aws.amazon.com/redshift/latest/dg/r_COPY.html)

Here, you can specify the column order of the destination table that the file should load into. 

