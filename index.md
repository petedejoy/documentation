---
title: Overview of the Astronomer Platform
keywords: introduction homepage
sidebar: platform_sidebar
summary: Astronomer is a data engineering platform that that helps you collect, process, and route data. It is available in SaaS, Private Cloud, and Open editions. It includes two modules, Clickstream and Apache Airflow.
---

## Purpose

Astronomer is a data engineering platform that provides a highly integrated set of tools that helps you collect, process, and route data (i.e. data engineering). Astronomer is built on industry proven open-source technologies (Apache Mesos, Apache Kafka, Apache Spark, Apache Airflow), and takes care of orchestrating and managing cloud infrastructure. The goal is to increase your ability to focus on data analytics and data science initiatives.

## Editions

* [Private Cloud](/v2/editions/private-cloud/overview.html) - we deploy a managed deployment of our platform to your preferred cloud (AWS, Google Cloud, Azure) through our Kubernetes Orchastrator.
* [Open](/v2/editions/open/overview.html) - run the platform on your local machine, or adapt parts of it for your own use.
* [SaaS](/v2/editions/saas/overview.html) - easiest way to get started, signup for an account at https://app.astronomer.io/ and get started with the platform quickly.

## Modules

* [Clickstream](v2/clickstream/overview.html) - an Analytics.js-based module, which helps you collect data from your web and mobile applications, and route those events to your tools and to your data lake.
* [Apache Airflow](v2/apache_airflow/tutorial/core-airflow-concepts.html) - Run and monitor Apache Airflow data workflows, with a [CLI](v2/apache_airflow/cli.html) to make deployment easy.

## What it's not

Astronomer doesn't include:

* A data warehouse - There are a growing number of great data warehouse options. Astronomer integrates with all of them.
* Data visualization - Same deal, there are a growing number of great visualization tools, and we believe that you should "own your data" and handle all data processing outside of your visualization tools.
