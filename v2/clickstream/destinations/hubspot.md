---
title: Hubspot
sidebar: platform_sidebar
---
Astronomer Clickstream makes it easy to send your data to Hubspot. Once you follow the steps below, your data will be routed through our platform and pushed to Hubspot in the appropriate format. 

## What is Hubspot and how does it work?

Hubspot is an inbound marketing and sales software that helps companies attract visitors, convert leads, and close customers. 

The marketing automation platform includes everything from a landing page builder to SEO tools as well as a repository for managing specific campaign leads.

Hubspot also monitors social media engagement and tracks the ROI of advertising on major social media platforms, equipping your team with the data you need to make strategic marketing decisions and investments. 

Often used in tandem with another CRM like Salesforce, Hubspot integrates multiple platforms into source of truth. 

[Learn more about Hubspot](https://www.hubspot.com/)

## Why send data to Hubspot using Astronomer Clickstream?

Using Hubspot with Astronomer Clickstream allows you to automatically keep all of the customer data in your HubSpot account up-to-date and accurate, rather than spending valuable time uploading lists or relying on lead forms to capture contacts. By enabling the Hubspot integration in your Astronomer UI, you can keep all customer data records synced and up-to-date accross multiple systems in real time.

## Getting Started with Hubspot and Astronomer Clickstream

To get started sending events to [Hubspot](http://www.hubspot.com), all you'll need is your Portal ID and API, both of which can be found shortly after you create an account.

### Hubspot Side

Create a Hubspot account via their [website](http://www.hubspot.com). 

After you go through the initial onboarding, click on your account tab on the top right of the window. Note that you might notice something called a `Hub ID` next to the account tab. That's the ID you'll need for the Atronomer integration.

Now, go to `Settings` -> `Configuration`

Select the `Integrations` option and you'll be brought to a screen that looks like the one below. Next, click the option on the left hand menu labeled `Get your HubSpot API Key.`

![hubspot1](../../../images/hubspot1.png)

On this page you'll see a large blue button appropriately labeled `Generate New Key.` 

![hubspot2](../../../images/hubspot2.png)

One handy feature of Hubspot is the full API Key History, including creation, viewing, and deactivation dates.

![hubspot3](../../../images/hubspot3.png)

### Astronomer Side

Now, all you have to do is add both of these credentials (your Portal ID and your newly created API Key) into the Astronomer UI and give your new connection a unique name. 

![hubspot4](../../../images/hubspot4.gif)

Once you do that, just click `Create Destination` to activate your pipeline.