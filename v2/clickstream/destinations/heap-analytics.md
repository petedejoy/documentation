---
title: Heap Analytics
sidebar: platform_sidebar
---

Astronomer Clickstream makes it easy to send your data to Heap. Once you follow the steps below, your data will be routed through our platform and pushed to Heap in the appropriate format. 

## What is Heap and how does it work?

Heap is a mobile and web analytics tool. It automatically captures every user action in your web or mobile app and lets you analyze it retroactively. It also tracks real-time and retroactive analytics to create reports based on events like clicks, taps, swipes, and more. Designed with marketers in mind, Heap supports point-and-click web and mobile tag creation so that users can define custom events without coding. 

Heap is powered by a Javascript library that you'll need to install on every page that you want to track. This library collects all actions and some basic contextual information, including CSS selectors and text on your links and buttons. If you want to go deeper than this basic information, you'll need to write custom code into your site using the Heap Javascript API. Similarly, if you want to record events that happen when users aren't actively on your site, such as when someone makes a payment or opens an email, you'll need to write code to pull that data and send it to Heap's API. 

## Why send data to Heap using Astronomer Clickstream?

Integrating Heap with Astronomer Clickstream allows you to collect valuable data without manually adding the Heap code snippet into your site header. Instead, you simply enable the Heap destination in your UI and Astronomer will take care of translating user traits and sending them to Heap. 

## Getting Started with Heap and Astronomer Clickstream

Once you create a Heap account, a page will load suggesting you install Heap into your app. If you're using Astronomer for a web app, this isn't necessary as you'll be able to copy over the App ID into your Astronomer account. Your App ID will be located at the end of the javascript snippet they provide with the 'heap.load()' function.

![heap-analytics1](../../../images/heap-analytics1.png)

It's important to note here that Heap automatically sets you up with a Development and Production project when you create an account. Make sure you're copying over the right ID as that will affect which project within Heap your data gets sent to.

![heap-analytics2](../../../images/heap-analytics2.png)

Add your App ID into the Heap connector on your Astronomer dashboard and give your new connection a unique name. Click 'Create Destination' and your pipeline will be activated.

![heap-analytics3](../../../images/heap-analytics3.gif)


When you return to your Heap account, you might get a message saying "There's no data here!" Be sure to check all locations, as your data might be in a different environment (i.e. development instead of production).

![heap-analytics4](../../../images/heap-analytics4.png)

You can see what specific events are coming in by going to the 'Events' page, located in the left-hand menu bar.

![heap-analytics5](../../../images/heap-analytics5.png)