---
title: Astronomer Hooks
sidebar: platform_sidebar
---

For a complete list of Airflow Hooks, Operators, and Utilities maintained by Astronomer, check out our [Airflow Plugins](https://github.com/airflow-plugins?utf8=%E2%9C%93&q=&type=&language=) organization on Github.


## BambooHR

```python

from airflow.hooks.http_hook import HttpHook


class BambooHRHook(HttpHook):
    """
    Hook for BambooHR.
    Inherits from the base HttpHook to make a request to BambooHR.
    Uses basic authentication via a never expiring token that should
    be stored in the 'Login' field in the Airflow Connection panel.
    Only allows GET requests.
    """

    def __init__(self, bamboo_conn_id, method='GET'):
        super().__init__(method, http_conn_id=bamboo_conn_id)

    def get_conn(self, headers=None):
        session = super().get_conn(headers=headers)
        return session

    def run(self, company_name, endpoint, payload=None):
        self.endpoint = '{0}/v1/{1}'.format(company_name, endpoint)

        # Hard code hook to return JSON
        headers = {"Accept": "application/json"}

        return super().run(self.endpoint, data=payload, headers=headers)
```
_[Source](https://github.com/airflow-plugins/bamboo_hr_plugin/blob/master/hooks/bamboo_hr_hook.py)_

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

## Salesforce Bulk API

- _Source Type_: REST API
- _Authentication_: Basic
- _Rate Limit_: N/A

**Bulk Query** (Use bulk query to efficiently query large data sets and reduce the number of API requests. A bulk query can retrieve up to 15 GB of data, divided into 15 1-GB files. The data formats supported are CSV, XML, and JSON.):
Bulk queries can be created using the Salesforce Object Query Language. Queries can be tested using the Developer Console in the Salesforce UI.
Sample SOQL query:
```
SELECT Id, Name FROM Account LIMIT 10
```
**Note:** While the SOAP and REST APIs return compound fields, the Bulk Query API does not support returning compound fields. The components of a compound field may be returned through the Bulk API, however. Example: "Name" is a compound field not returned through the Bulk API, while it's components, "First Name" and "Last Name" are returned through the Bulk API. Further reading: https://help.salesforce.com/articleView?id=000204592&type=1

## Github

```python
from airflow.hooks.http_hook import HttpHook


class GithubHook(HttpHook):

    def __init__(self, github_conn_id):
        self.github_token = None
        conn_id = self.get_connection(github_conn_id)
        if conn_id.extra_dejson.get('token'):
            self.github_token = conn_id.extra_dejson.get('token')
        super().__init__(method='GET', http_conn_id=github_conn_id)

    def get_conn(self, headers):
        """
        Accepts both Basic and Token Authentication.
        If a token exists in the "Extras" section
        with key "token", it is passed in the header.
        If not, the hook looks for a user name and password.
        In either case, it is important to ensure your privacy
        settings for your desired authentication method allow
        read access to user, org, and repo information.
        """
        if self.github_token:
            headers = {'Authorization': 'token {0}'.format(self.github_token)}
            session = super().get_conn(headers)
            session.auth = None
            return session
        return super().get_conn(headers)
```
## Google Analytics

```python
from airflow.hooks.base_hook import BaseHook

from apiclient.discovery import build
from oauth2client.service_account import ServiceAccountCredentials

import time

class GoogleAnalyticsHook(BaseHook):
    def __init__(self, google_analytics_conn_id='google_analytics_default'):
        self.google_analytics_conn_id = google_analytics_conn_id
        self.connection = self.get_connection(google_analytics_conn_id)

        self.client_secrets = self.connection.extra_dejson['client_secrets']

    def get_service_object(self, api_name, api_version, scopes):
        credentials = ServiceAccountCredentials.from_json_keyfile_dict(self.client_secrets, scopes)
        return build(api_name, api_version, credentials=credentials)

    def get_analytics_report(self, view_id, since, until, sampling_level, dimensions, metrics, page_size, include_empty_rows):
        analytics = self.get_service_object('analyticsreporting', 'v4', ['https://www.googleapis.com/auth/analytics.readonly'])

        reportRequest = {
            'viewId': view_id,
            'dateRanges': [{ 'startDate': since, 'endDate': until }],
            'samplingLevel': sampling_level or 'LARGE',
            'dimensions': dimensions,
            'metrics': metrics,
            'pageSize': page_size or 100,
            'includeEmptyRows': include_empty_rows or False
        }

        response = analytics.reports().batchGet(body={ 'reportRequests': [reportRequest] }).execute()

        if response.get('reports'):
            report = response['reports'][0]
            rows = report.get('data', {}).get('rows', [])

            while report.get('nextPageToken'):
                time.sleep(1)
                reportRequest.update({ 'pageToken': report['nextPageToken'] })
                response = analytics.reports().batchGet(body={ 'reportRequests': [reportRequest] }).execute()
                report = response['reports'][0]
                rows.extend(report.get('data', {}).get('rows', []))

            if report['data']:
                report['data']['rows'] = rows

            return report
        else:
            return {}
```


