---
title: Autopilot Hook
sidebar: platform_sidebar
---

For a complete list of Airflow Hooks, Operators, and Utilities maintained by Astronomer, check out our [Airflow Plugins](https://github.com/airflow-plugins?utf8=%E2%9C%93&q=&type=&language=) organization on Github.


## Autopilot

~~~ python

from airflow.hooks.http_hook import HttpHook


class AutopilotHook(HttpHook):
    def __init__(self, method='GET', http_conn_id='autopilot_conn'):
        super().__init__(method, http_conn_id)
        print('method = ', method)
        self.http_conn_id = http_conn_id
        self.headers = ''

    def get_conn(self, headers=None):
        conn = super().get_connection(self.http_conn_id)
        self.headers =  {'autopilotapikey': conn.extra_dejson.get('key'),
            'accept-encoding': 'application/json'}
        session = super().get_conn(self.headers)

        return session

    def run(self,
            endpoint,
            data=None,
            headers=None,
            extra_options=None):
        print('here', endpoint, data, headers)
        return super().run(endpoint, data, headers, extra_options)

    def get_pandas_df(self, sql):
        pass

    def get_records(self, sql):
        pass

~~~

_[Source](https://github.com/airflow-plugins/autopilot_plugin/blob/master/hooks/autopilot_hook.py)_