---
title: Apache Airflow Operators Overview
sidebar: platform_sidebar
---

Along with Hooks, Operators are key to extending capabilities with Airflow while keeping your DAGs clean and simple.

An **operator** is an object that embodies an operation utilizing one or more hooks, typically to transfer data between one hook to another.

In Airflow, operators allow for generation of certain types of tasks that become nodes in the DAG when instantiated. All operators derive from BaseOperator and inherit many attributes and methods that way. There are 3 main types of operators:

  * **Action** - These operators perform an action or tell another system to perform an action.
  * **Transfer** - These operators move data from one system to another.
  * **Sensors** - This type of operator will keep running until a certain criterion is met.
