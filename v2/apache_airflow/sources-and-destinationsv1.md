
## Sources in Progress
Hooks for these sources are currently being developed by our team.

### GitHub
- _Source Type_: REST v3 -- (GraphQL v4 API currently unsupported)
- _Authentication_: Basic Authentication via Personal Token
- _Rate Limit_: Standard rate limit is 5000 requests/hour. Additionally, Github has [Abuse Controls](https://developer.github.com/v3/#abuse-rate-limits) that have an unspecified limit but will block requests if exceeding a certain high threshold of concurrent requests.
- Removed fields - Because Github returns duplicate data between endpoints, nested objects are removed (with the exception of their `id` field) to avoid unnecessary storage. For example, for each commit object, all information regarding the author is returned when this data is already available via the `members` endpoint so all unnecessary fields other than `id` are removed.

 | Endpoint      | Removed Object |
 |---------------|----------------|
 |Commits        |Author          |
 |Commits        |Committer       |
 |Issues         |Assignees       |
 |Issues         |Creator         |
 |Issues         |Repository      |
 |Issues         |User            |
 |Issue Comments |User            |
 |Repositories   |Owner           |
 |Repo Comments  |User            |

Reference: https://developer.github.com/v3/

**Commits sample response:**
```
{
    "url": "https://api.github.com/repos/octocat/Hello-World/commits/6dcb09b5b57875f334f61aebed695e2e4193db5e",
    "sha": "6dcb09b5b57875f334f61aebed695e2e4193db5e",
    "html_url": "https://github.com/octocat/Hello-World/commit/6dcb09b5b57875f334f61aebed695e2e4193db5e",
    "comments_url": "https://api.github.com/repos/octocat/Hello-World/commits/6dcb09b5b57875f334f61aebed695e2e4193db5e/comments",
    "commit": {
      "url": "https://api.github.com/repos/octocat/Hello-World/git/commits/6dcb09b5b57875f334f61aebed695e2e4193db5e",
      "author": {
        "name": "Monalisa Octocat",
        "email": "support@github.com",
        "date": "2011-04-14T16:00:49Z"
      },
      "committer": {
        "name": "Monalisa Octocat",
        "email": "support@github.com",
        "date": "2011-04-14T16:00:49Z"
      },
      "message": "Fix all the bugs",
      "tree": {
        "url": "https://api.github.com/repos/octocat/Hello-World/tree/6dcb09b5b57875f334f61aebed695e2e4193db5e",
        "sha": "6dcb09b5b57875f334f61aebed695e2e4193db5e"
      },
      "comment_count": 0,
      "verification": {
        "verified": false,
        "reason": "unsigned",
        "signature": null,
        "payload": null
      }
    },
    "author": {
      "id": 1
    },
    "committer": {
      "id": 1
    },
    "parents": [
      {
        "url": "https://api.github.com/repos/octocat/Hello-World/commits/6dcb09b5b57875f334f61aebed695e2e4193db5e",
        "sha": "6dcb09b5b57875f334f61aebed695e2e4193db5e"
      }
    ]
  }
```

**Commit Comments sample response:**
```
  {
    "html_url": "https://github.com/octocat/Hello-World/commit/6dcb09b5b57875f334f61aebed695e2e4193db5e#commitcomment-1",
    "url": "https://api.github.com/repos/octocat/Hello-World/comments/1",
    "id": 1,
    "body": "Great stuff",
    "path": "file1.txt",
    "position": 4,
    "line": 14,
    "commit_id": "6dcb09b5b57875f334f61aebed695e2e4193db5e",
    "user": {
      "id": 1
    },
    "created_at": "2011-04-14T16:00:49Z",
    "updated_at": "2011-04-14T16:00:49Z"
  }
```

**Issues sample response:**
```
{
    "id": 1,
    "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
    "repository_url": "https://api.github.com/repos/octocat/Hello-World",
    "labels_url": "https://api.github.com/repos/octocat/Hello-World/issues/1347/labels{/name}",
    "comments_url": "https://api.github.com/repos/octocat/Hello-World/issues/1347/comments",
    "events_url": "https://api.github.com/repos/octocat/Hello-World/issues/1347/events",
    "html_url": "https://github.com/octocat/Hello-World/issues/1347",
    "number": 1347,
    "state": "open",
    "title": "Found a bug",
    "body": "I'm having a problem with this.",
    "user": {
      "id": 1,
    },
    "labels": [
      {
        "id": 208045946,
        "url": "https://api.github.com/repos/octocat/Hello-World/labels/bug",
        "name": "bug",
        "color": "f29513",
        "default": true
      }
    ],
    "assignee": {
      "id": 1,
    },
    "assignees": [
      {
        "login": "octocat",
        "id": 1,
        "avatar_url": "https://github.com/images/error/octocat_happy.gif",
        "gravatar_id": "",
        "url": "https://api.github.com/users/octocat",
        "html_url": "https://github.com/octocat",
        "followers_url": "https://api.github.com/users/octocat/followers",
        "following_url": "https://api.github.com/users/octocat/following{/other_user}",
        "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
        "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
        "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
        "organizations_url": "https://api.github.com/users/octocat/orgs",
        "repos_url": "https://api.github.com/users/octocat/repos",
        "events_url": "https://api.github.com/users/octocat/events{/privacy}",
        "received_events_url": "https://api.github.com/users/octocat/received_events",
        "type": "User",
        "site_admin": false
      }
    ],
    "milestone": {
      "url": "https://api.github.com/repos/octocat/Hello-World/milestones/1",
      "html_url": "https://github.com/octocat/Hello-World/milestones/v1.0",
      "labels_url": "https://api.github.com/repos/octocat/Hello-World/milestones/1/labels",
      "id": 1002604,
      "number": 1,
      "state": "open",
      "title": "v1.0",
      "description": "Tracking milestone for version 1.0",
      "creator": {
        "id": 1,
      },
      "open_issues": 4,
      "closed_issues": 8,
      "created_at": "2011-04-10T20:09:31Z",
      "updated_at": "2014-03-03T18:58:10Z",
      "closed_at": "2013-02-12T13:22:01Z",
      "due_on": "2012-10-09T23:39:01Z"
    },
    "locked": false,
    "comments": 0,
    "pull_request": {
      "url": "https://api.github.com/repos/octocat/Hello-World/pulls/1347",
      "html_url": "https://github.com/octocat/Hello-World/pull/1347",
      "diff_url": "https://github.com/octocat/Hello-World/pull/1347.diff",
      "patch_url": "https://github.com/octocat/Hello-World/pull/1347.patch"
    },
    "closed_at": null,
    "created_at": "2011-04-22T13:33:48Z",
    "updated_at": "2011-04-22T13:33:48Z",
    "repository": {
      "id": 1296269
    }
  }
```

**Issue Comments sample response:**
```
  {
    "id": 1,
    "url": "https://api.github.com/repos/octocat/Hello-World/issues/comments/1",
    "html_url": "https://github.com/octocat/Hello-World/issues/1347#issuecomment-1",
    "body": "Me too",
    "user": {
      "id": 1,
    },
    "created_at": "2011-04-14T16:00:49Z",
    "updated_at": "2011-04-14T16:00:49Z"
  }
```

**Members sample response:**
```
  {
    "login": "octocat",
    "id": 1,
    "avatar_url": "https://github.com/images/error/octocat_happy.gif",
    "gravatar_id": "",
    "url": "https://api.github.com/users/octocat",
    "html_url": "https://github.com/octocat",
    "followers_url": "https://api.github.com/users/octocat/followers",
    "following_url": "https://api.github.com/users/octocat/following{/other_user}",
    "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
    "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
    "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
    "organizations_url": "https://api.github.com/users/octocat/orgs",
    "repos_url": "https://api.github.com/users/octocat/repos",
    "events_url": "https://api.github.com/users/octocat/events{/privacy}",
    "received_events_url": "https://api.github.com/users/octocat/received_events",
    "type": "User",
    "site_admin": false
  }
```

**Organizations sample response:**
```
  {
    "login": "github",
    "id": 1,
    "url": "https://api.github.com/orgs/github",
    "repos_url": "https://api.github.com/orgs/github/repos",
    "events_url": "https://api.github.com/orgs/github/events",
    "hooks_url": "https://api.github.com/orgs/github/hooks",
    "issues_url": "https://api.github.com/orgs/github/issues",
    "members_url": "https://api.github.com/orgs/github/members{/member}",
    "public_members_url": "https://api.github.com/orgs/github/public_members{/member}",
    "avatar_url": "https://github.com/images/error/octocat_happy.gif",
    "description": "A great organization"
  }
```

**Repositories sample response:**
```
{
    "id": 1296269,
    "owner": {
      "id": 1
    },
    "name": "Hello-World",
    "full_name": "octocat/Hello-World",
    "description": "This your first repo!",
    "private": false,
    "fork": true,
    "url": "https://api.github.com/repos/octocat/Hello-World",
    "html_url": "https://github.com/octocat/Hello-World",
    "archive_url": "http://api.github.com/repos/octocat/Hello-World/{archive_format}{/ref}",
    "assignees_url": "http://api.github.com/repos/octocat/Hello-World/assignees{/user}",
    "blobs_url": "http://api.github.com/repos/octocat/Hello-World/git/blobs{/sha}",
    "branches_url": "http://api.github.com/repos/octocat/Hello-World/branches{/branch}",
    "clone_url": "https://github.com/octocat/Hello-World.git",
    "collaborators_url": "http://api.github.com/repos/octocat/Hello-World/collaborators{/collaborator}",
    "comments_url": "http://api.github.com/repos/octocat/Hello-World/comments{/number}",
    "commits_url": "http://api.github.com/repos/octocat/Hello-World/commits{/sha}",
    "compare_url": "http://api.github.com/repos/octocat/Hello-World/compare/{base}...{head}",
    "contents_url": "http://api.github.com/repos/octocat/Hello-World/contents/{+path}",
    "contributors_url": "http://api.github.com/repos/octocat/Hello-World/contributors",
    "deployments_url": "http://api.github.com/repos/octocat/Hello-World/deployments",
    "downloads_url": "http://api.github.com/repos/octocat/Hello-World/downloads",
    "events_url": "http://api.github.com/repos/octocat/Hello-World/events",
    "forks_url": "http://api.github.com/repos/octocat/Hello-World/forks",
    "git_commits_url": "http://api.github.com/repos/octocat/Hello-World/git/commits{/sha}",
    "git_refs_url": "http://api.github.com/repos/octocat/Hello-World/git/refs{/sha}",
    "git_tags_url": "http://api.github.com/repos/octocat/Hello-World/git/tags{/sha}",
    "git_url": "git:github.com/octocat/Hello-World.git",
    "hooks_url": "http://api.github.com/repos/octocat/Hello-World/hooks",
    "issue_comment_url": "http://api.github.com/repos/octocat/Hello-World/issues/comments{/number}",
    "issue_events_url": "http://api.github.com/repos/octocat/Hello-World/issues/events{/number}",
    "issues_url": "http://api.github.com/repos/octocat/Hello-World/issues{/number}",
    "keys_url": "http://api.github.com/repos/octocat/Hello-World/keys{/key_id}",
    "labels_url": "http://api.github.com/repos/octocat/Hello-World/labels{/name}",
    "languages_url": "http://api.github.com/repos/octocat/Hello-World/languages",
    "merges_url": "http://api.github.com/repos/octocat/Hello-World/merges",
    "milestones_url": "http://api.github.com/repos/octocat/Hello-World/milestones{/number}",
    "mirror_url": "git:git.example.com/octocat/Hello-World",
    "notifications_url": "http://api.github.com/repos/octocat/Hello-World/notifications{?since, all, participating}",
    "pulls_url": "http://api.github.com/repos/octocat/Hello-World/pulls{/number}",
    "releases_url": "http://api.github.com/repos/octocat/Hello-World/releases{/id}",
    "ssh_url": "git@github.com:octocat/Hello-World.git",
    "stargazers_url": "http://api.github.com/repos/octocat/Hello-World/stargazers",
    "statuses_url": "http://api.github.com/repos/octocat/Hello-World/statuses/{sha}",
    "subscribers_url": "http://api.github.com/repos/octocat/Hello-World/subscribers",
    "subscription_url": "http://api.github.com/repos/octocat/Hello-World/subscription",
    "svn_url": "https://svn.github.com/octocat/Hello-World",
    "tags_url": "http://api.github.com/repos/octocat/Hello-World/tags",
    "teams_url": "http://api.github.com/repos/octocat/Hello-World/teams",
    "trees_url": "http://api.github.com/repos/octocat/Hello-World/git/trees{/sha}",
    "homepage": "https://github.com",
    "language": null,
    "forks_count": 9,
    "stargazers_count": 80,
    "watchers_count": 80,
    "size": 108,
    "default_branch": "master",
    "open_issues_count": 0,
    "topics": [
      "octocat",
      "atom",
      "electron",
      "API"
    ],
    "has_issues": true,
    "has_wiki": true,
    "has_pages": false,
    "has_downloads": true,
    "archived": false,
    "pushed_at": "2011-01-26T19:06:43Z",
    "created_at": "2011-01-26T19:01:12Z",
    "updated_at": "2011-01-26T19:14:43Z",
    "permissions": {
      "admin": false,
      "push": false,
      "pull": true
    },
    "allow_rebase_merge": true,
    "allow_squash_merge": true,
    "allow_merge_commit": true,
    "subscribers_count": 42,
    "network_count": 0
  }
```
*** 
## Sources in Queue
These are sources for which we have done preliminary requirements gathering but development work has not begun. 

### AutoPilot

- _Source Type_: REST API
- _Authentication_: API key
- _Rate Limit_: N/A

**Endpoints**
- Get all contacts (List all contacts)
- Get Contacts (List contact records by contact ID)
- List of Lists (List of available lists)
- Get contacts on a list (Returns a list of all contacts on a provided list)
- List smart segments (Get a list of all smart segments)
- Smart segment contacts (Get a list of contacts on a smart segment)
- Get custom fields
- List journeys with API triggers

### FreshDesk

- _Source Type_: RESTful API
- _Authentication_: API key or Basic Auth
- _Rate Limit_: Varies by plan

 |Plan     |Rate Limit (_Hourly_)  |
 |---------|------------------|
 |Sprout   |1,000             |
 |Blossom  |3,000             |
 |Garden   |3,000             |
 |Estate   |5,000             |
 |Forest   |5,000             |

**Endpoints:**
- Tickets - List All Tickets
- Contacts - List All Contacts
- Agents - List All Agents
- Roles - List All Roles
- Groups - List All Groups
- Companies - List All Companies
- Surveys - List All Surveys
- Satisfaction Ratings - View All Satisfaction Ratings
- Time Entries - List All Time Entries
- Products - List All Products
- Business Hours - List All Business Hours
- SLA Policies - List All SLA Policies

### Freshsales

- _Source Type_: REST API
- _Authentication_: Basic or API toekn
- _Rate Limit_: N/A

### Google Analytics

- _Source Type_:
- _Authentication_: OAuth2
- _Rate Limit_:
	- 50,000 requests per project per day, which can be increased.
	- 10 queries per second (QPS) per IP address.
	- Further Reading: https://developers.google.com/analytics/devguides/reporting/core/v2/limits-quotas

  **Data sources**
  Reporting API, Batch reports: https://developers.google.com/analytics/devguides/reporting/core/v4/rest/v4/reports/batchGet

  Sample request:
  ```
  POST https://analyticsreporting.googleapis.com/v4/reports:batchGet
  {
    "viewId": string,
    "dateRanges": [
      {
        object(DateRange)
      }
    ],
    "samplingLevel": enum(Sampling),
    "dimensions": [
      {
        object(Dimension)
      }
    ],
    "dimensionFilterClauses": [
      {
        object(DimensionFilterClause)
      }
    ],
    "metrics": [
      {
        object(Metric)
      }
    ],
    "metricFilterClauses": [
      {
        object(MetricFilterClause)
      }
    ],
    "filtersExpression": string,
    "orderBys": [
      {
        object(OrderBy)
      }
    ],
    "segments": [
      {
        object(Segment)
      }
    ],
    "pivots": [
      {
        object(Pivot)
      }
    ],
    "cohortGroup": {
      object(CohortGroup)
    },
    "pageToken": string,
    "pageSize": number,
    "includeEmptyRows": boolean,
    "hideTotals": boolean,
    "hideValueRanges": boolean,
  }

  ```

  Sample response:
  ```
  {
    "columnHeader": {
      object(ColumnHeader)
    },
    "data": {
      object(ReportData)
    },
    "nextPageToken": string,
  }
  ```

### Hubspot

- _Source Type_: REST
- _Authentication_: API key (OAuth is strongly encouraged and required to become an featured integration)
- _Rate Limit_: https://developers.hubspot.com/apps/api_guidelines
   - 10 requests per second
   - 40,000 requests per day

**`GET /email/public/v1/campaigns/by-id`**

**Example request:** `https://api.hubapi.com/email/public/v1/campaigns/by-id?hapikey=demo&limit=3`
Optional parameters:
  - Offset
  - Limit

```
{
    "hasMore": true,
    "offset": "MTYxOTkyMDA=",
    "campaigns": [
        {
            "id": 16275278,
            "appId": 113,
            "appName": "Batch"
        },
        {
            "id": 16273490,
            "appId": 113,
            "appName": "Batch"
        },
        {
            "id": 16199200,
            "appId": 113,
            "appName": "Batch"
        }
    ]
}
```

**`GET /email/public/v1/events`** (Query the event log for events matching specified parameters.)

**Example request:** `https://api.hubapi.com/email/public/v1/events?hapikey=demo&campaignId=13054799&appId=20185`

```
{
    "events": [
        {
            "appId": 20185,
            "appName": "AbBatch",
            "browser": {
                "family": "Google Image Cache",
                "name": "Google Image Cache",
                "producer": "",
                "producerUrl": "",
                "type": "Proxy",
                "url": "",
                "version": []
            },
            "created": 1401715797602,
            "emailCampaignId": 13054799,
            "hmid": "ELPoAxjZnQEoz+acBjoSbWF4aWFrQGh1YnNwb3QuY29t",
            "id": "fb5f4051-0bf9-3b3c-92f4-ffbab071ed66",
            "ipAddress": "66.249.88.8",
            "location": {
                "city": "Unknown",
                "country": "Unknown",
                "state": "Unknown"
            },
            "portalId": 62515,
            "recipient": "maxiak@hubspot.com",
            "type": "OPEN",
            "userAgent": "Mozilla/5.0 (Windows; U; Windows NT 5.1; de; rv:1.9.0.7) Gecko/2009021910 Firefox/3.0.7 (via ggpht.com GoogleImageProxy)"
        },
        {
            "appId": 20185,
            "appName": "AbBatch",
            "browser": null,
            "created": 1401715797000,
            "emailCampaignId": 13054799,
            "hmid": "CiQ4ZWE5NTlmYy00MmU1LTRlZDctOTJjZC0zNjI0ZGRlNGYwODQQs+gDGNmdASAAKM/mnAYwoRY6Em1heGlha0BodWJzcG90LmNvbUCUhZPm5ShIAVooMWQ5NmYyODcyNDFjMmQzYWU1MDEwNTc3NmRkMDI5NzQ4ZjVjY2U3NXCR9A0=",
            "id": "9221577f-8a9b-38e5-a96a-08e57550e8c2",
            "ipAddress": "66.249.88.63",
            "location": null,
            "portalId": 62515,
            "recipient": "maxiak@hubspot.com",
            "sentBy": {
                "created": 1401715737236,
                "id": "8ea959fc-42e5-4ed7-92cd-3624dde4f084"
            },
            "type": "OPEN",
            "userAgent": "Mozilla/5.0 (Windows; U; Windows NT 5.1; de; rv:1.9.0.7) Gecko/2009021910 Firefox/3.0.7 (via ggpht.com GoogleImageProxy)"
        },
        {
            "appId": 20185,
            "appName": "AbBatch",
            "created": 1401715744000,
            "emailCampaignId": 13054799,
            "hmid": "CiQ4ZWE5NTlmYy00MmU1LTRlZDctOTJjZC0zNjI0ZGRlNGYwODQQs+gDGNmdASAAKM/mnAYwoRY6Em1heGlha0BodWJzcG90LmNvbUCUhZPm5ShIAVooMWQ5NmYyODcyNDFjMmQzYWU1MDEwNTc3NmRkMDI5NzQ4ZjVjY2U3NXCR9A0=",
            "id": "e4e7b45d-83ff-3faa-81a5-d241a3ce6e31",
            "portalId": 62515,
            "recipient": "maxiak@hubspot.com",
            "response": "250 Thanks ",
            "sentBy": {
                "created": 1401715737236,
                "id": "8ea959fc-42e5-4ed7-92cd-3624dde4f084"
            },
            "smtpId": "<1114083043.73189221401715737245.JavaMail.root@hemingway>",
            "type": "DELIVERED"
        },
        {
            "appId": 20185,
            "appName": "AbBatch",
            "created": 1401715737236,
            "emailCampaignId": 13054799,
            "hmid": "CiQ4ZWE5NTlmYy00MmU1LTRlZDctOTJjZC0zNjI0ZGRlNGYwODQQs+gDGNmdASAAKM/mnAYwoRY6Em1heGlha0BodWJzcG90LmNvbUCUhZPm5ShIAVooMWQ5NmYyODcyNDFjMmQzYWU1MDEwNTc3NmRkMDI5NzQ4ZjVjY2U3NXCR9A0=",
            "id": "8ea959fc-42e5-4ed7-92cd-3624dde4f084",
            "portalId": 62515,
            "recipient": "maxiak@hubspot.com",
            "sendId": "1d96f287241c2d3ae50105776dd029748f5cce75",
            "sentBy": {
                "created": 1401715737236,
                "id": "8ea959fc-42e5-4ed7-92cd-3624dde4f084"
            },
            "subject": "test",
            "type": "SENT"
        },
        {
            "appId": 20185,
            "appName": "AbBatch",
            "created": 1401715737000,
            "emailCampaignId": 13054799,
            "hmid": "CiQ4ZWE5NTlmYy00MmU1LTRlZDctOTJjZC0zNjI0ZGRlNGYwODQQs+gDGNmdASAAKM/mnAYwoRY6Em1heGlha0BodWJzcG90LmNvbUCUhZPm5ShIAVooMWQ5NmYyODcyNDFjMmQzYWU1MDEwNTc3NmRkMDI5NzQ4ZjVjY2U3NXCR9A0=",
            "id": "c26a72e7-d78b-3ec0-8801-54d951608c48",
            "portalId": 62515,
            "recipient": "maxiak@hubspot.com",
            "sentBy": {
                "created": 1401715737236,
                "id": "8ea959fc-42e5-4ed7-92cd-3624dde4f084"
            },
            "type": "PROCESSED"
        }
    ],
    "hasMore": false,
    "offset": "Ch8KFgjImIKLlZvVgIgBEMD9rLz93Jy1wgEYqIOT5uUoFZRhY64="
}

```

### Instagram

- _Source Type_: REST API
- _Authentication_: OAuth 2.0
- _Rate Limit_:

Global rate limits are applied inclusive of all API calls made by an app per access token over the 1-hour sliding window, regardless of the particular endpoint. Rate limits also apply to invalid or malformed requests.

| *Client Status* | *Rate Limit* (_Hourly_) |
|-----------------|-------------------------|
|Sandbox	  |500 / hour               |
|Live	          |5000 / hour              |

### JIRA

- _Source Type_: REST API
- _Authentication_: OAuth 1.0 or Basic
- _Rate Limit_: 500 API requests per 5 minutes. Once you exceed the limit, calls will return HTTP status 429 and a message telling you that you've been limited.

### Marketo

- _Source Type_: REST API
- _Authentication_: Basic
- _Rate Limit_: N/A

**Data Sources:**
#### [Authentication](http://developers.marketo.com/rest-api/endpoint-reference/authentication-endpoint-reference/#!/Identity/identityUsingGET)

Identity (Returned access token expires within 60 minutes of request. Subsequent requests will return the same token with an updated expiry count in seconds.

**Sample request:**
```
https://541-SJO-620.mktorest.com/identity/oauth/token?grant_type=client_credentials&client_id=b8bcba05-644f-4cd9-bc11-b196a89e4dc3&client_secret=<SECRET>

```

**Sample response:**
```
{
    "access_token": "<ACCESS_TOKEN>",
    "token_type": "bearer",
    "expires_in": 3599,
    "scope": "implementation@astronomer.io"
}
```

### [Paging Tokens](http://developers.marketo.com/rest-api/paging-tokens/)
To page through results, or retrieve data updated relative to a given data, Marketo provides paging tokens.
Documentation: http://developers.marketo.com/rest-api/paging-tokens/

#### Retrieve paging token:

**Sample request:**
`GET /rest/v1/activities/pagingtoken.json?sinceDatetime=2014-10-06T13:22:17-08:00`

**Sample response:**

```
{
    "requestId": "1607c#14884f3e74e",
    "success": true,
    "nextPageToken": "GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ"
}
```

### [Activities](http://developers.marketo.com/rest-api/lead-database/activities/)

#### [Describe activities](http://developers.marketo.com/rest-api/endpoint-reference/lead-database-endpoint-reference/#!/Activities/getAllActivityTypesUsingGET)

**Sample request:**
`GET /rest/v1/activities/types.json`

**Sample response:**
```
{  
   "requestId":"6e78#148ad3b76f1",
   "success":true,
   "result":[  
       {  
         "id":2,
         "name":"Fill Out Form",
         "description":"User fills out and submits form on web page",
         "primaryAttribute":{  
            "name":"Webform ID",
            "dataType":"integer"
         },
         "attributes":[  
            {  
               "name":"Client IP Address",
               "dataType":"string"
            },
            {  
               "name":"Form Fields",
               "dataType":"text"
            },
            {  
               "name":"Query Parameters",
               "dataType":"string"
            },
            {  
               "name":"Referrer URL",
               "dataType":"string"
            },
            {  
               "name":"User Agent",
               "dataType":"string"
            },
            {  
               "name":"Webpage ID",
               "dataType":"integer"
            }
         ]
      }
   ]
}
```

#### [Get Lead Activities](http://developers.marketo.com/rest-api/endpoint-reference/lead-database-endpoint-reference/#!/Activities/getLeadActivitiesUsingGET)

**Sample request:**
```
GET https://541-SJO-620.mktorest.com/rest/v1/activities.json?access_token=<TOKEN>&nextPageToken=K33T5MIVQSZCDLDDPSIAJAGHW6UR2MPYNBT7E42JMVTTXSIP4PYA====&activityTypeIds=2
```

**Sample response:**
```
{
    "requestId": "bad3#15f49676762",
    "result": [
        {
            "id": 1318761919,
            "marketoGUID": "1318761919",
            "leadId": 4692803,
            "activityDate": "2014-10-06T21:22:55Z",
            "activityTypeId": 2,
            "primaryAttributeValueId": 1730,
            "primaryAttributeValue": "By-State",
            "attributes": [
                {
                    "name": "Client IP Address",
                    "value": "68.174.28.205"
                },
                {
                    "name": "Form Fields",
                    "value": "a:27:{s:6:\"module\";s:11:\"leadCapture\";s:6:\"action\";s:5:\"save2\";s:17:\"Self_ID_d_Type__c\";s:13:\"Subcontractor\";s:9:\"FirstName\";s:3:\"Bob\";s:8:\"LastName\";s:7:\"Johnson\";s:7:\"Company\";s:18:\"Swift Construction\";s:5:\"Email\";s:25:\"bob@swiftconstruction.com\";s:5:\"Phone\";s:14:\"(845) 217-5220\";s:10:\"PostalCode\";s:5:\"12477\";s:21:\"Market_of_Interest__c\";s:2:\"NY\";s:18:\"Prevailing_Wage__c\";s:3:\"Yes\";s:19:\"GA_Campaign_Name__c\";s:14:\"UU-WS-By-State\";s:20:\"GA_Campaign_NameC__c\";s:14:\"UU-WS-By-State\";s:12:\"GA_Medium__c\";s:7:\"Website\";s:12:\"GA_Source__c\";s:7:\"Website\";s:23:\"Last_Form_Filled_Out__c\";s:14:\"UU-WS-By-State\";s:6:\"formid\";s:4:\"1730\";s:4:\"lpId\";s:4:\"4188\";s:5:\"subId\";s:3:\"150\";s:10:\"munchkinId\";s:11:\"541-SJO-620\";s:5:\"lpurl\";s:60:\"http://go.isqft.com/New-York.html?cr={creative}&kw={keyword}\";s:2:\"cr\";s:0:\"\";s:2:\"kw\";s:0:\"\";s:1:\"q\";s:0:\"\";s:8:\"_mkt_trk\";s:55:\"id:541-SJO-620&token:_mch-isqft.com-1412630284776-83634\";s:7:\"formVid\";s:4:\"1730\";s:13:\"_mktoReferrer\";s:48:\"http://go.isqft.com/New-York.html?aliId=48258821\";}"
                },
                {
                    "name": "Query Parameters",
                    "value": "aliId=48258821"
                },
                {
                    "name": "Referrer URL",
                    "value": "http://go.isqft.com/New-York.html?aliId=48258821"
                },
                {
                    "name": "User Agent",
                    "value": "Mozilla/5.0 (iPhone; CPU iPhone OS 8_0_2 like Mac OS X) AppleWebKit/600.1.4 (KHTML, like Gecko) Version/8.0 Mobile/12A405 Safari/600.1.4"
                },
                {
                    "name": "Webpage ID",
                    "value": 4498
                }
            ]
        }
```

### [Campaigns](http://developers.marketo.com/rest-api/endpoint-reference/lead-database-endpoint-reference/#!/Campaigns/getCampaignsUsingGET)
List all campaign records (Returns all campaign records, active or inactive)

**Sample request:**
```
https://541-SJO-620.mktorest.com/rest/v1/campaigns.json?access_token=<TOKEN>
```
**Sample response:**
```
{
    "requestId": "1327f#15f496cd5da",
    "result": [
        {
            "id": 1021,
            "name": "Fills out Form",
            "description": " ",
            "type": "trigger",
            "workspaceName": "Default",
            "createdAt": "2013-02-28T23:22:56Z",
            "updatedAt": "2014-10-06T13:50:12Z",
            "active": false
        },
        {
            "id": 1023,
            "name": "Visits Key Web Page",
            "description": " ",
            "type": "trigger",
            "workspaceName": "Default",
            "createdAt": "2013-02-28T23:22:57Z",
            "updatedAt": "2017-02-08T19:56:33Z",
            "active": false
        }
],
    "success": true,
    "nextPageToken": "MWRJ3IIXQAHBHAGM7CKL5A62GE======"
}
```

### [Leads](http://developers.marketo.com/rest-api/endpoint-reference/lead-database-endpoint-reference/#!/Leads/getLeadsByFilterUsingGET)

#### [Describe leads](http://developers.marketo.com/rest-api/endpoint-reference/lead-database-endpoint-reference/#!/Leads/describeUsingGET_2)

**Sample request:**
```
https://541-SJO-620.mktorest.com/rest/v1/leads/describe.json?access_token=<TOKEN>
```

**Sample response:**
```
{
    "requestId": "113b#15f4971b10c",
    "result": [
        {
            "id": 2,
            "displayName": "Company Name",
            "dataType": "string",
            "length": 255,
            "rest": {
                "name": "company",
                "readOnly": false
            },
            "soap": {
                "name": "Company",
                "readOnly": false
            }
        },
        {
            "id": 3,
            "displayName": "Site",
            "dataType": "string",
            "length": 255,
            "rest": {
                "name": "site",
                "readOnly": false
            },
            "soap": {
                "name": "Site",
                "readOnly": false
            }
        },
        {
            "id": 4,
            "displayName": "Billing Address",
            "dataType": "text",
            "rest": {
                "name": "billingStreet",
                "readOnly": false
            },
            "soap": {
                "name": "BillingStreet",
                "readOnly": false
            }
        },
        {
            "id": 5,
            "displayName": "Billing City",
            "dataType": "string",
            "length": 255,
            "rest": {
                "name": "billingCity",
                "readOnly": false
            },
            "soap": {
                "name": "BillingCity",
                "readOnly": false
            }
        }
],
    "success": true
}
```

### [Bulk Lead Extract](http://developers.marketo.com/rest-api/bulk-extract/bulk-lead-extract/)

**Create a bulk job**

Sample request:
```
POST /bulk/v1/leads/export/create.json
```
Body:
```
 {   "fields": [      "firstName",      "lastName",      "id",      "email"   ],   "format": "CSV",   "columnHeaderNames": {      "firstName": "First Name",      "lastName": "Last Name",      "id": "Marketo Id",      "email": "Email Address"   },   "filter": {      "createdAt": {         "startAt": "2017-01-01T00:00:00Z",         "endAt": "2017-01-30T00:00:00Z"      }   }}

```

Sample response:
```
{   "requestId": "e42b#14272d07d78",   "success": true,   "result": [      {         "exportId": "ce45a7a1-f19d-4ce2-882c-a3c795940a7d",         "status": "Created",         "createdAt": "2017-01-21T11:47:30-08:00",         "queuedAt": "2017-01-21T11:48:30-08:00",         "format": "CSV"      }   ]}
```

**Enqueue Job** (This will start the created job, because that's not automatic.)

Sample request:
```
POST /bulk/v1/leads/export/{exportId}/enqueue.json
```

Sample response:
This will respond with a status of “Queued” after which it will be set to “Processing” when there is an available export slot.

**Polling job status**

Sample request:


Sample response:
```
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "exportId": "ce45a7a1-f19d-4ce2-882c-a3c795940a7d",
         "status": "Processing",
         "createdAt": "2017-01-21T11:47:30-08:00",
         "queuedAt": "2017-01-21T11:48:30-08:00",
         "format": "CSV"
      }
   ]
}
```
````
GET /bulk/v1/leads/export/{exportId}/status.json
```

Retrieving job data

Sample request:
```
GET /bulk/v1/leads/export/{exportId}/file.json
```

**[response.csv.txt](https://github.com/astronomerio/services/files/1407726/response.csv.txt)**

### [Programs](http://developers.marketo.com/rest-api/assets/programs/)

#### Programs by Data Range
**Sample request:**
```
GET /rest/asset/v1/programs.json?earliestUpdatedAt=2015-11-18T00:00:00Z+0000&latestUpdatedAt=2015-11-19T00:00:00Z+0000
```

**Sample request:**
```
{    "success": true,    "warnings": [],    "errors": [],    "requestId": "7a39#1511bf8a41c",    "result": [        {            "id": 1035,            "name": "clone it",            "description": "",            "createdAt": "2015-11-18T15:25:35Z+0000",            "updatedAt": "2015-11-18T15:25:46Z+0000",            "url": "https://app-devlocal1.marketo.com/#NP1035A1",            "type": "Engagement",            "channel": "Nurture",            "folder": {                "type": "Folder",                "value": 28,                "folderName": "Nurturing"            },            "status": "on",            "workspace": "Default"        },        {            "id": 1032,            "name": "email prog",            "description": "",            "createdAt": "2015-11-18T14:56:28Z+0000",            "updatedAt": "2015-11-18T14:56:28Z+0000",            "url": "https://app-devlocal1.marketo.com/#EBP1032A1",            "type": "Email",            "channel": "Email Send",            "folder": {                "type": "Folder",                "value": 26,                "folderName": "Data Management"            },            "status": "unlocked",            "workspace": "Default"        }    ]}
```

### [Staticlists](http://developers.marketo.com/rest-api/endpoint-reference/lead-database-endpoint-reference/#!/Static_Lists/getLeadsByListIdUsingGET)

**List of lists:**

**Sample request:**
```
https://541-SJO-620.mktorest.com/rest/v1/lists.json?access_token=<TOKEN>
```

**Sample response:**
```
{
    "requestId": "1830f#15f49e770d7",
    "result": [
        {
            "id": 1034,
            "name": "Bluehornet Bounces",
            "workspaceName": "Default",
            "createdAt": "2013-03-25T18:48:01Z",
            "updatedAt": "2013-05-21T22:09:25Z"
        },
        {
            "id": 1035,
            "name": "Bluehornet Opt-Out",
            "workspaceName": "Default",
            "createdAt": "2013-03-25T19:38:10Z",
            "updatedAt": "2013-04-01T14:48:55Z"
        },
        {
            "id": 1079,
            "name": "Imcomplete Profile 2013-04",
            "workspaceName": "Default",
            "createdAt": "2013-04-04T13:20:22Z",
            "updatedAt": "2013-04-15T20:28:42Z"
        }
    ],
    "success": true,
    "nextPageToken": "JLZMTQW6MQ23DDJ5H2FAPK4MEY======"
}
```

**Person records from static lists (passing in list id with each request)**
Additional parameter: **fields** (Comma-separated list of lead fields to return for each record. If unset will return email, updatedAt, createdAt, lastName, firstName and id)

**Sample request:**
```
https://541-SJO-620.mktorest.com/rest/v1/list/57777/leads.json?access_token=ad06332d-ceaf-49f7-91df-092394f2a378:sj
```

**Sample response:**
```
{
    "requestId": "1368e#15f49ead0ae",
    "result": [
        {
            "id": 238533,
            "updatedAt": "2017-10-19T14:20:50Z",
            "lastName": "CLARKE",
            "email": "sales@fake.com",
            "createdAt": "2013-03-11T04:26:07Z",
            "firstName": "PETER"
        },
        {
            "id": 262512,
            "updatedAt": "2017-10-18T20:23:43Z",
            "lastName": "Bisson",
            "email": "fake@yahoo.com",
            "createdAt": "2013-03-11T06:38:32Z",
            "firstName": "Richard"
        }
    ],
    "success": true,
    "nextPageToken": "PS5VL5WD4UOWGOUCJR6VY7JQOYHUSZXFAIXVQSVBTJW7Q23CCGZZ7QMV5UITS6VRTX4WNM6GIO5NI==="
}
```

## Roadmap
 - FTP
 - [HootSuite](https://developer.hootsuite.com/docs/api-overview)
 - Kissmetrics
 - MongoDB
 - MySQL
 - New Relic
 - Oracle
 - Pig
 - Pinterest
 - PostgreSQL
 - Presto
 - S3
 - Samba
 - Sengrid
 - Stripe
 - SurveyMonkey
 - Twilio
 - Zendesk

## Destinations:

- S3 (LINK)
- MongoDB (LINK)
- FTP (LINK)
- MySQL (LINK)
- Postgres (LINK)

## Operators
- MongoDB to S3 (LINK)
- FTP to S3 (LINK)
- Salesforce to S3 (LINK)

