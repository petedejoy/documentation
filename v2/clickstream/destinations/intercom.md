---
title: Intercom
sidebar: platform_sidebar
---

To get started sending events to Intercom, all you'll need is your App Id and API Key. These are a bit hard to get because Intercom typically blocks you from seeing your dashboard until you've sent events to them but we'll show you how to get around that since paradoxically, this is the very information you will need to send those events in the first place.

**Step 1** Put your email into the central 'Enter Your Email' form on their [website](http://www.intercom.io)

**Step 2** A page will load suggesting you asking how you want to set Intercom up....either integrate one of their libraries or import users from another service/csv. We're going to hack this a bit. Stay with me.

![intercom1](/1.0/assets/img/guides/streaming/clickstream/intercom/intercom1.png)

Clicking into the 'Integrate' pathway, we come to this page of options that is pretty much the same as on the page before it. Here's where we diverge from the traditional setup. Click on the 'Segment' option.

![intercom2](/1.0/assets/img/guides/streaming/clickstream/intercom/intercom2.png)

I know! I know! You're still setting up Astronomer (we don't secretly work for Segment, but hey, this is also the process for setting them up so nothing is stopping you; you're welcome Segment.) Anyways, you get to this page and logically click 'Next' to continue the setup.

![intercom3](/1.0/assets/img/guides/streaming/clickstream/intercom/intercom3.png)

Here you'll actually create your account and get started using Intercom. This page is why we went through the Segment loophole. With other setup methods, this page is only accessible until after you've validated your app with their code snippets or imported users from a csv or 3rd party integrations. Gotta love loopholes, right?

![intercom4](/1.0/assets/img/guides/streaming/clickstream/intercom/intercom4.png)

<b>Step 3</b> Skip the Set up Intercom & Segment prompt and click on the gear wheel icon on the top right and then into the Integrations option in the dropdown.

![intercom5](/1.0/assets/img/guides/streaming/clickstream/intercom/intercom5.png)

From here you'll click on the 'API Keys' on the left hand panel to access your App Id and API Key.

![intercom6](/1.0/assets/img/guides/streaming/clickstream/intercom/intercom6.png)

<b>Step 4</b> Add your App ID and API Key into the Intercom connector on your Astronomer dashboard and give your new connection a unique name. Click 'Create Destination' and your pipeline will be activated.

![intercom7](/1.0/assets/img/guides/streaming/clickstream/intercom/intercom7.gif)

<b>Step 5</b> If you look back at your Intercom account, your events should begin to be trickling in. If you click on the 'People' icon on the top of your dashboard, you'll see 1 new user. That's you!

![intercom8](/1.0/assets/img/guides/streaming/clickstream/intercom/intercom8.png)

Click on that new user to see the history of events being recorded.

![intercom9](/1.0/assets/img/guides/streaming/clickstream/intercom/intercom9.png)
