---
title: VWO
sidebar: platform_sidebar
---

Astronomer Clickstream makes it easy to send your data to VWO. Once you follow the steps below, your data will be routed through our platform and pushed to VWO in the appropriate format.

## What is VWO and how does it work?

VWO is a web and mobile optimization platform that creates varied web campaigns for A/B testing. It tracks revenue, clicks, signups, and conversion goals so that marketers can analyze performance. It also monitors user engagement by providing heatmaps and click analytics for a full visualization of how your customers are interacting with your site.

Using VWO natively requires the installation of their JavaScript library. Experiments can then be deployed within the VWO web app. You will need to write custom code if you want to export experiment data for analysis or include other tools in your marketing automation stack.

## Why send data to VWO using Astronomer Clickstream?

Since VWO loads data synchronously, we can't add their JavaScript snippet for you. However, integrating VWO with Astronomer Clickstream eliminates the need to add custom code to your site if you want to include other tools in your analytics stack. By triggering an event when a visitor views an experiment variation, Astronomer allows you to send A/B test data downstream of your other integrations. You can use this downstream data in an analytics tool of your choice, or dump it in a warehouse for more advanced analytics.

## Getting Started with VWO and Astronomer Clickstream

### VWO Side

To get started, you'll need to add the VWO JavaScript snippet to the pages that you want to track. You can check out their docs on how to do that [here](https://vwo.com/knowledge/add-vwo-smartcode-to-your-website/).  

### Astronomer Side

Since the VWO snippet is now on your site, all you need to do is enable the VWO integration in your Astronomer UI to get started. Note that there are a few different custom metrics you can track to VWO. We have outlined how to set up those methods below.

### Additional Features

#### Sending Experiment Data from VWO

Begin by checking the option to `Send experiment data to other tools` for either a `track` or `identify` call in your VWO UI.

![vwo1](../../../images/vwo1.png)

In JavaScript, a `track` call that sends experiment data to another tool will look like this:
```
analytics.track('Experiment Viewed', {
    experiment_id: 'Astro-home-page-title-1`
    variation_name: 'Stop wondering what your users want.'
});
```

#### Sending Revenue Data from VWO

You can send revenue data from VWO as a `track` event. You would do this with the following example code:
```
analytics.track('Order Completed'. {
        total: 100  
});
```





