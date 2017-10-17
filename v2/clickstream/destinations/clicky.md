---
title: Clicky
sidebar: platform_sidebar
---

## What is Clicky and how does it work?

Clicky is a real-time web analytics tool that supports user segmentation, allowing marketers to define and track customers based on unique constraints like user action, traffic source, location, or device. It enables an intuitive heatmap view so that users can analyze and discover where users are clicking on their website. It also allows on-site analytics to track total visitors on site, pages viewed, and user actions. 

Like Google Analytics, Clicky is geard toward optimizing traffic sources, content engagement, and conversions. Unlike Google Analytics, it allows you to attach personal user data like names and email addresses to your visitor data so you know more about who is on your site. Clicky operates through its own Javascript library, which can be added to your site by pasting a code snippet on all pages in your web app. Setting up custom goals and identifying users is more complex and requires code hooks for each action or attribute you need to track.

## Why send data to Clicky using Astronomer Clickstream?

Integrating Clicky with Astronomer clickstream avoids the painstaking process of installing the Clicky Javascript library on each page of your site. Once you enable Clicky in your Astronomer UI, this Javascript library will be automatically loaded into each page and you will begin collecting user information, including page views, traffic sources, device info, visitor locations, and times on page. 

## Getting Started with Clicky and Astronomer Clickstream

Astronomer Clickstream makes it easy to send your data to Clicky. Once you follow the steps below, your data will be routed through our platform and pushed to Clicky in the appropriate format. 

Once you've made an account with Clicky, you will land on a page outlining basic information. Click the blue 'Preferences' button on the right side of the main menu bar.

![clicky3](/1.0/assets/img/guides/streaming/clickstream/clicky/clicky3.png)

Your site ID will be at the top of this page. Copy this ID to your clipboard.

[clicky4](/1.0/assets/img/guides/streaming/clickstream/clicky/clicky4.png)

Paste this ID into the Astronomer UI to begin sending data to Clicky. Your pipeline will be activated once you click 'Create Destination.'



