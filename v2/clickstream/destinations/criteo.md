---
title: Criteo
sidebar: platform_sidebar
---
## Getting Started with Criteo and Astronomer Clickstream
To get started sending events to Criteo, you'll need to have signed up for [Criteo Remarketing](http://www.criteo.com/) and working with a Criteo Account Strategist to plan your remarketing campaign.  You'll need a few technical components from your Account Strategist to move forward with enabling this connector. Note that this destination supports the client-side analytics.js source only.

Begin by retrieving and deploying the latest version of Criteo's loader file (a `.js` file that should get loaded into your page by your servers).  You'll also need your remarketing campaign tags to enable tracking with Astronomer.

Once your loader `.js` file is deployed on your page, you'll be ready to configure the Criteo connector within your Astronomer UI.  

Copy your Criteo Account ID into the "Account ID" field in your Astronomer Criteo configuration, and give your new connection a unique name. Your pipeline will be activated once you click 'Create Destination.'

## Beyond the Basics

You can also map custom event names to a few of Criteo's reserved keywords in the Conversion Events section. In the example shown, `myEventName` is a custom event mapped to Criteo's `trackTransaction 

![criteo1](/1.0/assets/img/guides/streaming/clickstream/criteo/criteo1.png)
