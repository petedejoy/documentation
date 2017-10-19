---
title: Ruby
sidebar: platform_sidebar
---

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
