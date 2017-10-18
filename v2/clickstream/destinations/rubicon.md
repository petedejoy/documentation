---
title: Rubicon
sidebar: platform_sidebar
---
Astronomer Clickstream makes it easy to send your data to Rubicon. Once you follow the steps below, your data will be routed through our platform and pushed to Rubicon in the appropriate format. 

## What is Rubicon?

Rubicon is an adtech company used by publishers to perform transactions with top brands around the globe. It offers a unified platform, dynamic campaigns, brand protection, and a global marketplace for anyone who wants to buy or sell advertisements.

## Why send data to Rubicon using Astronomer Clickstream

Using Astronomer data to power or complement your Rubicon platform will allow you to more insightfully gauge the way your customers engage with your ads. Automating this pipeline with Astronomer will not only save you a headache, but also will allow you to make more informed business decisions.  

## Getting Started with Rubicon and Astronomer Clickstream

### Rubicon Side 

Once you're signed up on [Rubicon Project](http://rubiconproject.com/), work with your account manager to:
- Create your company's specific campaign
- Retrieve your your Page ID, Conversion ID, and any conversion event names from them.  

*Note:* This connector supports client-side analytics.js only. You need to have implemented Astronomer [inside your website](../sources/analyticsjs.md) prior to enabling this connector.


### Astronomer Side

Within your Astronomer Rubicon connector UI, give your new connection a unique name.  

Then, paste your Page ID into the `pid` field, and your Conversion ID into the `Conversion ID` field.  In the `Conversion Events` area, paste in any conversion event names given to you by Rubicon.  If you have more than one conversion event, choose the `+` icon to add more.

![rubicon1](https://docs.astronomer.io/docs//1.0/assets/img/guides/streaming/clickstream/rubicon/rubicon1.png)

With your configuration entered, choose `Create Destination.`

Generate page views and events on your website by triggering `analytics.track('your conversion event name');`.  Confirm with your Rubicon account manager that conversion events for your specific campaigns are being received as expected.
