---
title: Hubspot
sidebar: platform_sidebar
---
#NOT DONE
To get started sending events to [Hubspot](http://www.hubspot.com), all you'll need is your Portal ID and API, both of which can be found shortly after you create an account.

**Getting Credentials from Hubspot:**

<b>Step 1 -</b> Create a Hubspot account via their [website](http://www.hubspot.com). After you go through the initial onboarding, you'll want to click on your account tab on the top right of the window. **NOTE**: You might notice something called a "Hub ID" next to the account tab. That's the ID you'll need for the Atronomer integration. You're halfway there already!

**Go to Settings->Configuration**

<b>Step 2 -</b>Select the "Integrations" option and you'll be brought to a screen that looks like the below. Next, you'll want to click the option on the left hand menu labeled "Get your HubSpot API Key."

![hubspot1](/1.0/assets/img/guides/streaming/clickstream/hubspot/hubspot1.png)


<b>Step 3 -</b> On this page you'll see a large blue button appropriately labeled 'Generate New Key.' Wanna guess what button you need to press? Yep.

![hubspot2](/1.0/assets/img/guides/streaming/clickstream/hubspot/hubspot2.png)


One handy feature of Hubspot is the full API Key History, including creation, viewing, and deactivation dates.

![hubspot3](/1.0/assets/img/guides/streaming/clickstream/hubspot/hubspot3.png)

**Set Up the Hubspot Configuration in your Astronomer App**

<b>Step 4 -</b> Add both of these credentials (your Portal ID and your newly created API Key) and give your new connection a unique name. Click 'Create Destination' and your pipeline will be activated.

Overview Tab:
*Portal Id* (required)(text field)
Copy your portal id and past it here.

*API Key* (required)(text field)
Copy the 32-character API Key you generated from Hubspot, and paste it here.

![hubspot4](/1.0/assets/img/guides/streaming/clickstream/hubspot/hubspot4.gif)