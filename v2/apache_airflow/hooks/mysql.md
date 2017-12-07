---
title: MySQL Hook
sidebar: platform_sidebar
---

For a complete list of Airflow Hooks, Operators, and Utilities maintained by Astronomer, check out our [Airflow Plugins](https://github.com/airflow-plugins?utf8=%E2%9C%93&q=&type=&language=) organization on Github.

## MySQL
~~~ python
from airflow.hooks.mysql_hook import MySqlHook


class AstroMySqlHook(MySqlHook):
    def get_schema(self, table):
        query = \
            """
            SELECT COLUMN_NAME, COLUMN_TYPE
            FROM COLUMNS
            WHERE TABLE_NAME = '{0}';
            """.format(table)
        self.schema = 'information_schema'
        return super().get_records(query)
~~~
[Source](https://github.com/airflow-plugins/mysql_plugin/blob/master/hooks/astro_mysql_hook.py)
