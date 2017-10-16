---
title: Sample DAG Deployment
sidebar: platform_sidebar
---

This is a step-by-step guide for using the Astronomer CLI to deploy a DAG to your Airflow instance.

### Prerequisites
* Before you can deploy a DAG, you will need to have both docker and the Astronomer CLI installed.

    Head to [Astronomer CLI Setup](https://github.com/astronomerio/pro-beta/wiki/Astronomer-CLI) for more instructions.

* You will also need to have a provisioned Airflow instance for your organization. Check this by going to your [Astronomer Pro App](pro.astronomer.io). Your PRO tab should look show Webserver and Scheduler as "Ready".

### Project Setup
First, you will need to login with your Astronomer credentials: `astro login`

Next, create a project directory, this is where your DAGs will be stored locally:
>mkdir /path/to/project

...and navigate to it:
>cd /path/to/project

### Quickstart DAG Deployment
Initialize a project: `astro init` which will create 2 folders in your project: `dags` and `plugins`.

Navigate to `dags`:

>cd /path/to/project/dags

Now, we need a DAG:

```
nano /path/to/project/dags/sample_dag.py
```

Copy and Paste this Sample DAG:
```python
from datetime import datetime
from airflow import DAG
from airflow.operators.dummy_operator import DummyOperator

args = {
    'owner': 'airflow',
    'start_date': datetime(2017, 9, 10, 0, 0),
    'random_logic': False
}

dag = DAG(
    'sample_dag',
    schedule_interval="@once",
    default_args=args
)

t1 = DummyOperator(
    task_id='extract_data',
    dag=dag
)

t2 = DummyOperator(
    task_id='load_data',
    dag=dag
)

t3 = DummyOperator(
    task_id='random_task',
    dag=dag
)

t1.set_downstream(t2)
t2.set_downstream(t3)

```
Save the DAG, return to the shell prompt, and now, we're ready to deploy (make sure your User belongs to an organization):

`astro deploy`

This will then prompt you to select from a list of organizations associated with your Astronomer account, and confirms you are sure you want to deploy.

Once you confirm, it will bundle all but a few blacklisted files and push to the API, and then to S3.

At this point, you can navigate to your Airflow instance via the Dashboard URL at pro.astronomer.io to see the deployed DAG. If necessary, refresh the page to see your newly deployed DAG.

In order to log out of your account, simply enter:

`astro logout`
