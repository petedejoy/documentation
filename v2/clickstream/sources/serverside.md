---
title: Server Side Sources
sidebar: platform_sidebar
---

# Getting Started with Server-Side Sources

Server-side ingestion allows you to send data to Astronomer directly from your servers. These sources should be used only when standard analytics.js will not work. Use cases will include payment events, data sets where accuracy is extremely important, dat d that needs to be calculated from a database query, or sensitive information.

We support a number of open source libraries, including:
* HTTP API
* MeteorJS
* Node.js
* PHP
* Python
* Ruby

## HTTP API

This library lets you record analytics data from any website or application. You can then route that data to any destination supported by our platform.

### Getting Started with HTTP API

#### Authentication

You'll need to supply your app_ID with each request using HTTP Basic Auth.

Basic Auth base64 encodes a 'username:password' and prepends it with the string 'Basic'. The native libraries should handle this for you, but if they do not you'll need to base64 encode a string in which the username is the app_ID and the password is empty.

For example, if your app_ID is `bXlhcHA6`, you'll need to encode `bXlhcHA6:`. The resut of this will be `Basic YlhsaGNIQTY6`. The complete authorization header would then be `Authorization: Basic YlhsaGNIQTY6`.

#### Content-Type

Make sure to set the content-type header to `application/json`.

### Calls in HTTP API

Check out our 'Calls' section for information on when you should use each call. Below are some examples of how you'd call specific objects in HTTP API.

#### Identify

Post `https://api.astronomer.io/v1/identify`
```
{
  'userId': '1234qwerty',
  'traits': {
    'name': 'Arthur Dent',
    'email': 'earthling1@hitchhikersguide.com',
    'hasTowel': True,
  }
  'timestamp': '2015-11-10T00:45:23.412Z'
}
```

#### Track

Post `https://api.astronomer.io/v1/track`
```
{
  'userId': '1234qwerty',
  'event': 'Added File',
  'properties': {
    'fileTitle': 'Life, the Universe, and Everything',
    'fileSize': '42kb',
    'fileType': 'PDF'
  },
  'timestamp': '2015-11-10T00:45:23.412Z'
}
```

#### Page

Post `https://api.astronomer.io/v1/page`
```
{
  'userId': '1234qwerty',
  'section': 'Blog',
  'name': '10 Questions with Marvin, the clinically depressed robot',
  'properties': {
    'referrer': 'http://reddit.com/r/AMA'
  }
}
```

#### Group

Post `https://api.astronomer.io/v1/group`
```
{
  'userId': '1234qwerty',
  'groupId': '5678dvorak',
  'traits': {
    'name': 'The Hitchhikers',
    'relativePosition': '[39.1000 N, 84.5167 W]'
    }
}
```

#### Alias

Post  `https://api.astronomer.io/v1/alias`
```
{
  "previousId": "anonymous_id",
  "userId": "assigned_id_or_email",
  "timestamp": "2015-11-10T00:45:23.412Z"
}
```

## MeteorJS



## Node.js

This library lets you record all analytics data from your node code. You can check out it's open source code [here] (https://github.com/segmentio/analytics-node).You can use this library in your web server controller code. It is high-performing in that it uses an internal queue to make 'identify' and 'track' calls non-blocking and fast. It also batches messages and flushes aysynchronously to our servers.

### Getting Started with Node.js

#### Step 1
Install the astronomer npm module.
```
npm install --save astronomer
```

#### Step 2
Initialize this package with teh App ID found in the settings section of your Astronomer account.
```
var Analytics = require('astronomer');
var Analytics = new analytics{'ASTRONOMER_APP_ID')}
```

#### Step 3

Set your event methods(identify, track, etc.) throughout your app. 
*Note: We've standardized to analytics.js. If you've used a tool like [Segment](https://segment.com/) in the past, you will find that instrumenting events in Astronomer works in the exact same way.*

### Calls in Node.js

Check out our 'Calls' section for information on when you should use each call. Below are some examples of how you'd call specific objects in node.js.

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

## PHP

This library lets you record analytics data from your PHP code. It is a little different than other server-side libraries in that PHP is a single-threaded language, meaning it only processes once language at a time. 

### Getting Started with PHP

#### Step 1

Clone the PHP integration into your application directory.
```
git clone https://github.com/astronomerio/analytics-php
```

#### Step 2

Add the following to your code to load in the library.
```
require_once(\"/path/to/analytics-php/lib/Segment.php\");
```

#### Step 3

Initialize the module with the App ID found in the setting sections of your Astronomer account. Note that you are only required to do this intitialization once.
```
class_alias('Segment', 'analytics');
analytics::init("ASTRONOMER_APP_ID");
```

After this initialization, you have a ready-to-use instance with all calls built in. 
*Note: We've standardized to analytics.js. If you've used a tool like [Segment](https://segment.com/) in the past, you will find that instrumenting events in Astronomer works in the exact same way.*

### Calls in PHP

Check out our 'Calls' section for information on when you should use each call. Below are some examples of how you'd call specific objects in PHP.

#### Identify
```
analytics::identify(array(
         "userId" => "1234qwerty",
         "traits" => array(
         "name" => "Arthur Dent",
         "email" => "earthling1@hitchhikersguide.com\",
         "hasTowel" => True,)
);
```

#### Track
```
analytics::track(array(
        "userId" => "1234qwerty",
        "event" => "Added File",
        "properties" => array(
        "fileTitle" => "Life, the Universe, and Everything\",
        "fileSize" => "42kb",
        "fileType" => "PDF")
        )
);
```

#### Page
```
analytics::page(array(
        "userId" => "1234qwerty",
        "section" => "Blog",
        "name" => "10 Questions with Marvin, the clinically depressed robot",
        "properties" => array(
        "referrer" => "http://reddit.com/r/AMA")
        )
);
```

#### Group
```
analytics::group(array(
        "userId" => "1234qwerty",
        "groupId" => "5678dvorak",
        "traits" => array(
        "name" => "The Hitchhikers",
        "relativePosition" => "[39.1000° N, 84.5167° W]")
        )
);
```

#### Alias
```
analytics::alias(array(
        "previousId" => "1ff049u10459u7",
        "userId" => "1234qwerty")
);
```


## Python

This library lets you record analytics data from your Python code. You can use this library in your web server controller code. It is high-performing in that it uses an internal queue to make 'identify' and 'track' calls non-blocking and fast. It also batches messages and flushes aysynchronously to our servers.

Visit the [Python Package Index (PyPI)] (https://pypi.python.org/pypi/astronomer-analytics) for the `astronomer-analytics` package details.

### Getting Started with Python

#### Step 1

Install `astronomer-analytics` using `pip`
```
pip install astronomer-analytics
```

#### Step 2

Inside your python app, set you app_id inside an instance of the Analytics object.
```
import analytics
analytics.app_id = ‘astronomer_app_id’
```
*Note that you can find your app_id in the settings section of your Astronomer App.*

### Calls in Python - NOT DONE

Check out our 'Calls' section for information on when you should use each call. Below are some examples of how you'd call specific objects in Python.

#### Identify
```
analytics.identify('userID' : '1234qwerty', {
    'name': 'Arthur Dent',
    'email': 'earthling1@hitchhikersguide.com',
    'friends': 100
})
```

#### Track
```
analytics.track('userID' : '1234qwerty', 'Signed Up')
```

#### Page
```
analytics.page('user_id', 'Docs', 'Python', {
  'url': 'http://astronomer.io'
})
```

#### Group
```
analytics.group('user_id', 'group_id', {
  'name': 'Initech',
  'domain': 'Accounting Software'
})
```


### Ruby - NOT DONE

This library lets you record analytics data from your Ruby code. You can use this library in your web server controller code. It is high-performing in that it uses an internal queue to make 'identify' and 'track' calls non-blocking and fast. It also batches messages and flushes aysynchronously to our servers.

Check out our `astronomer` [Ruby gem](https://rubygems.org/gems/astronomer/) to see the library.

#### Step 1

Install `astronomer` either:
* Directly into a Gemfile
```
gem 'astronomer', '~>2.0', '>= 2.0.14'
```
* Directly into environment gems
```
gem install astronomer
```

#### Step 2

Inside your Ruby application, you'll want to set your app_id inside an instance of the Analytics object:
```
analytics = Segment::Analytics.new({
  app_id: 'YOUR_APP_ID'
})
```
*Note that you can find your app_id in the settings section of your Astronomer App.*