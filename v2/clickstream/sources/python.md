---
title: Python
sidebar: platform_sidebar
---

## Python

This library lets you record analytics data from your Python code. You can use this library in your web server controller code. It is high-performing in that it uses an internal queue to make 'identify' and 'track' calls non-blocking and fast. It also batches messages and flushes asynchronously to our servers.

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
analytics.source_id = ‘astronomer_source_id’
```

***Note**: You can find your source_id in the settings section of your Astronomer App.*

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
