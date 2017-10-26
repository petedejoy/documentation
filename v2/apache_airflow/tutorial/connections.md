---
title: Apache Airflow Connections
sidebar: platform_sidebar
---

This document covers how to set up various connections in Airflow. This information is needed in order to connect to your environment.

Connections can be maintained in the Airflow Interface (Menu --> Admin --> Connections)


##### Microsoft SQL Server
* `Host`: localhost
* `Schema`: n/a
* `Login`: _your username_
* `Password`: _blank_
* `Port`: 1433
* `Extras`: n/a

##### MongoDb
* `Host`:
* `Schema`: Authentication Database
* `Login`:
* `Password`:
* `Port`: 27017
* `Extras`: JSON Object of [connection options](https://docs.mongodb.com/manual/reference/connection-string/#connection-string-options)

##### MySQL
* `Host`: localhost
* `Schema`: n/a
* `Login`: _your username_
* `Password`: _blank_
* `Port`: 3306
* `Extras`: n/a

##### S3
* `Host`: n/a
* `Schema`: n/a
* `Login`: n/a
* `Password`: n/a
* `Port`: n/a
* `Extras`: {"aws_access_key_id":" ","aws_secret_access_key":" "}

##### Postgres
* `Host`: localhost
* `Schema`: _your schema name_
* `Login`: _your username_
* `Password`: _blank_
* `Port`: 5432
* `Extras`: n/a