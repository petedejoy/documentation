---
title: Calls
sidebar: platform_sidebar
---

Astronomer utilizes 6 different types of API calls to track users. Each call represents a distinct type of semantic information about a user and shares the same common fields. 

* Identify
* Track
* Page
* Group
* Alias

## Identify
The `identify` method is used to associate behavior and to record traits about your users. The call includes a unique User ID and any option traits you know about them (email, name, role, etc.) Implementing `identify` is one of the first steps to getting the most out of Astronomer Clickstream, keep reading to see how to do it...

We recommend calling `identify` at a couple of points:
  * After a user registers
  * After a user logs in
  * When a user updates their info
  * Upon loading any pages that are accessible by a logged-in user

Here's a sample `identify` snippet:
```
analytics.identify("1205119", {
    "name": "Dagny Smith",
    "email": "dagny@astronomer.io"
    "plan": "enterprise"
    });
```

And the resulting payload:
```
{
    "type": "identify",
    "traits": {
        "name": "Dagny Smith",
        "email": "dagny@astronomer.io"
        "plan": "enterprise",
    },
    "userID": "1205119"
}
```

As you can see, an `identify` call has 2 components beyond the common fields:

| Field               | Type   | Description                                                                                                      |
| ------------------- | ------ | ---------------------------------------------------------------------------------------------------------------- |
| `traits` (optional) | Object | Dictionary of user traits like `name` or `email`                                                                 |
| `userID` (required) | String | Unique identifier for the user in your database. Either a `userID` or an `anonymousID` is required for this call |

### Anonymous and User ID's
For cases where you don't actually know who the user is but you still want to be able to associate them to traits, events or page views, you should use an Anonymous ID. 

The Anonynymous ID can really be any pseudo-unique identifier. Feel free to use any readily available identifier or generate a new random one. [UUIDs](https://en.wikipedia.org/wiki/Universally_unique_identifier) work great.

**Note** Our web and mobile libraries automatically use Anonymous IDs to keep track of users asso no need to worry about them when using those libraries.

User IDs are a more permanent and consistent identifier and we recommend including them in your `identify` calls as often as possible. You are most likely already using a unique identifier to recognize a user in your own database - this identifier is a great `UserID`.

Also, we recommend using something like a database ID over something like an email address or a username as they are more robust and consistent. If you want to track information like email addresses or usernames, send them through as `traits` instead.

### Traits
In an `identify` call, traits are pieces of information that you know about a user. Traits can really be anything - from email addresses to age to A/B test variations. The world is your oyster!

## Track 
To record any actions your users perform, along with properties that describe the action, you will want to use a `track` call. Each of these actions is known as an event, and each of these events has a name. Calling `track` is one of the first steps to getting the most out of Astronomer Clickstream, keep reading to see how to do it...

Here's a sample `track` call:
```
analytics.track("Viewed Product", {
  "product": "Cat Feather Toy",
  "model_number": "B001BOVEU4",
  "price": "9.99"
});
```

That sample call would yield the following payload:
```
{
    "type":  "track",
    "event": "Viewed Product",
    "properties": {
        "model_number": "B001BOVEU4"
        "price": "9.99"
    }
}
```
As you can see, a `track` call has 2 components beyond the common fields: 

| Field                   | Type   | Description                                                           |
| ----------------------- | ------ | --------------------------------------------------------------------- |
| `event` (required)      | String | Name of the action that a user has performed                          |
| `properties` (optional) | String | Dictionary of properties of the event, like `model_number` or `price` |

### Properties
Properties are extra bits of information that you can tie to the events you track and can really be anything. We recommend sending properties as often as possible to give you a more complete picture of what your users are doing!

## Page
The `page` call allows you to record whenever a user sees a page of your webiste, along with any optional properties you want to include about the page. Calling `page` or `screen` is one of the first steps to getting the most out of Astronomer Clickstream, keep reading to see how to do it...

**Important** In the `analytics.js` snippet, a `page` call is included by default (just after the `analytics.load`). We do this because this method needs to be called at least once per page load. You have the option of sprucing up the call with a `name` or `properties` and can call it multiple times if you have a single-page application. 

Here's a sample `page` call:
```
analytics.page("Home")
```

And, here's the corresponding payload:
```
{
    "type": "page",
    "name": "Home",
    "properties": {
        "title": "Astronomer: The Platform for Data Engineering",
        "url": "https://ww.astronomer.io"
    }
}
```
As you can see, a `page` call has 2 components beyond the common fields: 

| Field                   | Type   | Description                                                           |
| ----------------------- | ------ | --------------------------------------------------------------------- |
| `name` (optional)       | String | Name of the page                                                      |
| `properties` (optional) | String | Dictionary of properties of the page, like `url` or `referrer` |

### Properties
Properties are extra bits of information that you can tie to the pages you track and can really be anything. We recommend sending properties as often as possible to give you a more complete picture of what your users are doing!

**Note** In analytics.js, we automatically send the following properties: `title`, `path`, `url`, `referrer`, and `search`.

## Group
Use the `group` call when you want to associate an individual user with a group - a company, organization, account, team, etc.

While a user can be in more than one group, not all platforms support multiple groups. This method also lets you record custom traits about the group. 

Calling `group` is slightly more advanced than `identify`, `track`, or `page` but it's pretty useful if you have accounts with multiple users. 

Here's a sample `group` call:
```
analytics.group("ak9g2hgpcf",{
    "name": "Astronomer",
    "industry": "Technology",
    "employees": "48"
});
```

And, the corresponding payload:
```
{
    "type": "Group",
    "groupID": "ak9g2hgpcf",
    "traits": {
        "name": "Astronomer",
        "industry": "Technology",
        "employees": "48"
    }
}
```
As you can see, a `group` call has 2 components beyond the common fields: 

| Field               | Type   | Description                                                       |
| ------------------- | ------ | ----------------------------------------------------------------- |
| `groupID` (required)| String | Name of the page                                                  |
| `traits` (optional) | String | Dictionary of traits of the group, like `industry` or `employees` |

### Group ID
A Group ID is the unique identifier by which you recognize a group in your database. 

### Traits
Traits are extra bits of information that you can tie to the pages you track and can really be anything.

## Alias
The `alias` method is used to merge two user identities, effectively connecting two sets of user data as one. Calling `alias` is slightly more advanced than `identify`, `track`, or `page` but it's required to manage user identities successfully in some of our destinations. 
