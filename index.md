---
title: Overview of the Astronomer Platform
keywords: introduction homepage
sidebar: platform_sidebar
summary: Astronomer is a data engineering platform that that helps you collect, process, and route data. It is available in Cloud, Enterprise, and Open editions. It includes two modules, Clickstream and Apache Airflow.
---

## Purpose

Astronomer is a data engineering platform that provides a highly integrated set of tools that helps you collect, process, and route data (i.e. data engineering). Astronomer is built on industry proven open-source technologies (Apache Mesos, Apache Kafka, Apache Spark, Apache Airflow), and takes care of orchestrating and managing cloud infrastructure. The goal is to increase your ability to focus on data analytics and data science initiatives.

[![Astronomer Overview](/images/how_it_works.png)](/images/how_it_works.png)

## Editions

* [Open](/v2/editions/open/overview.html) - run our Clickstream or Airflow module on your local machine, and adapt all oparts of it for your own use.
* [Enterprise](/v2/editions/enterprise/overview.html) - our full platform deployable via Kubernetes to your preferred cloud (AWS, Google Cloud, Azure).
* [Cloud](/v2/editions/cloud/overview.html) - we run enterprise edition for you - signup for an account at https://cloud.astronomer.io/ and get started with the platform quickly.

## Modules

* [Clickstream](/v2/clickstream/overview.html) - an Analytics.js-based module, which helps you collect data from your web and mobile applications, and route those events to your tools and to your data lake.
    - Best suited for those:
        - Just getting started collecting User Data
        - Have web apps and mobile apps with users that aren’t being tracked
        - Are using Google Analytics and a couple others tools
        - Want to warehouse user interaction data
        - Are a freemium, low revenue per monthly active user or e-commerce business model

    - Use Cases for Clickstream:
        - Product Analytics
        - Marketing Automation
        - User data tracking and warehousing

* [Apache Airflow](/v2/apache_airflow/tutorial/core-airflow-concepts.html) - Run and monitor Apache Airflow data workflows, with a [CLI](/v2/apache_airflow/cli.html) to make deployment easy.
    - Best suited for those:
        - Familiar with Airflow, but tired of running it themselves
        - Already using Airflow but planning on adding more team members
        - Wanting to collaborate on workflows
        - Currently using a drag-and-drop or other ETL solution, but unhappy or have outgrown it
        - Ready to invest in modern data infrastructure

    - Use Cases for Airflow:
        - Aggregating various data sources to a data lake, data warehouse or database
        - Post-processing data (more of an ELT approach than ETL)
        - Enhancing or enriching data mid-stream
        - Automating workflows

## What it's not

Astronomer doesn't include:

* A data warehouse - There are a growing number of great data warehouse options. Astronomer integrates with all of them.
* Data visualization - Same deal, there are a growing number of great visualization tools, and we believe that you should "own your data" and handle all data processing outside of your visualization tools.
