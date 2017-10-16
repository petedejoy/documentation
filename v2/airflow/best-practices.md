---
title: DAG Writing Best Practices
sidebar: platform_sidebar
---
## Idempotency
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
It can be tempting to write your DAGs so that they move data directly from your source to destination. It usually makes for less code and involves less pieces, but doing so removes your ability to re-run just the extract or load portion of the pipeline individually. By putting an intermediary storage such as S3 or SQL Staging tables in between your source and destination, you gain the ability to separate the testing and re-running of the extract and load. 

For example, depending on your data retention policy you could modify the load logic and re-run the entire historical pipeline without having to re-run the extracts. This is also useful in situations where you no longer have to the source systems for various reasons. 

## Transformations
Look to implement an ELT data pipeline pattern with your DAG definition file. This means that you should look to offload as much of the transformation logic to the source systems or the destinations systems as possible. With python at your fingertips it can be tempting to attempt the transformations in the DAG but offloading those transformations to the source or destination systems will lead to better performance overall and you'll get the added benefit of keeping your DAG lean and readable.

### SQL Destination
Users will have a wide variety of constraints depending on the flavor of SQL used and resources available to that system. In general, seek to create staging tables in the form of temp tables or a more permanent schema. These staging tables will give you greater control of your data before pushing to a final destination.

### Mongo Source
To to use [aggregation pipelines](https://docs.mongodb.com/manual/core/aggregation-pipeline/) to perform your transformations on extract from a Mongo source.

### SQL Source
A SQL query can go a long way to cleaning up and combining data before it ever enters the pipeline - this will reduce headaches overall.

## Readability

### Task Depedencies
Task dependencies are set using the ```set_upstream()``` and ```set_upstream()``` operators. Using either will depend on your preferences, but it is best not to mix and match as the task for becomes difficult to interpret.

Example.

Instead of this

```
task_1.set_downstream(task_2)
task_3.set_upstream(task_2)
```

Try to use the same operator like this

```
task_1.set_downstream(task_2)
task_2.set_downstream(task_3)
```

or this

```
task_3.set_upstream(task_2)
task_2.set_upstream(task_1)
```