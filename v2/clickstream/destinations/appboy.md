---
title: Appboy
sidebar: platform_sidebar
---
Astronomer Clickstream makes it easy to send your data to Appboy. Once you follow the steps below, your data will be routed through our platform and pushed to Appboy in the appropriate format. 

## What is Appboy and how does it work?

Appboy is a mobile marketing automation platform that allows your marketing team to engage with audience across lifecycles. It does this by pooling first-party and third-party data through APIs, in-store purchases, and mobile information. Appboy also automates email delivery by using predictive analytics to decipher optimal messaging time based on user actions or API triggers.

Because Appboy has a predictive analytics component, it functions most effectively when all of your customer data is available in the tool. In order to collect this data across multiple channels, you would need to do a lot of upfront work: planning about what customer data you want to track, learning and implementing Appboy SDKs, and implementing server-to-server API calls.

## Why send data to AppBoy using Astronomer Clickstream?

Integrating Appboy with Astronomer Clickstream means that you can track users accross your web, mobile, and server-side apps. Without installing additional code in the form of Appboy SDKs or API libraries, you'll be able to recieve all [`identify` and `track` calls](,,/calls.html) in the format that Appboy understands.

## Getting started with AppBoy

Note that you can only integrate Appboy with server-side and mobile sources.

### Appboy Side

Once you've created your Appboy account, you'll need to find your `App Group Identifier`. You can find this ID in the Appboy Dashboard under `App Settings-->Developer Console`. 

### Astronomer side

Paste your `App Group Identifier` into the approprate field in your Astronomer UI to get your data flowing!
