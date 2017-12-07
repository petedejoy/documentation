---
title: Salesforce Bulk API Hook
sidebar: platform_sidebar
---

For a complete list of Airflow Hooks, Operators, and Utilities maintained by Astronomer, check out our [Airflow Plugins](https://github.com/airflow-plugins?utf8=%E2%9C%93&q=&type=&language=) organization on Github.

## Salesforce Bulk API

- _Source Type_: REST API
- _Authentication_: Basic
- _Rate Limit_: N/A

**Bulk Query** (Use bulk query to efficiently query large data sets and reduce the number of API requests. A bulk query can retrieve up to 15 GB of data, divided into 15 1-GB files. The data formats supported are CSV, XML, and JSON.):
Bulk queries can be created using the Salesforce Object Query Language. Queries can be tested using the Developer Console in the Salesforce UI.
Sample SOQL query:
~~~
SELECT Id, Name FROM Account LIMIT 10
~~~
**Note:** While the SOAP and REST APIs return compound fields, the Bulk Query API does not support returning compound fields. The components of a compound field may be returned through the Bulk API, however. Example: "Name" is a compound field not returned through the Bulk API, while it's components, "First Name" and "Last Name" are returned through the Bulk API. Further reading: https://help.salesforce.com/articleView?id=000204592&type=1

