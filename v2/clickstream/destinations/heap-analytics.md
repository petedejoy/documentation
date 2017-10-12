---
title: Heap Analytics
sidebar: platform_sidebar
---
#NOT DONE
To get started sending events to Heap, all you'll need is your Event Key, which can be found as soon as you create an account with them.

**Step 1 -** Create a Heap Analytics account via their [website](http://www.heapanalytics.com)

**Step 2 -** A page will load suggesting you install Heap into your app. If you're using Astronomer for a web app, this isn't necessary as you'll be able to copy over the App ID into your Astronomer account. Your App ID will be located at the end of the javascript snippet they provide with the 'heap.load()' function.

![heap-analytics1](/1.0/assets/img/guides/streaming/clickstream/heap-analytics/heap-analytics1.png)

It's important to note here that Heap automatically sets you up with a Development and Production project when you create an account. Make sure you're copying over the right ID as that will affect which project within Heap your data gets sent to.

![heap-analytics2](/1.0/assets/img/guides/streaming/clickstream/heap-analytics/heap-analytics2.png)

<b>Step 3 -</b> Add your App ID into the Heap connector on your Astronomer dashboard and give your new connection a unique name. Click 'Create Destination' and your pipeline will be activated.

![heap-analytics3](/1.0/assets/img/guides/streaming/clickstream/heap-analytics/heap-analytics3.gif)


<b>Step 4 -</b> When you return to your Heap account, you might get a message saying "There's no data here!" Oh no! But actually, look very closely as there might actually be data in a different environment (i.e. development instead of production.)

![heap-analytics4](/1.0/assets/img/guides/streaming/clickstream/heap-analytics/heap-analytics4.png)

You can see what specific events are coming in by going to the 'Events' page, located in the left-hand menu bar.

![heap-analytics5](/1.0/assets/img/guides/streaming/clickstream/heap-analytics/heap-analytics5.png)