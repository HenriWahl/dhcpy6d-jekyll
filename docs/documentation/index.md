---
layout: page
title: Documentation
permalink: /documentation
has_children: true
has_toc: false
---

# Documentation

These pages should give you an overview of various aspects of dhcpy6d:

- [How it works](/documentation/function "Function")
- [How to install it](/documentation/installation "Installation")
- [How to configure it](/documentation/config/ "Configuration")
    - [General settings](/documentation/config/general/ "General")
    - [Addresses](/documentation/config/addresses/ "Addresses")
    - [Classes](/documentation/config/classes/ "Classes")
    - [Prefixes](/documentation/config/prefixes/)
    - [Minimal configuration](/documentation/config/minimal/ "Minimal")
    - [Full configuration](/documentation/config/full/ "Full")
    - [Clients](/documentation/config/client/ "Clients")
- [How to create its databases](/documentation/sql/ "SQL")
- [How to configure the router](/documentation/router-configuration/ "Router configuration")
- [Manual pages](/documentation/manpages/ "Manpages")

## Supported DHCPv6 Options

The following DHCPv6 options used by clients and servers are supported at the moment. If not stated otherwise these options are described in [RFC 3315](http://tools.ietf.org/html/rfc3315). This list is intended to grow.

- 1 – Client Identifier Option
- 2- Server Identifier Option
- 3 – Identity Associaton for Non-temporary Addresses Option
- 4 – Identity Association for Temporary Address Option
- 5 – IA Address Option
- 6 – Option Request Option
- 7 – Preference Option
- 12 – Server Unicast Option
- 13 – Status Code Option
- 14 – Rapid Commit Option
- 16 – Vendor Class Option
- 23 – DNS Recursive Nameserver Option
- 24 – Domain Search List
- 32 – Information Refresh Time
- 39 – Client FQDN Option
- 56 – NTP Server Option