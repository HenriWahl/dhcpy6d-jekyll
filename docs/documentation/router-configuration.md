---
layout: page
title: Router Configuration
permalink: /documentation/router-configuration
parent: Documentation
---

# Router configuration

In order to cooperate flawlessly with dhcpy6d your router has to advertise the correct information in its [Router Advertisement](https://en.wikipedia.org/wiki/Neighbor_Discovery_Protocol) messages. It **must** announce the M-flag (managed) and **must not** deliver any prefix information to the clients.

A working radvd.conf for the [radvd daemon](http://www.litech.org/radvd/) looks like this:

```conf
interface eth0 {
AdvSendAdvert on;
AdvManagedFlag on;
};
```

An interface configuration on [Cisco IOS](http://www.cisco.com/en/US/products/ps6537/products_ios_sub_category_home.html) should at least contain these lines:

```terminal
ipv6 nd prefix 2001:db8::/64 no-advertise
ipv6 nd managed-config-flag
```