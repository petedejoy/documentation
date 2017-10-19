---
title: .NET
sidebar: platform_sidebar
---

## .NET

This library lets you record analytics data from your ASP.NET, C#, F#, and Visual Basic code. Just pop this library into your web server controller code and it will take care of hitting our servers so that we can route your data to an analytics service of your choice.

### Getting Started with .NET

#### Step 1

To start, you must install our client-side library, analytics.js, to your ASP.NET master page. Follow the steps outlined in our [analytics.js doc](../analyticsjs.md) and place your snippet directly in your ASP.NET Site.master. This will allow you to use `page ` calls.

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