---
title: Criteo
sidebar: platform_sidebar
---
#NOT DONE
To get started sending events to Criteo, you'll need to have signed up for [Criteo Remarketing](http://www.criteo.com/) and working with a Criteo Account Strategist to plan your remarketing campaign.  You'll need a few technical components from your Account Strategist to move forward with enabling this connector.

### This connector supports client-side analytics.js only.  You also need to have instrumented Astronomer [inside your website](https://docs.astronomer.io/docs/1.0/streaming/clickstream/collectors/analyticsjs/) prior to enabling this connector.

### Step 1:
Retrieve and deploy the latest version of Criteo's loader file (a `.js` file that should get loaded into your page by your servers).  You'll also need your remarketing campaign tags to enable tracking with Astronomer.

### Step 2:
With your loader `.js` file deployed on your page, you're ready to configure the Criteo connector within your Astronomer UI.  

Copy your Criteo Account ID into the "Account ID" field in your Astronomer Criteo configuration, and give your new connection a unique name. 

(Optional) You can also map custom event names to a few of Criteo's reserved keywords in the Conversion Events area.  In the example shown, `myEventName` is a custom event mapped to Criteo's `trackTransaction` event name.


![criteo1](/1.0/assets/img/guides/streaming/clickstream/criteo/criteo1.png)

Click 'Create Destination' and your pipeline will be activated.

### Step 3:
Confirm with your Criteo Account Strategist that the loader `.js` file and any custom remarketing campaign tags that you've entered are being received as intended.
