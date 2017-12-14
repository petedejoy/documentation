---
title: DAG Writing Best Practices
sidebar: platform_sidebar
---
### Idempotency
Data pipelines are a messy business with a lot of various components that can fail. [Idempotent](https://en.wikipedia.org/wiki/Idempotence) DAGs allow you to deliver results faster when something breaks and can save you from losing data down the road.

### Incremental Record Filtering
When possible, seek to break out your pipelines into incremental extracts and loads. This results in each DagRun representing only a small subset of your total dataset. This means that a failure in one subset of the data won't affect the rest of your DagRuns from completing successfully.

There are three ways you can achieve incremental pipelines.

#### Last Modified Date
This is the gold standard for incremental loads. Ideally each record in your source system contains a column containing the last time the record was modified. Every DagRun then looks for records that were updated within it's specified date parameters.

As an example, an DAG that runs hourly will have 24 DagRuns in for each day. Each DagRun will be responsible for loading any records that fall between the start and end of it's hour. When any of those DagRuns fail it will not stop the others from continuing to run.

#### Sequence IDs
When a last modified date is not available, a sequence or incrementing ID, can be used for incremental loads. This logic works best when the source records are only being appended to and never updated. If the source records are updated you should seek to implement a Last Modified Date in that source system and key your logic off of that. In the case of the source system not being updated, basing your incremental logic off of a sequence ID can be a sound way to filter pipeline records without a last modified date.

### Intermediary Data Storage
It can be tempting to write your DAGs so that they move data directly from your source to destination. It usually makes for less code and involves less pieces, but doing so removes your ability to re-run just the extract or load portion of the pipeline individually. By putting an intermediary storage layer such as S3 or SQL Staging tables in between your source and destination, you can separate the testing and re-running of the extract and load.

For example, depending on your data retention policy you could modify the load logic and re-run the entire historical pipeline without having to re-run the extracts. This is also useful in situations where you no longer have to the source systems for various reasons.

### Static start_date
A dynamic start_date is misleading. It can cause failures when clearing out failed task instances and missing DAG runs.

## Transformations
Look to implement an ELT (extract, load, transform) data pipeline pattern with your DAG definition file. This means that you should look to offload as much of the transformation logic to the source systems or the destinations systems as possible. With python at your fingertips it can be tempting to attempt the transformations in the DAG but offloading those transformations to the source or destination systems will lead to better overall performance and keeps your DAG lean and readable.

### Use Staging Tables
Try to use staging tables before pushing to a final destination. This makes debugging errors easier as you'll have the exact data that caused an error and adds a layer of safety.

**Note** By default, each task counts as its own database session, so avoid temporary tables that only last a session. Instead, have the last task in your DAG clear out intermediary tables if everything runs successfully.  

### Mongo Source
Use [aggregation pipelines](https://docs.mongodb.com/manual/core/aggregation-pipeline/) to perform your transformations on extract from a Mongo source.

### SQL Source
Try to do basic transformations and aggregations in SQL queries - this offloads transformation logic onto the source system and keeps your DAG readable.

## Readability

### Use a consistent file structure.

To keep any custom plugins easy for someone else to use, use a consistent file structure. At Astronomer, we use:
~~~
+--plugin_name
| README.md - High level description of what the plugin contains and what it does.
| __init__.py - Calls the AirflowPLugins manager.
+--operators - Contains the operators.
|  +--__init__.py
|  +--operator_one.py
+--hooks - Contains the hook.
|  +--__init__.py
|  +--hook_one.py
~~~

See [here](https://github.com/airflow-plugins/) for examples!

### Change the name of your DAG when you change the start date.
Changing the `start_date` of a DAG creates a new entry in Airflow's database, which could confuse the scheduler because there will be two DAGs with the same name but different schedules.

Changing the name of a DAG also creates a new entry in the database, which powers the dashboard, so follow a consistent naming convention since changing a DAG's name doesn't delete the entry in the database for the old name.

### Avoid top level code in your DAG file.
The Airflow executor executes top level code on every heartbeat, so a small amount of top level code can cause performance issues. Try to treat the DAG file like a config file and leave all the heavy lifting for the hook and operator.

### Task Dependencies
Task dependencies are set using the `set_upstream()` and `set_upstream()` operators. Using either will depend on your preferences, but it is best to stay consistent with which one you use.

#### Example

Instead of this

~~~
task_1.set_downstream(task_2)
task_3.set_upstream(task_2)
~~~

Try to use the same operator like this

~~~
task_1.set_downstream(task_2)
task_2.set_downstream(task_3)
~~~

or this

~~~
task_3.set_upstream(task_2)
task_2.set_upstream(task_1)
~~~
