---
title: Monitoring Apache Airflow
sidebar: platform_sidebar
---

# Home Screen
This is the dashboard for all of your DAGs. From here you can get an overview for what is happening across all workflows for your organization.

## Dashboard Columns
Some of the high-level items you can glean from a glance are
* Is DAG Paused or Running?
* Schedule
  - How often should this DAG be running?
* Owner
  - Who should I contact when this DAG is not working properly?
* Recent Tasks
  - From the most recent run of this workflow, what is the count for each status in that DAG run?
* Last Run
  - Last active run for that DAG. If this column is empty your DAG is call caught up.
* DAG Runs
  - The final states and counts of each state for all DAG runs for that DAG

## States
A list of the various states you may see a DAG run or task instance in

* Success
* Running
* Failed
* Skipped (Task State Only)
* Retry (Task State Only)
* Queued (Task State Only)
* No Status

# Alerts
## Email
This method is best when you want to selectively email users who may be dependent on the outcome of workflows. Like most things in Airflow there a some options of how you can accomplish this task.

### Email in Default Args
When defining a DAG, many will often choose to define a set of default arguments (default_args), which will then be passed to every task in your workflow. A subset of these default_args are specific to emailing on retries and failures.

* ```email```
  - A string representation of an email or a list of emails
* ```email_on_retry```
  - A boolean representing whether or not to send an email to ```email``` on retry
* ```email_on_failure```
  - A boolean representing whether or not to send an email to ```email``` on failure

[Example Usecase](https://airflow.incubator.apache.org/tutorial.html?highlight=email)

### Custom Messaging Tasks
Airflow allows you to define complex workflows, this includes sending messages as a part of those workflows. Thanks to community contributed operators such as the [Slack](https://airflow.incubator.apache.org/_modules/slack_operator.html) or [email](https://pythonhosted.org/airflow/_modules/email_operator.html) operator you can notify your customers of successes, failures or other custom events as they happen.

#### Message on Success
In some cases, you may want to be notified when a workflow succeeds. The easiest way to achieve this is to add a task that happens at the end of your workflow for positive notifications.

#### Message on Failure
The built-in failure emails may not meet your needs for providing rich HTML content or sending a notification on failure via Slack. By adding a custom messaging task to your workflow and changing the [trigger rule](https://pythonhosted.org/airflow/concepts.html?highlight=trigger_rule#trigger-rules), these tasks can be customized to give notifications for DAG or task level granularity.
