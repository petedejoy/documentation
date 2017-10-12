---
title: Keen IO
sidebar: platform_sidebar
---
#NOT DONE
To get started sending events to Keen IO, you'll need a Project ID and Write Key. The ID is what tells Astronomer which project within Keen IO is yours and the Write Key gives Astronomer permission to send data into it. Both will be long strings of random characters (the ID will be 24 characters and the Write Key will be 224.)

<b>Step 1</b> Create a Keen IO account via their [website](http://www.keen.io)

<b>Step 2</b> Keen IO is kind enough to create your first project for you so you already have anything you'll need. They even have a reminder that you haven't sent any data to them yet. We'll fix that soon enough ;) For now, copy over your Project ID and Write Key (which you can get by clicking on 'Show API Keys')

![keen-io1](/1.0/assets/img/guides/streaming/clickstream/keen-io/keen-io1.png)


<b>Step 3</b> Add your Project ID and Write Key into the Keen IO integration on your Astronomer dashboard and give your new connection a unique name. Click 'Create Destination' and your pipeline will be activated.

![keen-io2](/1.0/assets/img/guides/streaming/clickstream/keen-io/keen-io2.gif)

<b>Step 4</b> Click around your app to send off some test events and then go back to Keen IO to see those events begin populating your project! They should appear in less than a minute!

![keen-io3](/1.0/assets/img/guides/streaming/clickstream/keen-io/keen-io3.png)
