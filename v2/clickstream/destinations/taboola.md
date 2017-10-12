---
title: Taboola
sidebar: platform_sidebar
---
#NOT DONE
To get started sending events to Taboola, all you'll need is your script source, which can be retrieved when you create your Taboola conversion tracking code.

### This connector supports client-side analytics.js only.  You also need to have instrumented Astronomer [inside your website](https://docs.astronomer.io/docs/1.0/streaming/clickstream/collectors/analyticsjs/) prior to enabling this connector.

### Step 1:
Create a [Taboola](https://www.taboola.com/) account. After you create your account, [create your Taboola conversion tracking code](https://help.taboola.com/hc/en-us/articles/115006164967-Creating-Your-Conversion-Tracking-Code).

### Step 2:
Find your script source, which can be found inside of your conversion tracking code, shown as `ScriptSrc` below:

``` javascript
<script src="//cdn.taboola.com/libtrc/ScriptSrc/tfa.js"></script>
```

### Step 3
Copy your `ScriptSrc`, paste it into the "Script Source" field in your Astronomer Taboola configuration, and give your new connection a unique name. Click 'Create Destination' and your pipeline will be activated.

Optionally, you can specify custom event names in the Conversion Events section, shown as `my_custom_event` in the example below.

![taboola1](/1.0/assets/img/guides/streaming/clickstream/taboola/taboola1.png)

### Step 4:
After a couple of minutes, you should be able to refresh your website and see the Taboola firing for page views and any custom events!
