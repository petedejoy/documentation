---
title: Segment | Clickstream Merge
sidebar: platform_sidebar
---
# Segment | Clickstream Merge

Made the switch from Segment to Astronomer Clickstream but want to have all of your data in one place? It's an easy process - we'll walk you through it. 

Check out this [blog post](https://www.astronomer.io/blog/switch-from-segment-to-astronomer-in-four-simple-st/) and follow the steps below:  

### Initial Column Audit

To start, we'd recommend that you take a few minutes to review your existing Segment tables with the tables created by Astronomer's Clickstream platform. Create a spreadsheet with tables from both platforms side by side to easily identify datatype conflicts. 

Here's the SQL to view that information:

```
SELECT * FROM information_schema.columns
WHERE table_schema = 'example_schema_name'
AND table_name = 'example_table_name'
```

### Datatype Conflicts

If you do identify some datatype conflicts, it's likely that your destination column will be able to accomodate the previous datatype (e.g. varchar(256) or varchar(512) or timestamp with timezone. Check out the following example:

![clickstream-merge1](../../../images/clickstream-merge1.png)

### Non-Existent Destination Columns

If you have some columns that don't exist in the destination tables, they'll need to either be dropped from the source (Segment) tables or added manually to the destination tables. 

You can do the latter manually via the [Alter Table Add Command](http://docs.aws.amazon.com/redshift/latest/dg/r_ALTER_TABLE.html).

### Differing Ordinal Positions

If the ordinal position differs between the two tables, a Bulk Insert ((e.g. `INSERT INTO {DESTINATION_TABLE} (SELECT * FROM SOURCE_TABLE}`) is slightly more complicated.

From here, you'll have 2 options: 

**A) Bulk Insert**

Here, use the specific column order as the destination tables rather than`SELECT` (see below)

![clickstream-merge2](../../../images/clickstream-merge2.png)

**B) Unload to S3 and then Copy**

This has a few more steps, but will likely be less taxing on your db depending on your row count. 

1. [Unload each source table to S3](http://docs.aws.amazon.com/redshift/latest/dg/r_UNLOAD.html)

2. [COPY each file from S3 into the corresponding destination table](http://docs.aws.amazon.com/redshift/latest/dg/r_COPY.html)

Here, you can specify the column order of the destination table that the file should load into. 


