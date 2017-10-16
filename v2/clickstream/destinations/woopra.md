---
title: Woopra
sidebar: platform_sidebar
---
Astronomer Clickstream makes it easy to send your data to *Woopra*. Follow the steps below to route your data through our platform and push it to *Woopra* in the appropriate format. 

## Getting Started with Woopra and Astronomer Clickstream

### **Woopra-Side**
Once you create your account on the woopra [website](https://www.woopra.com/), add a new project with the domain of your website or app. 


![woopra1](https://docs.astronomer.io/docs//1.0/assets/img/guides/streaming/clickstream/woopra/woopra1.png)


### **Astronomer-Side**

Add your domain name into the Woopra connector on your Astronomer dashboard and give your new connection a unique name. 

Click `Create Destination` and your pipeline will be activated.

![woopra2](https://docs.astronomer.io/docs//1.0/assets/img/guides/streaming/clickstream/woopra/woopra2.gif)


### **The Pipeline.**

You'll now see your events trickling in on your Woopra account. If you click on the `People` icon on the left hand side of the dashboard, you'll see 1 new user. That's you!

Click on that new user to see the history of events being recorded.

![woopra3](https://docs.astronomer.io/docs//1.0/assets/img/guides/streaming/clickstream/woopra/woopra3.png)

## Beyond the Basics

### **Tying server side events to client side sessions**

Pass us the `wooTracker` value inside your cookie if you want your server side events to be seen as part of the same "source" or session as your client side events. 

To retrieve this value, input the following command: 

```
analytics.ready(function(){
  var woopraCookie = window.woopra.cookie;

  // pass this value to your server
});
```

From the server side, you can attach it to the `integrations.Woopra.cookie` property. Here's a Ruby example that will let Woopra know that this server side event is part of the same session as the client. 

```
Analytics.track(
    user_id: '019mr8mf4r',
    event: 'Purchased Item',
    properties: { revenue: 39.95, shipping: '2-day' },
    integrations: {
      Woopra: {
       cookie: <wooTracker value>
      }
    })
```


