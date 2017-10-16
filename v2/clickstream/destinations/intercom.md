---
title: Intercom
sidebar: platform_sidebar
---

To get started sending events to Intercom, all you'll need is your App Id and API Key. Intercom typically blocks you from seeing your dashboard until you've sent events to them, but we'll show you how to get around that.

## Getting App ID and API Key on Intercom.

Once you're on the [Get started with Intercom](http://www.intercom.io) page, you'll be asked if you want to either (i) integrate one of their libraries or (ii) import users from another service/csv.

![intercom1](https://docs.astronomer.io/docs//1.0/assets/img/guides/streaming/clickstream/intercom/intercom1.png)

Click on `Integrate` and then `Segment` (You're still setting up Astronomer, don't worry).

![intercom2](https://docs.astronomer.io/docs//1.0/assets/img/guides/streaming/clickstream/intercom/intercom2.png)

 Once you get to this page, go ahead and click `Next` to continue the setup.

![intercom3](https://docs.astronomer.io/docs//1.0/assets/img/guides/streaming/clickstream/intercom/intercom3.png)

This is where you'll actually create your account and get started using Intercom.

![intercom4](https://docs.astronomer.io/docs//1.0/assets/img/guides/streaming/clickstream/intercom/intercom4.png)

Skip the `Set up Intercom & Segment` prompt and click on the gear wheel icon on the top right and then into the `Integrations` option in the dropdown.

![intercom5](https://docs.astronomer.io/docs//1.0/assets/img/guides/streaming/clickstream/intercom/intercom5.png)

From here you'll click on the `API Keys` on the left hand panel to access your App Id and API Key.

![intercom6](https://docs.astronomer.io/docs//1.0/assets/img/guides/streaming/clickstream/intercom/intercom6.png)

## Kicking off Intercom with Astronomer. 

Enter your App ID and API Key into the Intercom connector on your Astronomer dashboard. 

Give your new connection a unique name. 

Click `Create Destination` to activate your pipeline.

![intercom7](https://docs.astronomer.io/docs//1.0/assets/img/guides/streaming/clickstream/intercom/intercom7.gif)

At this point, you'll see events coming in to your Intercom account. If you click on the `People` icon on the top of your dashboard, you'll see 1 new user. That's you!

![intercom8](https://docs.astronomer.io/docs//1.0/assets/img/guides/streaming/clickstream/intercom/intercom8.png)

Click on that new user to see the history of events being recorded.

![intercom9](https://docs.astronomer.io/docs//1.0/assets/img/guides/streaming/clickstream/intercom/intercom9.png)
