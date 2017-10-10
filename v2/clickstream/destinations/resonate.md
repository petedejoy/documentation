---
title: Resonate
sidebar: platform_sidebar
---

To get started sending events to Resonate, you'll need to have signed up for [Resonate](https://www.resonate.com/), worked with a Resonate professional services director to create your company's specific campaign, and received your page impression, identify, and tracking `<img>` tags from them.  

### This connector supports client-side analytics.js only.  You also need to have instrumented Astronomer [inside your website](https://docs.astronomer.io/docs/1.0/streaming/clickstream/collectors/analyticsjs/) prior to enabling this connector.

### Step 1:
Retrieve your Resonate page impression and tracking tags from your professional services director. Ensure that you can identify which tags are page impression tags, and which are custom or conversion tags.

The tags will contain important parameters that you'll need from step two.  The following parameters are the same for every tag: `advkey`, `opptykey`.  The `event key` is unique to each tag, and is shown as `my_event_key` below.  We take care of the `cache_buster`.

``` javascript
<IMG SRC="https://ds.reson8.com/insights.gif?rand=[cache_buster]&t=0&pixt=resonate&advkey=my_advkey&opptykey=my_opptykey&evkey=my_event_key&evtype=custom" WIDTH=1 HEIGHT=1 BORDER=0>
```

The identify tag is a bit different, and you can extract your `User Tracking Key` from here, shown as `user_tracking_key` below.

``` javascript
<img src="https://ds.reson8.com/insights.gif?rand={{ cacheBuster }}&t=0&pixt=resonate&advkey={{ my_advkey }}&opptykey={{ my_opptykey }}&evkey={{ evkey }}&evtype={{ evtype }}&resnc1=esp&resnc2=open&resnc3={{ user_tracking_key }}">
```

### Step 2:

Copy your common tag parameters (`advkey`, `opptykey`), as well as your `User Tracking Key` from the identify tag,  and paste them into your Astronomer Resonate configuration.  

Next, you'll need to provide your page impression tag event key, as well as any custom events and their respective event keys (shown as `evkey` in the snippet above).  Give your new Resonate connection a name, and choose "Create Destination."

![resonate1](/1.0/assets/img/guides/streaming/clickstream/resonate/resonate1.png)

### Step 3:

Confirm with your Resonate professional services director that the `<img>` tags for your specific campaign are being received by them as expected.
