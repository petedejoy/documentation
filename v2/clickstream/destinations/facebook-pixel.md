---
title: Facebook Pixel
sidebar: platform_sidebar
---
#NOT DONE

Astronomer Clickstream makes it easy to send your data to Facebook Pixel. Once you follow the steps below, your data will be routed through our platform and pushed to Facebook Pixel in the appropriate format. 

## What is Facebook Pixel and how does it work?

Facebook Pixel is an Ad system designed for conversion, tracking, and remarketing leads. It allows you to manage all of your ads from one platform and uses prospecting tools to target ads to lookalike audiences. By providing this dynamic service, Facebook Pixel allows marketers to optimize cross-platform ads for custom conversions and see when users viewed content, searched for a product, interacted with their wishlist, or added payment info.

Facebook Pixel uses Javascript Tag API to track audiences and custom user events like page visibility and page length. In order to be used, this Javascript library must be added to every page of your site. It has a standard set of natively-integrated events such as product views, adds to cart, and purchases. In turn, that event data allows you to create more targeted ads for your user base. While extremely extensible, each unique user event that you want to track will require custom code to be added to your site in order to populate dynamic data like product sku, name, and price from your database.

## Why send data to Facebook Pixel using Astronomer Clickstream?

With Astronomer Clickstream, you can use Facebook Pixel without installing their Javascript library on every page on your site. We also eliminate the need to write custom code to track user event data. Once your Facebook Pixel is routed through Astronomer, our platform translates page views and events into corresponding Facebook Pixel events.

## Getting Started with Facebook Pixel and Astronomer Clickstream


To get started using the Facebook Pixel, you will first need to create a Facebook for Business account and [follow the instructions](https://www.facebook.com/business/a/online-sales/custom-audiences-website) for creating a Pixel. You'll only create one pixel for your site (typically labeled with the name of your business). This pixel will [replace all the functionality](https://www.facebook.com/business/help/1686199411616919) previously given to Facebook Audiences and Facebook Conversions (as well as allowing some additional features, such as custom conversions.)

![facebook-pixel1](/1.0/assets/img/guides/streaming/clickstream/facebook-pixel/facebook-pixel1.png)

Next, you will need to identify your unique Facebook Pixel ID, which will be a 15 digit number that uniquely identifies both your site. Put your Facebook Pixel ID into your Astronomer account and give your new connection a unique name.

Click 'Create Destination' and your pipeline will be activated.

Facebook has nine [Standard Events](https://www.facebook.com/business/a/add-pixel-standard-events) which are predefined within the Facebook for Business platform. To connect your events to these predefined ones within Facebook, just input the name of the Astronomer event and choose the appropriate Standard Facebook Event that corresponds to it.

![facebook-pixel3](/1.0/assets/img/guides/streaming/clickstream/facebook-pixel/facebook-pixel3.gif)


If you are using the Facebook Pixel integration as a replacement for Conversion Pixels as well, put each Conversion Pixel ID into your Astronomer account next to the corresponding event in Astronomer that you've already set up. Make sure you include all capitals letters and spaces used in your event labels.

![facebook-pixel4](/1.0/assets/img/guides/streaming/clickstream/facebook-pixel/facebook-pixel4.gif)

