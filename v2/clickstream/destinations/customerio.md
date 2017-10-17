---
title: Customer.io
sidebar: platform_sidebar
---

## What is Customer.io and how does it work?

Customer.io is an automated email based on customer behavioral data. It maps this data, including any event names or properties, so that you can create any user segmentation. It also uses Shopify's open-source Liquid logic for powerful and robust email template and personalization options. 

There are a few ways that Customer.io works. The first is by integrating with a clickstream tool like Astronomer. The other ways involve copy and pasting your customer.io javascript snippet into the footer of your website and using client libraries. 

## Why send data to Customer.io using Astronomer Clickstream?

If you elect to use the Customer.io Javascript snippet, you'll need to manually identify logged in users and any information you know about them. After manually identifying these users, you will be able to email everyone who logs into your site. Customer.io also lacks a libraries for Java, iOS, Android, and OS X.

Integrating Customer.io with Astronomer Clickstream allows the customer data coming in from websites, servers, and mobile apps to be sent directly to Customer.io without any additional installation. We eliminate the need for you to manually identify all logged in users to use the tool.

## Getting Started with Customer.io and Astronomer Clickstream

To get started sending events to Customer.io, you're going to need your Site ID and your API Key.

Once you create a [Customer.io](customer.io) account, you'll be asked to create an organization.

![customerio1](/1.0/assets/img/guides/streaming/clickstream/customerio/customerio1.png)

You will find both your Site ID and API Key clearly presented and labeled once you click on the 'Integration' tab within the 'Configuration' section of the left hand menu.

![customerio2](/1.0/assets/img/guides/streaming/clickstream/customerio/customerio2.png)

Add your App ID into the Customer.io connector on your Astronomer dashboard and give your new connection a unique name. Click 'Create Destination' and your pipeline will be activated.

![customerio3](/1.0/assets/img/guides/streaming/clickstream/customerio/customerio3.gif)
