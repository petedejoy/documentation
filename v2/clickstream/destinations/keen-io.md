---
title: Keen IO
sidebar: platform_sidebar
---
Astronomer Clickstream makes it easy to send your data to Keen.io. Once you follow the steps below, your data will be routed through our platform and pushed to Keen.io in the appropriate format. 

## What is Keen.io and how does it work?

Built for developers, Keen.io is an event data platform for real-time, intelligent data application. The platform allows you to collect and send event data wherever you need, directly build powerful analytics features into your tools and products, and programatically provision role-based data access for your users and customers.

Keen.io supports customizable APIs and a charting library, which gives developers room to build and customize native analytics tools. Plus, their third-party integrations will allow your team to pin point key behavior metrics and pull customer data accordingly. 

[Learn more about Keen.io](https://keen.io/)

## Why send data to Keen.io using Astronomer Clickstream?

Instead of having to manually adapt your code, Astronomer Clickstream's integration automatically collects and transforms data for Keen.io directly from web applications, mobile applications, and server-side implementations. 

Plus, with Astronomer, there is no need to manually install the Keen.io SDK in your web application.

## Getting Started with Keen IO and Astronomer Clickstream

### Keen.io Side 

To get started sending events to Keen IO, you'll need two things:

* `Project ID:` This tells Astronomer which project within Keen IO is yours
* `Write Key:` This gives Astronomer permission to send data to your Keen IO dashboard
Both of these things will be long strings of random characters. 

You can find your Write Key by clicking on `Show API Keys.`

![keen-io1](../../../images/keen-io1.png)

### Astronomer Side

Once you have your Project ID and Write Key, copy both into the Astronomer dashboard. 

Your pipeline will be activated once you click `Create Destination.`

