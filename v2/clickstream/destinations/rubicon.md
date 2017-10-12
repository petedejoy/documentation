---
title: Rubicon
sidebar: platform_sidebar
---
#NOT DONE
To get started sending events to Rubicon, you'll need to have signed up for the [Rubicon Project](http://rubiconproject.com/), worked with an account manager to create your company's specific campaign, and received your Page ID, Conversion ID, and any conversion event names from them.  

### This connector supports client-side analytics.js only.  You also need to have instrumented Astronomer [inside your website](https://docs.astronomer.io/docs/1.0/streaming/clickstream/collectors/analyticsjs/) prior to enabling this connector.

### Step 1:
Retrieve your Rubicon Page ID, Conversion ID, and conversion event names from your account manager.

### Step 2:
Within your Astronomer Rubicon connector UI, give your new connection a unique name.  Then, paste your Page ID into the "pid" field, and your Conversion ID into the "Conversion ID" field.  In the "Conversion Events" area, paste in any conversion event names given to you by Rubicon.  If you have more than one conversion event, choose the `+` icon to add more.

![rubicon1](/1.0/assets/img/guides/streaming/clickstream/rubicon/rubicon1.png)

With your configuration entered, choose "Create Destination."

### Step 3:

Generate page views and events on your website by triggering `analytics.track('your conversion event name');`.  Confirm with your Rubicon account manager that conversion events for your specific campaigns are being received as expected.
