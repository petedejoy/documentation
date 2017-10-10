---
title: Retention Science
sidebar: platform_sidebar
---

To get started sending events to Retention Science, you'll need to have signed up for [Retention Science](https://www.retentionscience.com/), worked with a Retention Science account manager to create your company's specific remarketing campaign, and received your Site ID and tracking `<script>` tags from them.  

### This connector supports client-side analytics.js only.  You also need to have instrumented Astronomer [inside your website](https://docs.astronomer.io/docs/1.0/streaming/clickstream/collectors/analyticsjs/) prior to enabling this connector.

### Step 1:
Retrieve your Retention Science Site ID and tracking tags from your account manager.  If you're using any custom events, identify those as well.

### Step 2:

Paste your Site ID into the "Site ID" field in your Astronomer Retention Science configuration, and give your new connection a unique name. Check the "Enable On-Site" box, click 'Create Destination' and your pipeline will be activated. 

You'll notice two additional sections in our UI: the Custom Events and Reserved Events sections.  Both of these are optional, and you can use these to map custom events to specific Retention Science events.  However, Retention Science has a list of reserved event names (click, view, email_open, email_click, shopping_cart, checkout_success, search) that should not be entered as custom events.  We've provided those for mapping in the Reserved Events section of our UI (examples are shown below).

[retention-science1](/1.0/assets/img/guides/streaming/clickstream/retention-science/retention-science1.png)

### Step 3:

Confirm with your Retention Science account manager that the `<script>` tags for your specific campaigns are being sent as expected.
