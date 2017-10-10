---
title: KISSmetrics
sidebar: platform_sidebar
---
To get started sending events to Kissmetrics, you'll need your project specific API Key. The ID is what tells Astronomer which project within Kissmetrics is yours and the Write Key gives Astronomer permission to send data into it. Both will be long strings of random characters (the ID will be 24 characters and the Write Key will be 224.)

### Step 1:
Create a Kissmetrics account via their [website](http://www.kissmetrics.com)

### Step 2:
Before you're able to hit your dashboard, you'll need to integrate Kissmetrics into you app and, as luck would have it, you can do that through Astronomer! You'll need your API Key which is a 40 character string that you'll be able to find in the javascript snippet they suggest adding to your app.

![kissmetrics1](/1.0/assets/img/guides/streaming/clickstream/kissmetrics/kissmetrics1.png)


### Step 3:
Add your API Key into the Kissmetrics connector on your dashboard and give your new connection a unique name. Click 'Create Destination' and your pipeline will be activated.

![kissmetrics2](/1.0/assets/img/guides/streaming/clickstream/kissmetrics/kissmetrics2.gif)

### Step 4:
Click around your app to send off some test events. It might take an hour or so for events to start populating into your project but be patient! They're on their way. Once the first events are sent, the others will start following in much faster. You can check to see if events are coming in by clicking on the 'Live' tab at the top of the page and looking athe 'All Activity' section.

![kissmetrics3](/1.0/assets/img/guides/streaming/clickstream/kissmetrics/kissmetrics3.png)

### Step 5:
Watch [this funny video](https://www.youtube.com/watch?v=FArZxLj6DLk)! You've earned it!
