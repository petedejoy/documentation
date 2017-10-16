---
title: KISSmetrics
sidebar: platform_sidebar
---
Astronomer Clickstream makes it easy to send your data to KISSmetrics. Once you follow the steps below, your data will be routed through our platform and pushed to KISSmetrics in the appropriate format. 

## What is KISSmetrics and how does it work?

KISSmetrics is a behavioral email and analytics platform. It pulls cross-platform behavior reports so that marketers can analyze key audience growth statistics. It also supports automated or maula targeted emails based on completed custom actions, unique events, or funnels. At a high level, KISSmetrics gives marketers an overview of custom populations, population change, and growth, so that they can analyze these populations from customers who have completed specific actions or events.

Installing KISSmetrics requires mapping out your eventsand user traits to be collected, decide which libraries and SDKs you need to collect that data, and install them into your products. KISSmetrics event reporting is easy to use if your events are planned following best practices, but it takes a ton of work to get this set up correctly. 

If you are planning on setting up literally any other tool that requires event data, you should evaluate if it is worth your developers' time to add more than one tool. If you are planning on adding multiple analytics tools to your stack, event tracking ad custom coding work is going to be repetitive and time-consuming for your dev team.

## Why send data to KISSmetrics using Astronomer Clickstream?

Using Astronomer to send data to KISSmetrics ensures that your developers only need to implement one platform and learn two simple calls: `identify` and `track`. Without Astronomer, you would need to set up custom code for this tool and any other tool you are planning on using.

## Getting Started with 'DESTINATION' and Astronomer Clickstream

To get started sending events to Kissmetrics, you'll need your project specific API Key. The ID is what tells Astronomer which project within Kissmetrics is yours and the Write Key gives Astronomer permission to send data into it. Both will be long strings of random characters (the ID will be 24 characters and the Write Key will be 224.)

After creating a KISSmetrics account, you'll need to integrate Kissmetrics into your app. Luckily, this can be done through Astronomer; you'll just need your API Key which is a 40 character string that you'll be able to find in the javascript snippet they suggest adding to your app.

![kissmetrics1](/1.0/assets/img/guides/streaming/clickstream/kissmetrics/kissmetrics1.png)

Add your API Key into the Kissmetrics connector on your dashboard and give your new connection a unique name. Click 'Create Destination' and your pipeline will be activated.

![kissmetrics2](/1.0/assets/img/guides/streaming/clickstream/kissmetrics/kissmetrics2.gif)

Click around your app to send off some test events. It might take an hour or so for events to start populating into your project. You can check to see if events are coming in by clicking on the 'Live' tab at the top of the page and looking athe 'All Activity' section.

![kissmetrics3](/1.0/assets/img/guides/streaming/clickstream/kissmetrics/kissmetrics3.png)

