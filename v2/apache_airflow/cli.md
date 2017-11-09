---
title: Astro CLI
sidebar: platform_sidebar
---
The Astro CLI helps users create and test activities and deploy those activities and Astronomer/community pre-built activities in actual DAGs. Once DAGs have been tested locally, users can deploy them to our public cloud or their private installation.

## Prerequisites

If you want to run Airflow locally through the CLI you will need docker installed.

See [docker download](https://www.docker.com/community-edition#/download) to download docker for your specific operating system.

## Setup

```
curl -o- http://cli.astronomer.io/install.sh | bash
```

**Note:** The above command only works on Mac & Linux. All other OS users will need to head [here](https://github.com/astronomerio/astro/releases/tag/v0.0.9) and download the binary manually.

## Usage

Login:
`astro login`

Create a project directory and navigate to it:

```
mkdir /path/to/project
cd /path/to/project
```

## Deploying with the Astro CLI

Initialize a project:

`astro init`

Create a DAG:

```
nano /path/to/project/dags/hello_world.py
vi /path/to/project/dags/hello_word.py
```

Copy and paste:

```python
from datetime import datetime
from airflow import DAG
from airflow.operators.dummy_operator import DummyOperator
from airflow.operators.python_operator import PythonOperator


def print_hello():
    return 'Hello world!'


dag = DAG('hello', description='Simple tutorial DAG',
          schedule_interval='0 12 * * *',
          start_date=datetime(2017, 3, 20), catchup=False)

dummy_operator = DummyOperator(task_id='dummy_task', retries=3, dag=dag)

hello_operator = PythonOperator(task_id='hello_task', python_callable=print_hello, dag=dag)

dummy_operator >> hello_operator

```

And now we're ready to deploy (make sure your user belongs to an organization):

```
astro deploy
```

This will prompt you to select the organization, and confirms you are sure you want to deploy.
Once you do that, it will bundle all but a few blacklisted files and push to the API, and then to S3.

If you want to log out of your account:

```
astro logout
```

## Local Airflow

Run `astro airflow up` to start the local airflow cluster.

Once started, it can be accessed at `http://localhost:8080`.

Once finished you can run `astro airflow down` to stop the cluster.

---

## Practical Example DAG

```python
from airflow import DAG
from astronomer import Activity

dag = DAG()
salesforce_entity_1 = Activity(dag, 'astronomerio/salesforce-source', ...)
salesforce_entity_2 = Activity(dag, 'astronomerio/salesforce-source', ...)
salesforce_entity_3 = Activity(dag, 'astronomerio/salesforce-source', ...)
custom_transform = Activity(dag, 'myorganization/salesforce-transform', ...)
redshift_sink = Activity(dag, 'astronomerio/redshift-sink', ...)

custom_transform.set_upstream([salesforce_entity_1, salesforce_entity_2, salesforce_entity_3])
redshift_sink.set_upstream(custom_transform)
```

## Commands

Usage:

```
  astro [command]
```

Available Commands:

```
  airflow       Run a local Airflow cluster
  config        Get or set Astro configs
  deploy        Deploy to production Airflow cluster
  help          Help about any command
  info          List important CLI information
  init          Create an Astronomer project
  login         Authenticate with Astronomer servers
  logout        Logout of current session
  organization  Organization functions
  status        Airflow cluster status
```

Flags:

```
  -d, --debug   debug output
  -h, --Help    help for astro
  -v, --verbose verbose output
```

Use `astro [command] --help` for more information about a command.

## Developing

### Metadata
When running/building locally you will need to generate the metadata file.  Running `make build-meta` or a `make build`
will build the meta data file. Once generated, you should be able to build/run without problem.
