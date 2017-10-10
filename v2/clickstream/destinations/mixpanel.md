---
title: Mixpanel
sidebar: platform_sidebar
---

This connector allows you to easily send customer data to [Mixpanel](https://mixpanel.com/).  

**Step 1:** Create a Mixpanel account via their [website](http://www.mixpanel.com).  When you sign in for the first time, you should have sample project called "My new project."  

**Step 2:** Click on the drop-down menu at the top right, and choose 'Project Settings'.

![mixpanel1](/1.0/assets/img/guides/streaming/clickstream/mixpanel/mixpanel1.png)

<b>Step 3: </b> A new box will open, containing your Token and API key.  You'll need to copy these two fields into the Astronomer App configuration for Mixpanel later.

![mixpanel2](/1.0/assets/img/guides/streaming/clickstream/mixpanel/mixpanel2.png)

**Step 4:** Set Up the Mixpanel Configuration in your Astronomer App

When you set up your Mixpanel Configuration, you'll see the following required or optional inputs:

Overview Tab:
*Token* (required)(text field)
Copy the 32-character token from your Mixpanel Project Settings, and paste it here.

*API Key* (required)(text field)
Copy the 32-character API Key from your Mixpanel Project Settings, and paste it here.

Add your Token and API Key into the Mixpanel connector on your Astronomer dashboard and give your new connection a unique name. Click 'Create Destination' and your pipeline will be activated.
![mixpanel3](/1.0/assets/img/guides/streaming/clickstream/mixpanel/mixpanel3.gif)

*Enable Mixpanel People* (optional)(checkbox)
By checking this box, all of your analytics.identify() calls will get sent to [Mixpanel's People](https://mixpanel.com/people/).

Events to Increment in People (optional)(text field)
In order to view and segment by last event date and event counts in Mixpanel People, Click "Enable Mixpanel People", and then list the events you want to see in People to the list at the bottom.

*You also have the opportunity to track additional pages by clicking on the appropriate checkbox.*

* Track Named Pages (optional) 

* Track Categorized Pages (optional)

* Track All Pages (optional)


<br>

**Step 5:** Almost immediately, you'll get a notice that Mixpanel is receiving events! Click on 'View Your Data' to start exploring.

![mixpanel6](/1.0/assets/img/guides/streaming/clickstream/mixpanel/mixpanel6.png)

You can see what specific events are coming in by going to the 'Live view' page, located in the left-hand menu bar.

![mixpanel7](/1.0/assets/img/guides/streaming/clickstream/mixpanel/mixpanel7.png)

