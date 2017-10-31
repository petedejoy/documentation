---
title: Core Apache Airflow Concepts
sidebar: platform_sidebar
---

## Apache Airflow
Airflow is a generic workflow scheduler with dependency management. Not only does it schedule periodic jobs, it also allows you to define explicit dependencies between different stages in your data pipeline.

## DAGs
The main concept of Airflow is a `DAG` - or Directed Acyclic Graph.
A `DAG` is a collection of all the tasks you want to run, organized in a way that reflects their relationships and dependencies.

For example, a simple DAG could consist of 3 tasks: A, B, and C. It could say that A has to run successfully before B can run, but C can run anytime. It could also say that A times out after 5 minutes and that B can be restarted up to 5 times in case it fails. More broadly, it might also say that the workflow will run every night at 10pm but shouldn't start until a certain date.

![alt_text](http://michal.karzynski.pl/images/illustrations/2017-03-19/airflow-example-dag.png)

_[An example Airflow Pipeline DAG](http://michal.karzynski.pl/blog/2017/03/19/developing-workflows-with-apache-airflow/)_

Notice that the DAG we just outlined only describes _how_ to carry out a workflow, not _what_ we want the workflow to actually do - A, B, and C could really be anything! This is an important element of DAGs - they aren't concerned with what its constituent tasks do, they just make sure the tasks happen at the right time, in the right order, and with the right handling of any unexpected issues.

## Operators
The atomic units of DAGs - while DAGs describe _how_ to run a workflow, `Operators` determine _what actually gets done._

Operators describe single tasks in a workflow and can usually stand on their own, meaning they don't need to share resources with any other operators. They are so independent that they may even run on two completely different machines.

Note: in general, if two operators need to share information (e.g. a filename or a small amount of data), you should consider combining them into a single operator.

Here are some common operators and the tasks they accomplish:

* `BashOperator` - executes a bash command
* `EmailOperator` - sends an email
* `PythonOperator` - uses python to run a task

See [here](https://github.com/astronomerio/pro-beta/wiki/Airflow-Operators) for more detailed descriptions of Airflow Operators and how to utilize them.

## Tasks
Once an operator is instantiated, it is referred to as a `task`. The instantiation defines specific values when calling the abstract operator, and the parameterized task becomes a node in a DAG.

### Task Instances
A task executed at a time is called a `TaskInstance`. This represents a specific run of a task and is a combination of a DAG, at task, and a specific point in time.

Task instances also have indicative states, which could be "running", "success", "failed", "skipped", "up for retry", etc.

## Workflows
By combining `DAGs` and `Operators` to create `TaskInstances`, you can build complex workflows. Head [here](https://github.com/astronomerio/pro-beta/wiki/Simple-Sample-DAG) to see how they come together in a basic DAG.

## Templating with Jinja
Imagine you want to reference a unique s3 file name that corresponds to the date of the DAG run they ran for. Templating with Jinja helps you do so without having to hardcode anything! Jinja is a template engine for Python and Apache Airflow uses it to provide authors with a set of built-in paramaters and macros. A Jinja template is simply a text file that contains the following:
 * **variables** and/or **expressions** - these get replaced with values when a template is rendered)
 * **tags** - these control the logic of the template. 

In Jinja, the default delimiters are configured as follows:

{% raw %}
 * `{{% ... %}}` for Statements 
 * `{{ ... }}` for Expressions
 * `{{# ... #}}` for Comments
 * `# ... ##` for Line Statements
 {% endraw %}

Head [here](http://jinja.pocoo.org/docs/2.9/) for more information about installing and using Jinja.

With Apache Airflow, Jinja templating allows you to defer the rendering of strings in your tasks until the actual running of those tasks. This becomes particularly useful when you want to access certain parameters of a `task_run` itself (i.e. `run_date` or `file_name`).

### Example

```python
date = "\{\{ ds \}\}"

t = BashOperator(
        task_id='test_env',
        bash_command='/tmp/test.sh',
        dag=dag,
        env={'EXECUTION_DATE: date}
)
```
In the example above, we passed the execution date as an environment variable to a Bash script. `

{% raw %} `{{ ds }}` {% endraw %} is a macro and because the `env` parameter of the `BashOperator` is templated with Jinja, the execution date will be available as an environment variable named `EXECUTION_DATE` in your Bash script. 

**Note:** Astronomer's architecture is built in a way so that a task's container is spun down as soon as the task is completed. So, if you're trying to do something like download a file with one task and then upload that same task with another, you'll need to create a combined Operator that does both. 

## XComs
XComs (aka cross-communication) 

## Other Core concepts

### Default Arguments
If a dictionary of `default_args` is passed to a DAG, it will apply them to any of its operators. This makes it easy to apply a common parameter (e.g. start_date) to many operators without having to type it many times.

### Context Manager
DAGs can be used as context managers to automatically assign new operators to that DAG.

### DAG Assignment
Operators do not have to be assigned to DAGs immediately. DAG assignment can be done explicitly when the operator is created, through deferred assignment, or even inferred from other operators.

### Additional Functionality
In addition to these core concepts, Airflow has a number of more complex features. More detail on these functionalities is available [here](http://airflow.incubator.apache.org/concepts.html#additional-functionality).

Sources:

  * [Airflow Concepts](https://airflow.incubator.apache.org/concepts.html?highlight=core%20airflow%20concepts)
  * [Integrating Apache Airflow with Databricks](https://databricks.com/blog/2017/07/19/integrating-apache-airflow-with-databricks.html)
  * [Get started developing workflows with Apache Airflow](http://michal.karzynski.pl/blog/2017/03/19/developing-workflows-with-apache-airflow/)
