---
title: Acquisio
sidebar: platform_sidebar
---

To get started sending events to Acquisio, you'll need to have signed up for [Acquisio](http://www.acquisio.com/), worked with an account manager to create your company's specific campaign, and received your Advertiser ID and any custom event names from them.  

### This connector supports client-side analytics.js only.  You also need to have instrumented Astronomer [inside your website](https://docs.astronomer.io/docs/1.0/streaming/clickstream/collectors/analyticsjs/) prior to enabling this connector.

### Step 1:
Retrieve your Advertiser ID and custom event names from your Acquisio account manager.

### Step 2:
Within your Astronomer Acquisio connector UI, give your new connection a unique name.  Then, paste your Advertiser ID into the "Advertiser ID" field.  In the "Events" area, paste in any conversion event names given to you by Acquisio.  If you have more than one custom event, choose the `+` icon to add more.

![acquisio1](/1.0/assets/img/guides/streaming/clickstream/acquisio/acquisio1.png)

With your configuration entered, choose "Create Destination."

### Step 3:

Generate page views and events on your website by triggering `analytics.track('your custom event name');`.  Confirm with your Acquisio account manager that custom events for your specific campaigns are being received as expected.
