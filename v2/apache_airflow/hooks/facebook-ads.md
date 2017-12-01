---
title: Facebook Ads Hook
sidebar: platform_sidebar
---

For a complete list of Airflow Hooks, Operators, and Utilities maintained by Astronomer, check out our [Airflow Plugins](https://github.com/airflow-plugins?utf8=%E2%9C%93&q=&type=&language=) organization on Github.


## Facebook Ads

```python
from airflow.hooks.base_hook import BaseHook

from urllib.parse import urlencode
import requests
import time


class FacebookAdsHook(BaseHook):
    def __init__(self, facebook_ads_conn_id='facebook_ads_default'):
        self.facebook_ads_conn_id = facebook_ads_conn_id
        self.connection = self.get_connection(facebook_ads_conn_id)

        self.base_uri = 'https://graph.facebook.com'
        self.api_version = self.connection.extra_dejson['apiVersion'] or '2.10'
        self.access_token = self.connection.extra_dejson['accessToken'] or self.connection.password

    def get_insights_for_account_id(self, account_id, insight_fields, breakdowns, time_range, time_increment='all_days', level='ad', limit=100):
        payload = urlencode({
            'access_token': self.access_token,
            'breakdowns': ','.join(breakdowns),
            'fields': ','.join(insight_fields),
            'time_range': time_range,
            'time_increment': time_increment,
            'level': level,
            'limit': limit
        })

        response = requests.get('{base_uri}/v{api_version}/act_{account_id}/insights?{payload}'.format(
            base_uri=self.base_uri,
            api_version=self.api_version,
            account_id=account_id,
            payload=payload
        ))

        response.raise_for_status()
        response_body = response.json()
        insights = []

        while 'next' in response_body.get('paging', {}):
            time.sleep(1)
            insights.extend(response_body['data'])
            response = requests.get(response_body['paging']['next'])
            response.raise_for_status()
            response_body = response.json()

        insights.extend(response_body['data'])

        return insights
```
_[Source](https://github.com/airflow-plugins/facebook_ads_plugin/blob/master/hooks/facebook_ads_hook.py)_

- _Source Type_: REST-based API.
- _Authentication_: OAuth (Token)
- _Rate Limit_: Rate limiting depends on the type of account being used:

|Account     |Limit   |
|---------|------------------|
|Development   |Heavily rate-limited per ad account. For development only. Not for production apps running for live advertisers.             |
|Basic  |Moderately rate limited per ad account             |
|Standard   |Lightly rate limited per ad account             |

```
- Rate limitation happens real time on a sliding window.
- Each Marketing API call is assigned a score. Your score is the sum of your API calls.
- Updates are 10~100 more expensive than creates.
- There's a max score, and when it's is reached, the throttling error is thrown.
	- Error, Code: 17, Message: User request limit reached
```