---
title: DoubleClick Floodlight
sidebar: platform_sidebar
---

Astronomer Clickstream makes it easy to send your data to Doubleclick Floodlight. Once you follow the steps below, your data will be routed through our platform and pushed to Doubleclick Floodlight in the appropriate format. 

##Getting Started with Doubleclick Floodlight and Astronomer Clickstream

With the Doubleclick Floodlight destination, you can make calls directly to Floodlight based on your mapped events. To begin doing this, you'll need your Advertiser ID.Because DoubleClick is a rather expensive platform, you might be going through a DoubleClick Partner, such as [Mightyhive](http://mightyhive.com). If this is the case, you'll have to obtain your Advertiser ID directly from the partner.

You will find this seven-digit code in the "Advertiser ID" section of the Overview tab. Below that, you'll also want to put your Activity Group label (referred to as "type" within Doubleclick) as well as your Activity Tag String Value (referred to as "cat") for tracking page views.

![doubleclick-floodlight](/1.0/assets/img/guides/streaming/clickstream/doubleclick-floodlight/doubleclick.gif)

<b>Step 2 -</b> If you want to pass in specific track events to Doubleclick, you can do so within the Events section in the Advanced tab. Simply specify the name of the event exactly as it is sent to Astronomer and the corresponding Type and CAT values for the Activity Group in DoubleClick.

<b>Step 3 -</b> Custom properties can be added to the events sent to Doubleclick by specifying the specific property and mapping to the corresponding property label in Doubleclick (e.g. u1, u2, etc.)

