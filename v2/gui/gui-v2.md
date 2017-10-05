---
post_title: Astronomer GUI
nav_title: Astronomer GUI
---

## Adding a New Organization

Astronomer organizes all pipelines by organization. There is not currently a limit on how many organizations you can have in your account - it's purely a matter of organizational preference. The benefits of using organizations extend to user permissions, where user access can be scoped to the connections of only one or a few organizations.

To create a new organization, click on the Orange button to the left of your existing organization name. That will bring you to your Organizations page where you'll see a button with a plus icon and the words "New Org".

Click this button and input the title of the organization name you would like.

![Create Organization](/1.0/assets/img/guides/gui-v2/create-new-org.gif)

Click Create and you will be  you will be taken to the organization's dashboard to begin setting up your apps and destinations.

![Blank Dashboard](/1.0/assets/img/guides/gui-v2/blank-dashboard.png)

## Switching Between Organizations

To switch between organizations, you follow a similar pattern as creating a new organization. Click the small organge icon in the upper left of the screen that contains the first letter of your organization name.

![Select New Organization](/1.0/assets/img/guides/gui-v2/switch-org.gif)

## Managing Organizations

Right now, users can edit their organization settings in two ways:

* Change Organization Name
* Delete Organization

To get to the organization settings screen, navigate to your organization's dashboard and click the gear icon next to the organization name. From this overlay, select the "Settings" tab.

You will now be able to enter a new organization name in the name field, or select "Delete Organization", where you will be asked to confirm your deletion.

![Manage Organization](/1.0/assets/img/guides/gui-v2/manage-org.gif)

## Adding a New User

New users can be added via your Organization Management page (the gear wheel next to your organization name in the top left). When adding each new user, you will have the option to make them an admin or regular user of your organization.

When adding new users, keep in mind that they will only be added to the organization you are currently within. If you would like to add a user to another organization, you will need to navigate to that organization from the "All Organization". (See [Switching Between Organizations](gui-v2/#switching-between-organizations) for more detail.)

![Add New User](/1.0/assets/img/guides/gui-v2/new-user.gif)

## Adding a Source

From your main dashboard, select the "New Source" button. You will then be asked to select the type of source. Currently, you are only able to add Javascript, Server-Side, iOS, and Android clickstream collectors as Sources. For more information on setting these Sources up, please visit the documentation [Clickstream Collectors](/1.0/streaming/clickstream/collectors/).

Next you will be asked to give your app a name. This is how it will be visualized throughout the app, so be sure to pick a succinct, descriptive name.

If you are ready to integrate Astronomer into your source, copy the App ID and visit our docs here (Link Pending) to begin the process of generating and placing your tracking code.

Select "Save" and you will be returned to your organization dashboard.

![Add New Javascript App](/1.0/assets/img/guides/gui-v2/add-new-javascript-app.gif)

## Managing a Source

Right now, users can edit their source settings in two ways:

* Change Source Name
* Delete Source

To edit a source, navigate to your organization's dashboard and click on the desired source's icon.

From the side panel that opens, you will now be able to enter a new name for your source in the name field, copy your App Id, or select "Delete", where you will be asked to confirm your deletion.

If you made changes to the source name, click "Save" to confirm and return to the organization dashboard.

![App Settings](/1.0/assets/img/guides/gui-v2/app-settings.gif)


---

## Coming Soon

- adding-astronomer-to-your-source
- adding-a-destination
- managing-a-destination
- adding-connections
- managing-connections
- add-new-user
- managing-users
- forgot-passord
- advanced-monitoring
- turn-destinations-on-and-off
- monitor-your-events
