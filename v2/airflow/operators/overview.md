---
title: Airflow Operators Overview
sidebar: platform_sidebar
---

Along with Hooks, Operators are key to extending capabilities with airflow while keeping your DAGs clean and simple.

An **operator** is an object that embodies an operation utilizing one or more hooks, typically to transfer data between one hook and another or to send/receive data from that

In Airflow, operators allow for generation of certain types of tasks that become nodes in the DAG when instantiated. All operators derive from BaseOperator and inherit many attributes and methods that way. There are 3 main types of operators:
  * **Action** - these operators perform an action or tell another system to perform an action.
  * **Transfer** - these operators move data from one system to another.
  * **Sensors** - this type of operator will keep running until a certain criterion is met.
