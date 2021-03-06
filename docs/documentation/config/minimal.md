---
layout: page
title: Minimal options
permalink: /documentation/config/minimal
parent: Configuration
grand_parent: Documentation
---

# Minimal Options

This is an example config file including the minimum necessary options:

```ini
# dhcpy6d minimal example configuration

[dhcpy6d]
# Interface to listen to multicast ff02::1:2.
interface = eth1
# Do not identify and configure clients.
store_config = none
# SQLite DB for leases and LLIP-MAC-mapping.
store_volatile = sqlite
store_sqlite_volatile = volatile.sqlite
# Not really necessary but might help for debugging.
log = on
log_console = on

# Special address type which applies to all not specially
# configured clients.
[address_default]
# Choosing MAC-based addresses.
category = mac
# ULA-type address pattern.
pattern = fd01:db8:dead:bad:beef:$mac$
```
