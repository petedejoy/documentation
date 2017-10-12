---
title: Google Analytics
sidebar: platform_sidebar
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

  * Any iOS or Android apps running our mobile libraries will start sending data to Google Analytics. New setting will take up to an hour to propagate to all of your existing users. If you added the iOS or Android library to your app code, it will be instanteous. 

  * Google Analytics will start automatically collecting data on your site or mobile app. It takes Google a couple of hours to process this data and add it to your reports, but you should still see events showing up in the real-time events dashboard. 

## Additional Functionality

### Page & Screen
For every `page` call, we send a pageview to Google Analytics. The resulting `page` event name in Google Analytics will correspond to the `fullName` of your page event. `fullName` consists of a combination of the `category` and `name` parameters of `page` calls.

Note that when sending `page` views from a server-side library, a `url` property is required for Google Analytics to accept your `page` event.

Also note that when calling `screen` in a mobile app, we'll send a screen view to Google Analytics but when calling `screen` server-side, you must pass in an application name through the `context.app.name` object for Google Analytics to accept your event.

Ive you've set an application name in your Android or iOS project, Segment will grab the name and pass `context.app.name` automatically. For iOS, we collect your project's `infoDictionary` and use whatever name you've set there. 

### Identify
Since it's against Google's Terms of Service to send Personally Identifiable Information (PII) to your Analytics reporting interface, we will never pass anything from an `identify` to Google unless you specifically tell us to. 

#### User ID
Google Analytics allows you to set a User-ID for your identified visitors. [Read more about their universal tracking method here.](https://support.google.com/analytics/answer/3123663)

To utilize this feature, you'll need to enable User-ID in your Google Analytics property and [create a User-ID view.](https://support.google.com/analytics/answer/3123666)

### Track
We'll record a Google Analytics event whenever you make a `track` call (see events in Google Analytics in Behavior -> Events -> Overview).

## Beyond the Basics
As mentioned above, Astronomer will automatically enable `Track Named Pages` and `Track Categorized Pages`. You'll notice that there a quite a few other Destination Details. Keep reading to learn what those are and why you might want to use them.

#### Use Classic Analytics on Your Site
When creating your Google Analytics profile, you can choose between Classic and Universal Analytics. Profiles created after March 2013 default to Universal while earlier profiles are Classic. 

To check your version, look for `_gaq.push` in your code. If you see it, you're using Classic and will need to enable this. 

#### Remarketing, Display Ads, and Deomgraphic Reports
Turn this feature on to use Google's remarketing tag (what was formely known as Doubleclick) or to identify demographic and interest data on visitors that is displayed in Demographic & Interest reports in Google Analytics.

#### Cookie Domain Name

#### Enable Enhanced E-commerce

#### Ignored Referrers

#### Track Named Pages

#### Track Categorized Pages

#### Include Querystring in Page Views

#### Anonymize IP Addresses

#### Enable Enhanced Link Attribution

#### Add the Non-interaction Flag to All Events

#### Site Speed Sample Rate

#### Use Classic Analytics for Your Serverside Tracking

#### Send User-ID to GA
**Important** If you are passing an email, phone number, full name, or any other PII as the `ide` in identify, do not use this feature as it is against the Google Analytics Terms of Service and your account could be suspended. 

#### Send Uncaught Exceptins to GA (Mobile)


