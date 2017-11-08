---
title: Introduction to Astronomer
keywords: introduction homepage
sidebar: platform_sidebar
summary: Astronomer is a data engineering platform that that helps you collect, process, and route data.
---

## Overview

Astronomer is a data engineering platform that provides a highly integrated set of tools that helps you collect, process, and route data (i.e. data engineering). Astronomer is built on industry proven open-source technologies (Apache Mesos, Apache Kafka, Apache Spark, Apache Airflow), and takes care of orchestrating and managing cloud infrastrucutre. The goal is to increase your ability to focus on data analytics and data science initiatives.

Astronomer includes:

* Analytics.js-based [clickstream](v2/clickstream/overview.html) module, which helps you collect data from your wwb and mobile applications and route those events to your tools and to your data lake. 
* A scalable managed [Apache Airflow](v2/airflow/tutorial/core-airflow-concepts.html) module, with a [CLI](https://docs.astronomer.io/v2/apache_airflow/cli.html) to make deployment easy.

Astronomer doesn't include:

* A data warehouse: There are a growing number of great data warehouse options. Astronomer integrates with all of them.
* Data visualization: Same deal, there are a growing number of great visualization tools, and we believe that you should "own your data" and handle all data processing outside of your visualization tools.

## Enterprise edition coming soon

Astronomer is currently available as a SaaS offering, however we're also in final stages of being able to deploy private instances of the platform to virtual private clouds.
