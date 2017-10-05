---
post_title: Astronomer's Network
nav_title: Astronomer's Network
---

## Overview
In general, Astronomer's topology looks like this

![public-private](/1.0/assets/img/guides/network/public-private-vpc.png)

Inside of a single cloud we have public subnets for hosts that need direct access to the internet like DC/OS master nodes as well as bastion hosts. Behind an additional layer of security is the public subnet. This subnet does not allow for direct access to the internet and only allows incoming connections routed through a bastion host on the public subnet. However for these nodes to have access externally they make use of a NAT (Network Address Translation) gateway that exists on the public subnet to make outgoing requests. The address of the NAT gateway is what our customers need to whitelist to receive messages from our network.

### Quick Reference

Based on the type of service Astronomer is providing, you will need to whitelist one or more of the following IP Addresses:

#### Whitelist for DC/OS
* Staging: 52.6.84.242
* Production: 52.20.96.13

#### Whitelist for Clickstream
* Production: 52.86.240.182
