---
title: Twitter Ads
sidebar: platform_sidebar
---
#NOT DONE
To get started sending events to Twitter Ads, all you'll need is your Twitter Pixel ID, which can be retrieved when you create your Twitter Ads conversion tracking website tag.

### This connector supports client-side analytics.js only.  You also need to have instrumented Astronomer [inside your website](https://docs.astronomer.io/docs/1.0/streaming/clickstream/collectors/analyticsjs/) prior to enabling this connector.

### Step 1:
Create a [Twitter Ads account](https://ads.twitter.com/). After you create your account, choose "Conversion Tracking" from the "Tools" drop down.
![twitterads1](/1.0/assets/img/guides/streaming/clickstream/twitter-ads/twitterads1.png)

### Step 2:
A page will load asking you to accept Twitter Ads' conversion tracking policy. If you agree, check that box and choose "Generate website tag for conversion tracking." 
![twitterads2](/1.0/assets/img/guides/streaming/clickstream/twitter-ads/twitterads2.png)

You'll be taken to a page with instructions on how to set up your universal website tag, along with a code snippet. 

If you want to use the universal tag, simply copy your Twitter Pixel ID from the code snippet (identified below).

![twitterads3](/1.0/assets/img/guides/streaming/clickstream/twitter-ads/twitterads3.png)


### Step 3
Paste your Twitter Pixel ID into the "Page Pixel" field in your Astronomer Twitter Ads configuration, and give your new connection a unique name. Click 'Create Destination' and your pipeline will be activated. 

![twitterads4](/1.0/assets/img/guides/streaming/clickstream/twitter-ads/twitterads4.png)

If you’d like to use the Single Event Website Tags, you must map the event names to your Single Event Website Tags’ respective conversion pixel IDs. 

![twitterads5](/1.0/assets/img/guides/streaming/clickstream/twitter-ads/twitterads5.png)

### Step 4:
After a couple of minutes, you should be able to refresh your website and see the Twitter Ads pixel firing for page views!  If you're using Single Event Website Tags and have those mapped in, you should see specific pixels fire when triggering your respective events.  For example, `analytics.track("Custom Event 1");`, based on the input above, would fire the Twitter Ads pixel `pixel1`, on so on.
