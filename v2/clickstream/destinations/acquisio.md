---
title: Acquisio
sidebar: platform_sidebar
---

Astronomer Clickstream makes it easy to send your data to Acquisio. Once you follow the steps below, your data will be routed through our platform and pushed to Acquisio in the appropriate format. Note that this connector supports client-side analytics.js only.

To get started sending events to Acquisio, you'll need to have signed up for [Acquisio](http://www.acquisio.com/), worked with an account manager to create your company's specific campaign, and received your Advertiser ID and any custom event names from them.  

Once you recieve your Advertiser ID from your account manager, paste it into the "Advertiser ID" field in the Astronomer UI.  In the "Events" area, paste in any conversion event names given to you by Acquisio.  If you have more than one custom event, choose the `+` icon to add more.

With your configuration entered, choose "Create Destination."

Generate page views and events on your website by triggering `analytics.track('your custom event name');`.  Confirm with your Acquisio account manager that custom events for your specific campaigns are being received as expected.
