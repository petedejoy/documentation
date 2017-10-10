---
title: Pinterest
sidebar: platform_sidebar
---

To get started sending events to Pinterest, you'll need to have signed up for [Pinterest for Business](https://business.pinterest.com/en).

### This connector supports client-side analytics.js only.  You also need to have instrumented Astronomer [inside your website](https://docs.astronomer.io/docs/1.0/streaming/clickstream/collectors/analyticsjs/) prior to enabling this connector.

### Step 1:
Log into your [Pinterest for Business](https://business.pinterest.com/en) account.  You'll need to create your conversion tracking tags.  To do so, choose from the "Ads" dropdown and select "Conversion Tracking."

![pinterest1](/1.0/assets/img/guides/streaming/clickstream/pinterest/pinterest1.png)

On the next page, choose "Create a Pinterest tag".

![pinterest2](/1.0/assets/img/guides/streaming/clickstream/pinterest/pinterest2.png)

Give your new tag a custom name, and choose "Next."  

### Step 2:

The resulting page will show your Pinterest conversion tag for that custom event name.

![pinterest3](/1.0/assets/img/guides/streaming/clickstream/pinterest/pinterest3.png)

The generated Pinterest tag contains a value shown in red in two places.  Copy this value.

Note: we will fire `page` views for you, but you'll need to map in your custom events in order to fire those.

### Step 3:

Inside the Astronomer UI for Pinterest Conversion Tracking, give your new Pinterest connection a name.  Then, provide your custom event name and paste the value for that event (shown in red in Step 2).  Choose "Create Destination."

![pinterest4](/1.0/assets/img/guides/streaming/clickstream/pinterest/pinterest4.png)

### Step 4:

Generate page views and trigger your custom event inside your website with `analytics.track('your event name');`. You should see confirmation of those tags sent to Pinterest inside your Pinterest for Business dashboard, under "Conversion Tracking."
