---
title: Jinja Templating
sidebar: platform_sidebar
---

## Jinja Overview
Jinja is a template engine for Python and Apache Airflow uses it to provide authors with a set of built-in paramaters and macros. A Jinja template is simply a text file that contains the following:
 * **variables** and/or **expressions** - these get replaced with values when a template is rendered)
 * **tags** - these control the logic of the template. 

In Jinja, the default delimiters are configured as follows:
 * `{% ... %}` for Statements
 * `{{ ... }}` for Expressions
 * `{# ... #}` for Comments
 * `# ... ##` for Line Statements

Head [here](http://jinja.pocoo.org/docs/2.9/) for more information about installing and using Jinja.

## Templating with Jinja
With Apache Airflow, Jinja templating allows you to defer the rendering of strings in your tasks until the actual running of those tasks. This becomes particularly useful when you want to access certain parameters of a `task_run` itself (i.e. `run_date` or `file_name`).

Imagine you want to reference a unique s3 file name that corresponds to the date of the DAG run they ran for. Templating with Jinja helps you do so without having to hardcode anything.

### Example

```python
date = "{{ ds }}"

t = BashOperator(
        task_id='test_env',
        bash_command='/tmp/test.sh',
        dag=dag,
        env={'EXECUTION_DATE: date}
)
```
In the example above, `{{ ds }}` is a macro and because the `env` parameter of the `BashOperator` is templated with Jinja, the execution date will be available as an environment variable named `EXECUTION_DATE` in your Bash script. 

**Note:** Astronomer's architecture is built in a way so that a task's container is spun down as soon as the task is completed. So, if you're trying to do something like download a file with one task and then upload that same task with another, you'll need to create a combined Operator that does both. 