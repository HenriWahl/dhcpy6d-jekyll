---
layout: page
title: Function
permalink: /documentation/function
parent: Documentation
---

# Function

The most important reason for developing dhcpy6d is the missing MAC address support of RFC 3315 and all available DHCPv6 server implementations. This is a showstopper for IPv6 deployment in dualstack scenario in coexistence with already working DHCP infrastructure.

dhcpy6d solves this problem by keeping track of link local addresses and their related MAC addresses by reading the IPv6 neighbor cache when receiving a request (this obviously works only on local network segments – this mechanism does not allow native DHCPv6 relaying). Any request could be linked to a MAC address which could be used as a key to get configuration information for a distinct client as it used to be in DHCP.

In case the Link Local Address and its MAC are not known yet, dhcpy6d tries to get this information from **neighbor cache**. On Linux it is **accessed natively** since version 0.4, on *BSD the command **/usr/sbin/ndp -a -n** is executed. The neighbor cache looks like this:

\[root@dhcpy6d ~\]# ip -6 neigh
fe80::6403:25cf:5c97:5d41 dev eth0 lladdr 00:18:79:8b:c9:87 REACHABLE
fe80::8def:bc22:19bb:afb2 dev eth0 lladdr 00:31:02:d0:6a:12 REACHABLE
fe80::f9c8:5be3:d7ef:21d7 dev eth0 lladdr 00:17:22:2c:64:d9 REACHABLE
fe80::344c:1409:d01:a646 dev eth0 lladdr 00:40:95:c3:10:c4 REACHABLE
fe80::b40f:6547:df1:2343 dev eth0 lladdr 00:13:ba:7a:b3:37 REACHABLE

If caching of MACs is used this happens at maximum once per unknown client. As one can see in the above example, there are many entries in the neighbor cache which all are added to dhcpy6d’s internal Link Local Address-MAC Address mapping. This means that most clients will already be known and not trigger a new inspection of the neighbor cache. Thus the overhead of calling an external command will not be too big.

If longterm caching of MACs is disabled due to security concerns regarding cache poisoning the neighbor cache gets scanned with every new transaction, which might result in higher load but did not lead to problems yet in tests.

If the client’s Link Local Address and MAC are not yet seen in cache or by the external command call the server sends an answer that does not fit to the expected one. The message is “DHCPv6 StatusCode OK”. The client asks again and the neighbor cache has a chance to get filled with current data.

When the client is identified dhcpy6d assigns it the configured class. Every class has one or more address schemes which are applied to the client.

If the client is unknown it will get either a defined default address, an error message or no answer.

Addresses can be defined following different patterns:

- use **MAC address** as part of address, that might be of use in internal networks
- use certain **range** as in DHCP
- generate a **random address**, that might allow privacy on external connections even if privacy extensions are not enabled on client
- build address using an **internal ID** found in some kind of management database

The general [configuration](https://dhcpy6d.ifw-dresden.de/documentation/config/ "Configuration") is set in a config text file.

Client configuration can be stored in a [client config file](https://dhcpy6d.ifw-dresden.de/documentation/config/client/ "Clients") or in a database (MySQL or SQLite). Databases will fit better in larger environments.

Volatile information like leases and Link-Local-Address-MAC-relations are stored in either MySQL or SQLite database. See [database schemes](https://dhcpy6d.ifw-dresden.de/documentation/sql/ "SQL") for further details.

Despite MAC addresses are important for certain dualstack environments they can be ommited completely. DUIDs or hostnames can be used for identification too.