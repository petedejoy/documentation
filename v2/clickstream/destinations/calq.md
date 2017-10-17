---
title: Calq
sidebar: platform_sidebar
---
## What is Calq and how does it work?

Calq is a custom analytics tool for mobile and web apps. It supports custom funnels to allow marketers to view user flow, user drop off, product views, and user events. On top of those custom funnels, Calq enables retroactive funnels, allowing marketers to analyze historical actions such as products viewed, products added to cart, and category page viewed. It generates real-time reports that live-stream customer actions and provides query builders that allow marketers to write custom queries. It also allows developers to create custom properties and queries using "Action Query Language," which is similar to SQL.

Calq does advanced custom analytics for mobile and web apps. Sending data to Calq requires the use of the Calq API, which is facilitated by the available SDKs they provide. Implementing these collection methods requires manual additions to your application client or server code.

## Why send data to Calq using Astronomer Clickstream?

Installing Calq as a standalone tool in your stack will require carefully mapping out your events and user traits to be collected, deciding how to use a Calq SDK or API endpoint to collect the data, and performing the necessary implementations into your products. 

Integrating Calq with Astronomer Clickstream means that you will not need to install a Calq SDK, as Astronomer is able to collect and route information directly to Calq. Toward that objective, we make it much simpler to get started with Calq and our integration requires no changes to your code. Furthermore, since Astronomer can collect and transform data directly from Calq, you do not need to include any Calq code in your applcations. You'll recieve the benefits of tracking directly with Calq without any of the time, labor, and app load costs associated with adding new tracking code into your apps.

## Getting Started with Calq and Astronomer Clickstream

Astronomer Clickstream makes it easy to send your data to Calq. Once you follow the steps below, your data will be routed through our platform and pushed to Calq in the appropriate format. 

Once you create an account with Calq, you'll be asked to create a new project.

![calq1](/1.0/assets/img/guides/streaming/clickstream/calq/calq1.png)

After you create a new project, you will be given a write key. 

![calq2](/1.0/assets/img/guides/streaming/clickstream/calq/calq2.png)

Copy this key and add it into your Astronomer UI to get started. Click 'Create Destination' to activate your pipeline.


If you look back at your Calq account, you should see a message confirming that events have been recieved.

![calq4](/1.0/assets/img/guides/streaming/clickstream/calq/calq4.png)
