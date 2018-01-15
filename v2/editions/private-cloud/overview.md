---
title: Astronomer Private Cloud Edition
keywords: private-cloud airflow clickstream
sidebar: platform_sidebar
---

## Overview

Astronomer PCE aims to provide a managed, open-source-based data ingestion applications that can in any cloud.

* **Astronomer Pilot** provides a centralized GUI, API, monitoring, and alerts.
* **Astronomer Commander** provides orchestration with Kubernetes and Marathon (and Docker Swarm soon), which makes the platform deployable to AWS, Google Cloud, and Azure using your orchestration tool of choice.

Modules are deployed as interfaces and services that utilized shared data stores (Postgres, Redis, Kafka).

![Astronomer PCE Overview](/images/pce/pce_overview.png)

## Airflow

The Astronomer Platform aims to provide a managed, convenient, mostly-stock Airflow experience in any cloud.

![Airflow Open Diagram](/images/pce/airflow_open_diagram.png)

 Airflow has several ways to hook in and customize different pieces. Since we are aiming to provide the best possible Airflow experience, with minimal commits on our fork, we’ve dropped support for the Mesos Executor, in favor of the Celery Executor.

### Celery

The Celery Executor has the most support for Airflow features and reduces our dependency on the lower-level infrastructure layer. We can run our managed deployment on any number of orchestrators now. We currently have production-grade deployments for Marathon and Kubernetes, and an open edition on Docker Compose.

### Kubernetes

Running our Airflow deployment on Kubernetes has a few advantages over Marathon. Kubernetes has support for a resource they refer to as StatefulSets. StatefulSets are a way to run replicated pods that can mount durable, external volumes. Pods deployed as a replica of a StatefulSet each get a stable, well-known hostname as well. These two properties, make it a perfect match for Airflow Celery workers. The stable hostnames seamlessly allow the Airflow webserver to make requests to the correct worker for log files for a specific task, and the external volumes, ensure that the log data remains, even after a shutdown/upgrade/etc.

### Log rotation

Our Celery workers also run with a tiny sidecar that takes care of truncating old log files to prevent the volumes from filling up, a problem we’ve run into in the past all too often.

### Prometheus

We can also leverage StatefulSets to run a deployment-specific, “highly-available” Prometheus server. This just means that we can run two prometheus replicas, each with their own external volume for storage.
To achieve the same type of behavior with Marathon, we would need to individually configure and manage duplicate deployments of these services or build external tooling to fake this behavior by running identical apps, that each mount their own external volumes - something we’re not looking to tackle at this point.

### Helm

Another advantage of running Airflow on Kubernetes is Helm. Helm is essentially a package management solution for Kubernetes. Using Helm, we can define service dependencies, and template our YAML files so they don’t need to be manually tweaked for each deployment. We are able to define as many YAML files for our services as we need and template values in, by tweaking a single, separate, YAML file that contains concrete values for all the variables in the templates. Helm has a lot of nice features in addition to just templating that really make wielding multiple deployments of the same distributed system a lot easier and manageable.

Marathon really doesn’t have an equivalent here so we’ve built a small utility to template our Marathon JSON files in a similar way, but we do not have any plans of building a full-blown package management solution, like Helm. The DC/OS universe competes a little bit here, but is no substitute for Helm.

On a slightly related note, Kubernetes primarily works with YAML files to declaratively define resources, while Marathon requires JSON files. YAML is a lot easier to work with for these kinds of tasks, as JSON gets tedious and lengthy.

### Deployability

Finally, Kubernetes exposes a lot more than just “applications”, that can be declaratively defined and submitted to the cluster, allowing us to build up an entire distributed system, rather than juggling multiple steps to piece the system together. For example, our source controlled YAML files can be deployed in a single step, and it creates everything from managed configs and secrets, to load balancers, to replicated services and everything in between. With a single command, the entire system is deployed, wired-up and properly exposed to the outside world. Although we can do some similar things with Marathon it’s not as straightforward and we’d again probably need to build some custom tooling.

In general, Kubernetes provide a lot more primitives for building up distributed systems, while Marathon is more bare-bones. Under the hood, Mesos provides a low-level way to programatically allocate resources, which is great for things like Spark. Declaratively defining services with Kubernetes provides a lot of nice features that Marathon does not support and also allows us to quickly build more robust, interconnected systems. These are just some of the big reasons we’re moving forward with Kubernetes.

### Deploying DAGs

Deploying DAGs involves a Docker Registry that sends a webhook to a component we call Commander, which will generate Kubernetes calls and send them to the Airflow deployment, which will perform a rolling update to the Airflow deployment containers.

![DAG Deployment](/images/pce/dag_deployment.png)

## Clickstream

The Astronomer Platform aims to provide a managed, convenient, open-source-based clickstream experience in any cloud. You can learn more about the functionality of the clickstream module [here](/v2/clickstream/overview.html).

* User Events are sent from your applications to the Go-based Event API which drops them into Apache Kafka.
* The Event Router reads from configuration for the application to determine what to do with each event, where to forward it to, etc., and rewrites the event to destination-specific Kafka topics.
* Serverside workers process events off those destination-specific Kafka topics and send the events in real-time off to their destination.
* Sending events in batch (for example, to Redshift) require the Airflow Module.

![Airflow Open Diagram](/images/pce/clickstream_open_diagram.png)
