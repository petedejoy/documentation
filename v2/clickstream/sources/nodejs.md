---
title: Node.js
sidebar: platform_sidebar
---

## Node.js

This library lets you record all analytics data from your node code. You can check out it's open source code [here] (https://github.com/segmentio/analytics-node).You can use this library in your web server controller code. It is high-performing in that it uses an internal queue to make 'identify' and 'track' calls non-blocking and fast. It also batches messages and flushes aysynchronously to our servers.

### Getting Started with Node.js

#### Step 1
Install the astronomer npm module.
```
npm install --save astronomer
```

#### Step 2
Initialize this package with the Source ID found in the settings section of your Astronomer account.
```
var Analytics = import('astronomer');
var Analytics = new analytics{'ASTRONOMER_SOURCE_ID')}
```

#### Step 3

Set your event methods (identify, track, etc.) throughout your app. 
*Note: We've standardized to analytics.js. If you've used a tool like [Segment](https://segment.com/) in the past, you will find that instrumenting events in Astronomer works in the exact same way.*

### Calls in Node.js

Check out our [Calls](../calls.md) section for information on when you should use each call. Below are some examples of how you'd call specific objects in node.js.

#### Identify

```
{
  "codes": [
    {
      "code": "analytics.identify({
          \n  userId: '1234qwerty',
          \n  traits: {
              \n    name: 'Arthur Dent',
              \n    email: 'earthling1@hitchhikersguide.com',
              \n    hasTowel: True,\n  }\n});",
      "language": "javascript"
    }
  ]
}
```

#### Track

```
{
  "codes": [
    {
      "code": "analytics.track({
          \n  userId: '1234qwerty',
          \n  event: 'Added File',
          \n  properties: {
              \n    fileTitle: 'Life, the Universe, and Everything',
              \n    fileSize: '42kb',
              \n    fileType: 'PDF'\n  }\n});",
      "language": "javascript"
    }
  ]
}
```

#### Page

```
analytics.page({
  userId: '1234qwerty',
  section: 'Blog',
  name: '10 Questions with Marvin, the clinically depressed robot',
  properties: {
    referrer: 'http://reddit.com/r/AMA'
  }
})
```

#### Group

```
analytics.group({
  userId: '1234qwerty',
  groupId: '5678dvorak',
  traits: {
    name: "The Hitchhikers",
    relativePosition: "[39.1000° N, 84.5167° W]\""
  }
})
```

#### Alias

```
analytics.alias({
  previousId: anonymous_id,
  userId: assigned_id_or_email
});
```
