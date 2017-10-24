---
title: Appboy
sidebar: platform_sidebar
---
Astronomer Clickstream makes it easy to send your data to Appboy. Once you follow the steps below, your data will be routed through our platform and pushed to Appboy in the appropriate format. 

## What is Appboy and how does it work?

Appboy is a mobile marketing automation platform that allows your marketing team to engage with audience across lifecycles. It does this by pooling first-party and third-party data through APIs, in-store purchases, and mobile information. Appboy also automates email delivery by using predictive analytics to decipher optimal messaging time based on user actions or API triggers.

Because Appboy has a predictive analytics component, it functions most effectively when all of your customer data is available in the tool. In order to collect this data across multiple channels, you would need to do a lot of upfront work: planning about what customer data you want to track, learning and implementing Appboy SDKs, and implementing server-to-server API calls.

## Why send data to AppBoy using Astronomer Clickstream?

This guide will explain how to integrate Redshift into Astronomer's clickstream platform as a destination, allowing you to leverage Amazon's technology to access, store, and query your customer data.

Our connector periodically runs an ETL (Extract - Transform - Load) process that pulls raw event data in S3, processes and transforms those raw events into a structured format, and then inserts structured event data from our bucket into your Redshift cluster. 


# Getting started with AppBoy