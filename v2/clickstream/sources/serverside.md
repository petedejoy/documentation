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

For example, if your Source ID is `bXlhcHA6`, you'll need to encode `bXlhcHA6:`. The resut of this will be `Basic YlhsaGNIQTY6`. The complete authorization header would then be `Authorization: Basic YlhsaGNIQTY6`.

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

*Note that this package is not being actively developed or maintained by Astronomer. However, it is still functional. If you would like to contribute to the package, please submit a pull request or email pete@astronomer.io.*

If you're using the Meteor javascript app platform and haven't instrumented your app for user analytics yet, our [Meteor Package](https://atmospherejs.com/astronomerio/core) will instrument for you automatically!

*Note that, if you are using the package `percolatestudio:segment.io`, you will need to remove this before installing Astronomer. This packages sets a global `analytics` object and makes the package unfunctional. 
```
{
  "type": "info",
  "title": "Which user actions get tracked?",
  "body": "All of them! This is done by tracking all Meteor methods, route changes (flow-router and iron-router), and insertions into minimongo."
}
```

### Getting Started wtih MeteorJS

First, open your termal, cd to your app, and add the Astronomer package:
```
meteor add astronomerio:core
```

To configure your Meteor app, follow the steps below:
1. Copy this snippet:
```
{
  "public": {
    "astronomer": {
      "appId": "XXXXXXXXXXXXXXXXXXX",
      "disableUserTracking": true,
      "disableRouteTracking": true,
      "disableMethodTracking": true,
      "ignoreNotFoundWarning": false
    }
  }
}
```
2. Create a new file called `settings.json` at the root directory of your Meteor application and paste the above snippet into that file. If you already have a file under this name, simply add the snippet to it.

3. In your Astronomer UI, find your `Source ID` and copy it to your clipboard. Paste this value into the `appID` field in the snippet from step 1.

4. Restart your Meteor Application

### Additional MeteorJS Features

`disableUserTracking:` `true` or `false`: This tracks aliased users. 

`disableRouteTracking:` `true` or `false`: This sends a Page call as routing is engaged within your Meteor App.

`disableMethodTracking:` `true` or `false`: This sends a Track call as methods are engaged within your Meteor App.

`ignoreNotFoundWarning:` `true` or `false`: This prevents a warning from appearing in the console if there is no `Source ID`.

*Note that every integration you activate will require you to set up a separate account with sepcific keys or ids that let Astronomer know which account is yours*

To confirm that events are being sent, follow the setps below:
1. Check the web browser's javascript console for your app, make sure you see "Authenticating with https://app.astronomer.io:443" to ensure that your settings are correct.
2. Take some actions in your app (sign up, change routes).
3. Click on the 'Live Stream' tab to see what events are being received by Astronomer.
4. Go to the integrations that you've activated and check to see that events are being properly received on their end.

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
var Analytics = new analytics{'ASTRONOMER_APP_ID')}
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

Initialize the module with the Source ID found in the setting sections of your Astronomer account. Note that you are only required to do this intitialization once.
```
class_alias('Segment', 'analytics');
analytics::init("ASTRONOMER_APP_ID");
```

After this initialization, you have a ready-to-use instance with all calls built in. 
*Note: We've standardized to analytics.js. If you've used a tool like [Segment](https://segment.com/) in the past, you will find that instrumenting events in Astronomer works in the exact same way.*

### Calls in PHP

Check out our [Calls](../calls.md) section for information on when you should use each call. Below are some examples of how you'd call specific objects in PHP.

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

Inside your python app, set you Source ID inside an instance of the Analytics object.
```
import analytics
analytics.app_id = ‘astronomer_app_id’
```
*Note that you can find your app_id in the settings section of your Astronomer App.*

### Calls in Python

Check out our [Calls](../calls.md) section for information on when you should use each call. Below are some examples of how you'd call specific objects in Python.

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
  'name': 'Astronomer',
  'domain': 'Data Engineering Platform'
})
```

#### Alias
```
analytics.alias(previous_id, user_id)
```

## Ruby

This library lets you record analytics data from your Ruby code. You can use this library in your web server controller code. It is high-performing in that it uses an internal queue to make 'identify' and 'track' calls non-blocking and fast. It also batches messages and flushes aysynchronously to our servers.

Check out our `astronomer` [Ruby gem](https://rubygems.org/gems/astronomer/) to see the library.

### Getting Started with Ruby

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

Inside your Ruby application, you'll want to set your `Source ID` inside an instance of the Analytics object:
```
analytics = Segment::Analytics.new({
  app_id: 'YOUR_APP_ID'
})
```
*Note that you can find your `Source ID` in the settings section of your Astronomer App.*

### Calls in Ruby

Check out our [Calls](../calls.md) section for information on when you should use each call. Below are some examples of how you'd call specific objects in Ruby.

#### Identify
```
analytics.identify(
    user_id: '1234qwerty',
    traits: { email: "#{} user,email }", fingers: 10 },
    context: {ip: '0.0.0.0'})

)
```

#### Track
```
analytics.track(
    user_id: `1234qwerty`,
    event: 'Add to cart'
    properties: {price: 50.00, color, 'Medium'}
)
```

#### Page
```
analytics.page(
    user_id: user_id,
    category: Prod site
    name: 'Landing page'
    properties: { url: 'https://astronomer.io'}
)
```

#### Group
```
analytics.group(
    user_id: '1234qwerty'
    group_id: '10'
    traits: { name: 'Astronomer', description: 'Data Engineering Platform'}
)
```

#### Alias
```
analytics.alias(previous_id: 'previous id', user_id: 'new id')
```

## .NET

This library lets you record analytics data from your ASP.NET, C#, F#, and Visual Basic code. Just pop this library into your web server controller code and it will take care of hitting our servers so that we can route your data to an analytics service of your choice.

### Getting Started with .NET

#### Step 1

To start, you must install our client-side library, analytics.js, to your ASP.NET master page. Follow the steps outlined in our [analytics.js doc] (../analyticsjs.md) and place your snippet directly in your ASP.NET Site.master. This will allow you to use `page ` calls.

#### Step 2

Next, you'll want to instally our .net library to start using the `identify` and `track` calls. We reccomend using [NuGet](https://docs.microsoft.com/en-us/nuget/tools/package-manager-console) to do this. 
```
Install-Package Analytics
```
You can also doing this by navigating through Visual Studio: `Toola-->Library Package Manager-->Package Manager Console'

Now you need to iniitialize the .NET library so that it knows where to send data. Do this with your `Source ID`, which can be found in your Astronomer UI once you've created a server-side source. Then you can use the `Analytics` singleton in any controller you want:
```
<%@ Application Language="C#" %>
<%@ Import Namespace="ASP.NET_Example" %>
<%@ Import Namespace="System.Web.Optimization" %>
<%@ Import Namespace="System.Web.Routing" %>
<%@ Import Namespace="Astronomer" %>

<script runat="server">

    void Application_Start(object sender, EventArgs e)
    {
        RouteConfig.RegisterRoutes(RouteTable.Routes);
        BundleConfig.RegisterBundles(BundleTable.Bundles);
        // this is your project's Source ID
        Astronomer.Analytics.Initialize("1234qwerty");
    }

</script>
```
Now, initialize the project:
```
Analytics.Initialize("YOUR_SOURCE_ID");
```
You will only need to perform this initialization once.

### Calls in .NET

Check out our [Calls](../calls.md) section for information on when you should use each call. Below are some examples of how you'd call specific objects in .NET.

#### Identify
```
Analytics.Client.Identify("1234qwerty", new Traits() {
    { "name", "#{ user.name }" },
    { "email", "#{ user.email }" },
    { "fingers", 10 }
});
```

#### Track
```
Analytics.Client.Track("1234qwerty", "Add to Cart", new Properties() {
    { "price", 50.00 },
    { "size", "Medium" }
});
```

#### Page
```
Analytics.Client.Page("1234qwerty", "Login", new Properties() {
    { "path", "/login" },
    { "title", "Astronomer Login" }
});
```

#### Group
```
Analytics.Client.Group("userId", "groupId", new Traits() {
    { "name", "Astronomer },
    { "website", "www.astronomer.io" }
});
```

#### Alias
```
Analytics.Client.Alias("previousId", "userId")
```