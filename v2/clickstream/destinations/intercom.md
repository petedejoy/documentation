---
title: Intercom
sidebar: platform_sidebar
---

Astronomer Clickstream makes it easy to send your data to Intercom. Once you follow the steps below, your data will be routed through our platform and pushed to Intercom in the appropriate format. 

## Getting Started with Intercom and Astronomer Clickstream

To activate your pipeline and start sending events to Intercom, you'll need to (i) identify your App Id and API Key from Intercom and (ii) input your credentials the Astronomer's platform. 

### Identifying your App ID and API Key on Intercom.

Once you're on the [Get started with Intercom](http://www.intercom.io) page, you'll be asked if you want to either (i) integrate one of their libraries or (ii) import users from another service/csv.

![intercom1](../../../images/intercom1.png)

Click on `Integrate` and then `Segment` (You're still setting up Astronomer, don't worry).

![intercom2](../../../images/intercom2.png)

 Go ahead and click `Next` to continue the setup.

![intercom3](../../../images/intercom3.png)

This is where you'll actually create your account and get started using Intercom.

![intercom4](../../../images/intercom4.png)

Skip the `Set up Intercom & Segment` prompt and click on the gear wheel icon on the top right and then into the `Integrations` option in the dropdown.

![intercom5](../../../images/intercom5.png)

From here, click on the `API Keys` on the left hand panel to access your App Id and API Key. Your App ID will look something like: `9iefb489`

![intercom6](../../../images/intercom6.png)

### Astronomer Platform Set-Up. 

Enter your App ID and API Key into the Intercom connector on your Astronomer dashboard. 

Give your new connection a unique name. 

Click `Create Destination` to activate your pipeline. 

![intercom7](../../../images/intercom7.gif)

At this point, you'll see events coming in to your Intercom account. If you click on the `People` icon on the top of your dashboard, you'll see 1 new user. That's you!

![intercom8](../../../images/intercom8.png)

Click on that new user to see the history of events being recorded.

![intercom9](../../../images/intercom9.png)

## Additional Functionality

### Identify
What happens when you call Identify.

### Track
What happens when you call Track.

### Page
What happens when you call Page.

### Group
What happens when you call Group.

### Alias
What happens when you call Alias.

## Beyond the Basics and Things to Note

### Disassociating Users from a Company (server-side only)

You can disassociate a user from a company by passing in a field inside the `company` trait with `remove: true` in your `identify` calls.

### Identity verification plus filtering via Destinations Object 

If you're using Intercom identity verification AND the `selective destinations functionality`, the context object will look like this: 

```
{
     integrations: {
         All: false,
         Intercom: {
            user_hash: '<%= OpenSSL::HMAC.hexdigest("sha256", "YOUR_INTERCOM_APP_SECRET", current_user.id) %>'
         }
     }
}
```

### Unsubscribe Users

With Astronomer Clickstream, you can unsubscribe users from email by setting a flag from `server side` libraries `unsubscribedFromEmails`, inside `context` object. 

`node.js` example: 

```
analytics.identify({
  userId: '4832094283057439285723523452345',
  anonymousId:'43254364571',
  context:{
    Intercom: { unsubscribedFromEmails: true }
  },
  traits: {
    firstName: 'John ',
    lastName: 'Jacob',
    email: 'jingleheimer@schmidt.com'
  }
});
```
*Note: This will only work from server side libraries and mobile, NOT work for analytics.js*

