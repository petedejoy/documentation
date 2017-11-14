---
title: Sources
sidebar: platform_sidebar
---

## BambooHR

- _Source Type_: REST API
- _Authentication_: Basic
- _Rate Limit_: N/A

Sample Request:
```
curl -i -u "{API Key}:x" "https://api.bamboohr.com/api/gateway.php/{subdomain}/v1/employees/directory"
```

- **Employees/directory**
`https://api.bamboohr.com/api/gateway.php/{subdomain}/v1/employees/directory`
- **jobInfo** (We can pass in an 'All' parameter to request info for all employees): `https://api.bamboohr.com/api/gateway.php/{subdomain}/v1/employees/all/tables/jobInfo/`
- **employmentStatus** (We can pass in an 'All' parameter to request statuses for all employees):
`https://api.bamboohr.com/api/gateway.php/{subdomain}/v1/employees/all/tables/employmentStatus/`

**Employee Directory sample response:**
```
<directory>
    <fieldset>
        <field id="displayName">Display name</field>
        <field id="firstName">First name</field>
        <field id="lastName">Last name</field>
        <field id="gender">Gender</field>
        <field id="jobTitle">Job title</field>
        <field id="workPhone">Work Phone</field>
        <field id="workPhoneExtension">Work Extension</field>
        <field id="skypeUsername">Skype Username</field>
        <field id="facebook">Facebook URL</field>
    </fieldset>
    <employees>
        <employee id="123">
            <field id="displayName">John Doe</field>
            <field id="firstName">John</field>
            <field id="lastName">Doe</field>
            <field id="gender">Male</field>
            <field id="jobTitle">Customer Service Representative</field>
            <field id="workPhone">555-555-5555</field>
            <field id="workPhoneExtension"/>
            <field id="skypeUsername">JohnDoe</field>
            <field id="facebook">JohnDoeFacebook</field>
        </employee>
    </employees>
</directory>
```

**jobInfo sample response:**
```
<table>
    <row id="1" employeeId="100">
        <field id="date">2010-06-01</field>
        <field id="location">New York Office</field>
        <field id="division">Sprockets</field>
        <field id="department">Research and Development</field>
        <field id="jobTitle">Machinist</field>
        <field id="reportsTo">John Smith</field>
    </row>
    <row id="2" employeeId="100">
        <field id="date">2009-03-01</field>
        <field id="location">New York Office</field>
        <field id="division">Sprockets</field>
        <field id="department">Sales</field>
        <field id="jobTitle">Salesman</field>
        <field id="reportsTo">Jane Doe</field>
    </row>
</table>
```

**employeeStatus sample response:**
```
<?xml version="1.0"?>
<table>
    <row id="3843" employeeId="100">
        <field id="date">2012-02-06</field>
        <field id="employmentStatus">Temp</field>
        <field id="benetracStatus"></field>
        <field id="gusto"></field>
    </row>
    <row id="4882" employeeId="100">
        <field id="date">2012-05-27</field>
        <field id="employmentStatus">Full time</field>
        <field id="benetracStatus"></field>
        <field id="gusto"></field>
    </row>
    <row id="5799" employeeId="100">
        <field id="date">2016-08-19</field>
        <field id="employmentStatus">Terminated</field>
        <field id="benetracStatus"></field>
        <field id="gusto"></field>
    </row>
</table>
```

## Facebook Ads

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
