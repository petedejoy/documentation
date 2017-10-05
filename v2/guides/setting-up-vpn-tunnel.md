---
post_title: Setting Up VPN Tunnel
nav_title: Setting Up VPN Tunnel
---

This guide is meant to assist in establishing a host-to-LAN (or host-to-site; or host-to-network) VPN tunnel, in order to securely access data behind an external firewall.

## A few notes to get started:
- Astronomer currently supports host-to-LAN (or host-to-site) VPN tunneling.  We do not have support for site-to-site tunneling.
- Brand appliance
  - If Cisco, a connection profile would need created with the name set to the following Astronomer NAT IP address: 52.54.195.131
  - Instructions for Fortinet appliances coming soon!
- We don’t currently support two-factor authentication for our pipelines, but we are working to make an alternative solution available, i.e. IPSec VPN.

With these clarifications, we would need the following parameters to connect host-to-LAN (or host-to-site):

IP address to firewall (REMOTE_HOST)
The network we're connecting to (REMOTE_SUBNET)
XAuth Pre-shared Key (XAUTH PSK)
IPSec IKE (encryption algorithms)
IPSec ESP (encryption algorithms)
IKE_LIFETIME (how long the tunnel is allowed to stay open)
XAUTH_USER (IPSec ESP authorization)
XAUTH_PASS (IPSec ESP password)


## Communicating Credentials
To communicate the necessary credentials, a 1Password vault will be created with a Secure Note providing the relevant fields to fill out. Only the members of Astronomer assigned to the account will have access to this vault. Once these fields are completed and Implementation Specialist notified, a full turnover with the assigned Implementation Engineer will occur with scope, deadlines and expectations clearly identified.

#### The following steps are only relevant for private installations of Astronomer. If you are using a cloud version of Astronomer, these steps will be taken by your assigned Implementation team.

- Inside of the production MongoDB, in the `connectionConfigs` collection, create a document (`vpnconnection`) with the VPN parameters.  This `vpnconnection` allows Astronomer to connect to databases, APIs, other VPN tunnels, etc.

- Create a separate document (`connectionconfig`) that uses the `vpnconnection` document from Step 2 to establish the tunnel to the thing we’re connecting to. This is an anonymized example of what exists for a current `connectionconfig`:
```
{
    "_id" : ObjectId("58b07b5b14391f41ebbac99e"),
    "updatedAt" : ISODate("2017-02-24T18:28:43.930+0000"),
    "createdAt" : ISODate("2017-02-24T18:28:43.930+0000"),
    "name" : "example-mssql-bistage",
    "code" : "mssql",
    "details" : {
        "server" : "someserver",
        "pool" : {
            "max" : NumberInt(10),
            "min" : NumberInt(2)
        },
        "database" : "somedatabase",
        "password" : "somepassword",
        "user" : "someuser",
        "port" : NumberInt(1433),
        "requestTimeout" : 60000.0
    },
    "vpnConnection" : ObjectId("id of the vpnconnection in Step 2"),
    "__v" : NumberInt(0)
}
```

Create a pipeline that specifies a connection equal to the ID of the `connectionconfig` created in the previous step.  List the connection inside the same block as the “lastExecuted” block, and just after the end of the “config” block:

`"connection" : ObjectId("58b07b5b14391f41ebbac99e")`

To Do:
- Add alternative solution for two-factor support (i.e. IPSec VPN)
