---
layout: post
title: dhcpy6d 1.0 finally out
date: 2020-04-03 00:31:08
categories: releases
permalink: /dhcpy6d-1-0-finally-out
---

Initially developed internally since 2009, going public in 2012 and now finally in 2020 we proudly present the version 1.0 release. After running reliably for years the time has come.

Meanwhile Python 2 is not supported anymore and so dhcpy6d was ported to Python 3. The port has the side effect that binaries are only provided for Debian 10 and RHEL/CentOS 8. Their older respective versions do not ship an appropriate version of Python, which should be at least of version 3.6. Assuming that the newer OS versions could be safely used already this should be no big problem.

Alternatively a containerized version is planned but not ready yet.

The new version of course comes with new features:

* added EUI64 address category
* added PXE boot support
* added support for fixed prefix per client config
* added address category dns to retrieve client ipv6 from DNS
* added self-creation of database tables
* improved PostgreSQL support
* migrated to Python 3
* code housekeeping
* fixes

Thanks to all [contributors](https://github.com/HenriWahl/dhcpy6d/graphs/contributors)!

Go get your copy at [/download](/download).

PS: The above picture has no relevance for IPv6, DHCPv6 or anything IT-ish. Just displaying something non-viral these days.


