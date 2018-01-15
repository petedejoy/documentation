---
title: Sources Overview
sidebar: platform_sidebar
---

## Client-side libraries

* [Javascript](../sources/analyticsjs.html)
* [Android](../sources/android.html)
* [iOS](../sources/ios.html)

## Server-side libraries

* [HTTP API](../sources/httpapi.html)
* [Java](../sources/java.html)
* [MeteorJS](../sources/meteorjs.html)
* [Node.js](../sources/nodejs.html)
* [.NET](../sources/net.html)
* [PHP](../sources/php.html)
* [Python](../sources/python.html)
* [Ruby](../sources/ruby.html)

> NOTE: Server-side ingestion allows you to send data to Astronomer directly from your application's server. We recommend using these sources only when client sources will not work, as client sources generally pass additional data about the user's browser and environment.  Use cases will include payment events, data that needs to be calculated from a database query, or sensitive information.

## Data Routing

We route all inbound data and translate it into a format that your destination of choice understands. You can see the sources that we currently support in the sidebar on the left hand side of the screen. If you don't see a source that you would like supported, send us an email at [humans@astronomer.io](mailto:humans@astronomer.io) to request.
