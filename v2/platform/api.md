---
post_title: Houston API
nav_title: Houston API
search: exclude
---

# Astronomer's Public API: Houston

Houston is a GraphQL API (utilizing Apollo) that allows interaction with the Astronomer Data Engineering Platform. Named after NASA’s Johnson Space Center in Houston, it provides direct communication and orchestration over our platform services.

We are currently in the Alpha stage of this project, so please expect changes to available queries, mutations, and their responses as we continue to develop this project.

We recommend using these projects while connecting to GraphQL:
* Client-side: [Apollo GraphQL](http://dev.apollodata.com/) 
* Node.js: [graphql-request](https://github.com/graphcool/graphql-request)

## Authentication

### JSON Web Tokens

JSON Web Tokens (JWT) encrypt important user session data in a way for our system to validate into a string that you can pass with every request. These tokens are set to expire on our system 24 hours after they are created.

#### Requesting JWT Access

In order to generate a JWT, you will first need a user account with Astronomer. Once you have a user account, the follow mutation (updated with your email, as the username, and password) will respond with your Token string for you to pass to our API.

```
mutation createToken{
  createToken(username:"someone@somewhere.com", password:"password"){
    success
    message
    token
    decoded {
      id
    }
  }
}
```

### Gaining Access to the Public API

#### Using a JWT

Once you have created a JSON Web Token, you need to embed it in the header of each request as authorization. Additionally, any operation to edit an Organization or any Connection or pipeline that an Organization controls will require that Organization’s ID in the header of your request as well, under organization.

JWT will expire after 24 hours. Once it is expired, you will need to generate a new JWT and replace the expired one with it.

#### Using an API Key

We’re working to provide trusted partners with API Keys that provide access to the Public API and do not self-expire. Stay tuned for updates, or send us a note at support@astronomer.io if you would like to be notified when this feature is made available.

## Data Models

### Users and Organizations

In order to access and control pipelines in the Astronomer platform, we give control of these operations to `Organizations`. `Users` are added to `Organizations` in order to utilize the org's control over those pipelines. Once an person is added to an `Organization`, they are titled either `Owner` or `User`.

Organization `Owners` have full read/write control over everything linked to that Organization, from editing pipelines to expanding User permissions. You can consider this role as having administrative privileges for this Organization.

Organization `Users` have specific read/write control over pipelines linked to that Organization, however cannot read the contents of Connections and cannot change access of other Users to their Organization.

#### Creating and Editing Users

Creating a new User - User accounts are tied to a specific email address and have to be confirmed via a link that is emailed to that account. We have two operations to create a User Account, Self Signup and Auto Signup. Self Signup assumes that you have both an email address and password that you want to configure. Auto Signup assumes you only have the email address for the account you want to configure, but the email account holder will need to set up their own password.

To create a new user account with the API, use the createNewUser mutation, you can use example below. Note: The profile argument is optional, however email and password are required.

mutation {
  createNewUser(
    email: "someone.new@somewhere.com"
    password: "password_string"
    profile: {
      {
        firstName: "Someone",
        lastName: "New",
        company: "My Company"
      }
    }
  ) {
    success
    message
    token
    decoded {
      id
    }
  }
}
There is no direct access to Auto Signup a user from the API, however it will be automatically triggered when adding a user to your Organization that does not have an Astronomer User account. See Editing Organization Users below to learn more.

#### Editing a User’s Account - (coming soon) Editing Organization Users - (coming soon)

#### Creating and Editing Organizations

In order to create any pipelines, you must first create an Organization to link those pipelines to. The User who creates and Organization is automatically given the Organization Owner role for that Organization, giving them access to all possible functionality.

Below is the mutation to create a new Organization:

createOrganization(
    name: "Human-friendly Organization Name"
    userId: "123456"
  ) {
    success
    message
    id
  }

### Clickstream Pipelines

Stream (or Clickstream) Pipelines focus on extracting or loading events in as close to real-time as possible.

#### Sources and Applications

Representing the source of your streaming events, we currently support for the platforms analytics.js, server, analytics-android and analytics-ios. The SDKs we offer for those platforms forward events to our Clickstream API to be ingested and distributed by our system. These Sources are grouped under an Organization, to allow you and other contributers that you specify to have access to view and/or edit them.

Upon Source creation, a 21 character long unique ID is generated to identify your Application within our system and to ensure your events are routed to the correct Destinations.

Below is the mutation to generate a Clickstream Source within our system:

mutation {
  createApplication(
      name: "Human-friendly Source Name",
      platform: "analytics.js",
      orgId: "1234567890"
    ) {
      success
      message
      id
    }
}
#### Destinations and Integrations

To find how to build the form for a Clickstream Pipeline, you want to query against clickstreamPrototypes. Within that response is a connectionPrototye and configPrototype array that list all the fields can use to configure a destination.

propertyName : Key for these values within a clickstreamConfig label : Human-friendly name for the field type : The form field to display. Some of these are standard (input, boolean, number) and others are more abstract (array, boolean, map). (expansion on all types to follow)

As of right now, the connection part has to be saved separately before you sane the configuration, as the Id for the connection will be referenced within the configuration. This allows you to reuse the connection for multiple configurations that are for the same platform for the tradeoff of having to make multiple requests to save them both initially.

Here is an example of the two mutations needed to set up a brand new clickstream destination

mutation {
  createConnection(
    integrationCode: "acquisio",
    details: {
      apiKey: "123"
    }
    name: "Friendly Connection Name"
    orgId: "1234567890"
    connectionPrototypeId: "123"
  ) {
    success
    message
    id
  }
}

mutation {
  createIntegration(
    appId: "456"
    integrationCode: "acquisio"
    configPayload:  {
          "events" : [
              "fvsbvsdfbsdfb"
          ]
    }
    connectionId: "123"
    name: "Friendly Application Name"
  ) {
    success
    message
    id
  }
}
### Query & Mutation Response

#### Query Response

Queries typically respond as an array of objects, even if the arguments you pass would limit the response to a single object. For instance, the query organizations will return an array with a single object if you search by orgId, but possibly multiple objects if you search by userId. This is standard due to two reasons: to (coming soon)

#### Mutation Response

Mutations typically respond with a statusMessage object to alert you on if the mutation you triggered was successful or not. This contains:

* `success` : True or False response if the request was successful
* `message` : Human-friendly message on what happened
* `id` : For operations that create new data, the id of the created object will be returned
* `code` : (coming soon)

Actions to mutate data within Astronomer’s platform tend to follow a create** and update** pattern, where we separate out the functions to make a new object with the ability to change or delete it in order to have strict control over the permissions over data control. For example, anyone can run createOrganization and make a new Organization where they are the Owner. However, only Organization Owners can run updateOrganization that allows for adding/removing users, updating Organization details, or deleting an Organization.

#### Error Response

(coming soon)


## Developer Tools



