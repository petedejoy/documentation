---
title: Lytics
sidebar: platform_sidebar
---
Astronomer Clickstream makes it easy to send your data to Lytics. Once you follow the steps below, your data will be routed through our platform and pushed to Lytics in the appropriate format. 

## What is Lytics and how does it work?

Lytics is a marketing analytics platform that crawls website text and images. In doing that, it automates digital catalogue and scoring of web content so that marketers can monitor and identify the most popular content, intensity of user engagement, and likelihood of user return. It also enables drag-and-drop segmentation, allowing teams to target customers based on channel, revenue, growth, or at-risk status.Lytics independently integrates with more than 65 popular platforms like Twitter, AdRoll, and Google Ads. It also allows marketers to provide a personalized help desk and in-app messages.

Lytics collects its data from a Javascript library that you'll need to load on all pages of your site. The most important data it uses has to do with user information like name and email, which is used to both power the mesaging features and ensure you're not asking already-known users to opt in. All data is collected using the Lytics API, which will require a developer to learn and implement its methods and data structure.

## Why send data to Lytics using Astronomer Clickstream?

Integrating Lytics with Astronomer Clickstream means that you won't have to write any custom code on top of your standard Astronomer integration. Enabling Lytics in your Astronomer UI automatically loads the Javascript library onto your site without making code changes.

Astronomer Clickstream automatically maps `page`, `identify`, and `track` calls directly to Lytics in the format it understands. Lytics can then use that customer data to power its implementations. You are also able to easily  push data from mobile apps or servers to Lytics using Astronomer Clickstream.

## Getting Started with Lytics and Astronomer Clickstream

To get started sending events to Lytics, you're only going to need your Data API Key and Account ID.

After you create your Lytics account, you'll be dropped into a welcome page asking you connect up some integrations.

![lytics1](../../../images/lytics1.png)

We're not on that page yet (if you work at Lytics, we'd love to join the ranks!) but here's how you connect us up. Click on your email address at the top right, and click on the 'Manage Accounts' option. There you'll see your ID on the left hand side of your account and your Data API on the right.

![lytics2](../../../images/lytics2.png)

Add your Account ID and Data API into the Lytics connector on your Astronomer dashboard and give your new connection a unique name. Click 'Create Destination' and your pipeline will be activated.

![lytics3](../../../images/lytics3.gif)


 Lytics updates their incoming data stream every two minutes so your events won't show up immediately, but give it a couple of minutes. You can check back in on the status of your project by going to the 'Data' tab at the top.

![lytics4](../../../images/lytics4.png)

