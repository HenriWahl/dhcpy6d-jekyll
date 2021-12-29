---
layout: page
title: About
permalink: /
---

# About

Dhcpy6d is an open source server for DHCPv6, the DHCP protocol for IPv6.  
Its development is driven by the need to be able to use the existing IPv4 infrastructure in coexistence with IPv6. In a dualstack scenario, the existing DHCPv4 most probably uses MAC addresses of clients to identify them. This is not intended by RFC 3315 for DHCPv6, but also not forbidden. Dhcpy6d is able to do so in local network segments and therefore offers a pragmatical method for parallel use of DHCPv4 and DHCPv6, because existing client management solutions could be used further.

At the moment it runs on *BSD, macOS and Linux, tested with Debian 10 and CentOS 8.

Licensed under GPL 2.0.

## Features:

- identifies clients by MAC address, DUID or hostname
- generates addresses randomly, by MAC address, by range, by given ID, as EUI64 or from DNS
- filters clients by MAC, DUID or hostname
- assigns multiple addresses per client
- supports prefix delegation
- calls external scripts to set and remove routes to advertised prefixes
- allows to organize clients in different classes
- stores leases in MySQL, PostgreSQL or SQLite database
- client information can be retrieved from database or textfile
- dynamically updates DNS to Bind
- supports rapid commit
- listens on multiple interfaces
- allows request limits to mitigate brute force

## Documentation:

- [How it works](/documentation/function/)
- [How to configure it](/documentation/config/)
    - [General settings](/documentation/config/general)
    - [Addresses](/documentation/config/addresses/)
    - [Prefixes](/documentation/config/prefixes/)
    - [Classes](/documentation/config/classes/)
    - [Minimal configuration](/documentation/config/minimal/)
    - [Full configuration](/documentation/config/full/)
    - [Clients](/documentation/config/client/)
- [How to create its databases](/documentation/sql/)

## Tested and working clients:

- Windows 7/8/10/2008/2012/2016/2019
- Dibbler
- ISC dhclient
- Wide DHCPv6
- NetworkManager
- dhcpcd
- MacOS X 10.7-10.15
- tested with ~4000 clients
