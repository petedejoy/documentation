---
title: destination - Google Analytics
sidebar: 
---

Astronomer makes is super simple to send your data to Google Analytics. Once you've set up your source to start tracking data, we'll translate and route that data to Google Analytics. Keep reading to learn how to use Google Analytics with Astronomer.

## Getting Started with Google Analytics x Astronomer
It only takes a few simple steps to set up Google Analytics in Astronomer. 

Before you begin, make sure you have a Google Analytics account and your unique Tracking ID on hand. The Tracking ID can be found in the Admin panel and should look like  'UA-XXXXXXXX-X'. Also, you will need to remove Google Analytics' snippet from your page if you were using it outside of Astronomer.

Next, head to app.astronomer.io and add a new destination for the source you want to track. Select Google Analytics and you will be brough to a Configure your destination panel. 

Here, you'll need to create a Friendly Name and enter your Google Analytics Tracking ID for the app. With just these two pieces of information, you can click `Create Destination` and Astronomer will start sending your Clickstream data to Google Analytics. 

_Note_, unless you specify otherwise, Astronomer will automatically enable `Track Named Pages` and `Track Categorized Pages`. 

What happens now? Well, once you enable Google Analytics in Astronomer, a couple of different things happen: 
    * Within a couple of minutes, our CDN is updated and our snippet will start loading Google Analytics javascript library onto your web pages. 
    * Your Google Analytics real-time dashboard will start showing live visitors.
    * Any iOS or Android apps running our mobile libraries will start sending data to Google Analytics. 