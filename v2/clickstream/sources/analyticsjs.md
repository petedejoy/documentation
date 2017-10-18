---
title: Source - Analytics.js
sidebar: platform_sidebar
---
## Getting Started with Astronomer Clickstream - Website

Using our analytics.js library, you can start sending customer data directly from your website to Astronomer. Accessing this user data will yield rich, actionable insights, and it only takes a few minutes to get set up!

### Create a Client-Side Source in the Astronomer UI

After logging in with your Astronomer credentials, add a new `Source → Client-Side`. Give your source a friendly name and copy that `Source ID` for the next step.

### Copy & Paste the Snippet

Next, you’ll need to copy and paste the snippet below into the <head> of your website.

```javascript
<script type="text/javascript">
  !function(){var analytics=window.analytics=window.analytics||[];if(!analytics.initialize)if(analytics.invoked)window.console&&console.error&&console.error("Astronomer snippet included twice.");else{analytics.invoked=!0;analytics.methods=["trackSubmit","trackClick","trackLink","trackForm","pageview","identify","reset","group","track","ready","alias","page","once","off","on"];analytics.factory=function(t){return function(){var e=Array.prototype.slice.call(arguments);e.unshift(t);analytics.push(e);return analytics}};for(var t=0;t<analytics.methods.length;t++){var e=analytics.methods[t];analytics[e]=analytics.factory(e)}analytics.load=function(t){var e=document.createElement("script");e.type="text/javascript";e.async=!0;e.src=("https:"===document.location.protocol?"https://":"http://")+"cdn.astronomer.io/analytics.js/v1/"+t+"/analytics.min.js";var n=document.getElementsByTagName("script")[0];n.parentNode.insertBefore(e,n)};analytics.SNIPPET_VERSION="3.1.0";
  analytics.load("YOUR_APP_ID");
  analytics.page()
  }}();
</script>
```

When you paste the snippet, replace ``"YOUR_APP_ID"`` with the `Source ID` for this particular project.

As soon as this snippet is running on your site, you can begin experimenting with destinations. Click back to Astronomer Clickstream UI and start adding destinations to the source you just configured.

To test your newly configured source, trigger some events on your website and look for them in the Monitoring Overview & Logs.

*Note: You will want to remove any other native 3rd party destination code that you may already have on your website. Skipping this step could cause issues if you turn on those same destinations (e.g. Mixpanel, Google Analytics, Amplitude, etc.) through Astronomer.*

If you are just looking for basic clickstream functionality, you’re all done setting up! We recommend enabling a simple integration, like Google Analytics, to start analyzing your website’s data.

If you’d like to use any tool that deals with the identity of your users (e.g. Mixpanel), keep reading to learn how to use the `identify` call.

### Identify Your Users

The `identify` method helps you associate your users and their actions to a unique and recognizable `userID` and `traits`. We recommend using a backend template to insert an `identify` call directly into the footer of every page of your site where the user is logged in. That way, your users will always be identified, no matter what page they first land on.

`identify` follows this basic definition:

```
analytics.identify([userId], [traits], [options], [callback]);
```

For example, a simple `identify` looks something like this:

```
analytics.identify('123456', {
  name: 'Dagny',
  email: 'dagny@astronomer.io}'
  role: 'buyer'
});
```

You’re now set up to use any basic CRM! Go ahead and switch on a CRM, like Intercom, to start seeing your user data through Astronomer.

While `identify` is an extremely useful call for a lot of integrations, many other analytics tools go beyond just identifying users; they record the actions each user performs too. See below for how to get to an even more holistic event tracking analytics setup.

### Track Your Users’ Actions

To get to a more complete event tracking analytics setup, you can add a `track` call to your website. This will tell Astronomer which actions you are performing on your site. With `track`, each user action triggers an “event,” which can also have associated properties.

Setting up `track` is very similar to the process you just went through to set up an `identify`. Here’s the basic `track` definition:

```
analytics.track(event, [properties], [options], [callback]);
```

And, here’s an example of what a simple `track` might look like:

```
analytics.track('Viewed Product', {
  product: 'Cat Feather Toy',
  model_number: 'B001BOVEU4',
});
```

*Note: In order to use a `track` call, you must specify a name for the event you want to track whereas properties, options, and callback are all optional fields.*

A lot of analytics tools support custom event mapping so, with `track` implemented, you’ll be able to attribute events to your users and start targeting them in a more informed and relevant way.

Congratulations, you’ve now successfully installed website tracking with Astronomer Connect!

Now the fun begins: head back to our app, turn on some destinations, and hit your business with insightful user data!

