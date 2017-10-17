---
title: Retention Science
sidebar: platform_sidebar
---

Astronomer Clickstream makes it easy to send your data to Retention Science. Once you follow the steps below, your data will be routed through our platform and pushed to Retention Science in the appropriate format. 

## What is Retention Science?

In their own words, ReSci builds AI software that transforms your customer base into powerful data science predictions. They take the guesswork out of marketing by uncovering and breaking down customer trends to develop and deliver thriving and successful campaigns.

Retention Science offers an automation suite that includes AI powered website personalization, subscription software, and automated email campaigns that unlock predictive and self-optimizing features that in turn deliver increased engagement and purchase rates.

Cortex, ReSci's marketing AI, can power your business with pocket data and predictions, a recommendation engine, and automated segmentation tools.

## Why send data to Retention Science using Astronomer Clickstream

Shipping Astronomer Clickstream data to Retention Science will better inform the Artificial Intelligence software, which in turn will empower your team to launch successful marketing campaigns, whether through email or directly on your website.

Read below for a guide on creating this integration. 


## Getting Started with Retention Science and Astronomer Clickstream

### Retention Science Side.

Once you have an account on [Retention Science](https://www.retentionscience.com/), work with a Retention Science account manager to:

- Create your company's specific remarketing campaign
- Identify your Site ID and tracking `<script>` tags  

*Note:* This connector supports client-side analytics.js only.  You also need to have instrumented Astronomer [inside your website](https://docs.astronomer.io/docs/1.0/streaming/clickstream/collectors/analyticsjs/) prior to enabling this connector.

### Astronomer Side. 

Paste your Site ID into the `Site ID` field in your Astronomer Retention Science configuration, and give your new connection a unique name.

Check the `Enable On-Site` box, click `Create Destination` and your pipeline will be activated. 

**Custom Events & Reserved Events**

You'll notice two additional sections in our UI. Both are optional, but you can use these to map custom events to specific Retention Science events.  

*Note:* Retention Science has a list of reserved event names (`click`, `view`, `email_open`, `email_click`, `shopping_cart`, `checkout_success`, `search`) that should not be entered as custom events.  We've provided those for mapping in the Reserved Events section of our UI. 

[Insert Example Image Here]

### Final Step. 

Confirm with your Retention Science account manager that the `<script>` tags for your specific campaigns are being sent as expected.
