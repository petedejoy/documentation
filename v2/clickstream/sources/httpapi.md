---
title: HTTP API
sidebar: platform_sidebar
---

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