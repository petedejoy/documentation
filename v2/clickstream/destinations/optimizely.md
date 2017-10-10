---
title: Optimizely
sidebar: platform_sidebar
---

Our Optimizely connector allows you to send events directly into Optimizely.  From there, you can record your Optimizely experiments or campaigns back into Astronomer, enabling you to analyze Optimizely data inside any other enabled tools within your Astronomer application.

This connector supports either Classic, Optimizely X, or both.

### Note: The Optimizely `<script>` tag needs to be on the page right away (Astronomer can’t load its client side library for you). In order to broadcast events, you MUST embed the Optimizely `<script>` tag in the `<head>` element on your page BEFORE the Astronomer snippet! 
See [this instructional video by Optimizely](https://help.optimizely.com/Set_Up_Optimizely/Implement_the_snippet_for_Optimizely_Classic) to find and embed their JavaScript snippet.  You'll want to include this snippet on every page you want to run experiments on (and remember, BEFORE the Astronomer snippet!). This connector supports client-side analytics.js (no server-side, iOS, or Android analytics).

### Step 1:
Create an [Optimizely](https://www.optimizely.com/) account, retreive your [JavaScript snippet](https://help.optimizely.com/Set_Up_Optimizely/Implement_the_snippet_for_Optimizely_Classic), and embed the snippet in each page that you want to run experiments on (remember, BEFORE the Astronomer snippet!).

### Step 2:
Within your Astronomer configuration, add the Optimizely destination connector, and give your new connection a unique name. 

Then, configure the Optimizely connector to support your desired features.  The steps for this will vary depending on whether you're deploying [Optimizely Classic](https://help.optimizely.com/Measure_success%3A_Track_visitor_behaviors/Custom_event_goals_in_Optimizely_Classic) or [Optimizely X Web](https://help.optimizely.com/Build_Campaigns_and_Experiments/Custom_events_in_Optimizely_X).

When you're done, check the boxes next to those features inside the Astronomer UI.  Those options are:

#### Send experiment data to other tools (as an identify call)
This is not recommended because if you’re running lots of experiments, this could lead to lots of unwanted properties in end tools, in addition to unwanted columns in Astronomer-connected databases.

#### Track Named Pages
This will track events to Optimizely for page method calls that have a name associated with them. 

#### Track Categorized Pages
This tracks events to Optimizely for page calls that have a category associated with them. 

#### Send experiment data to other tools (as a track call)
Sends the experiment and variation information as properties on a track call.

#### Send `Experiment Viewed` as a non-interaction event
Specifies the Experiment Viewed as a non-interaction event for Google Analytics

![optimizely1](/1.0/assets/img/guides/streaming/clickstream/optimizely/optimizely1.png)

### Step 3
Click 'Create Destination' and your pipeline will be activated. 
