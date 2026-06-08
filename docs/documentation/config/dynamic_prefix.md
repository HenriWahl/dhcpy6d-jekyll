---
layout: page
title: Dynamic Prefix
permalink: /documentation/config/dynamic_prefix
parent: Configuration
grand_parent: Documentation
---

# Dynamic Prefix

Dynamic prefixes change by e.g. ISPs can be injected into dhcpy6d during runtime.

## Prefix injection

An already running dhcpy6d daemon can be updated with a new changed prefix. Whatever script detects a new prefix may
call the following:

```terminal
dhcpy6d --message "prefix 2001:db8"
```

This call only sends the message to the running dhcpyd and stops after finishing. The prefix snippet will be inserted
wherever there is a **$prefix$** variable used in an address or prefix definition.

## The $prefix$ variable

The **$prefix$** variable will be replaced wherever it appears in an address or prefix definition:

```ini
[address_client]
category = range
range = 1000-1fff
pattern = $prefix$::$range$
```

With the previous example prefix snippet the result will be addresses in the range 2001:db8::1000 to 2001:db8::1fff.

The same applies to prefixes:

```ini
[prefix_client]
category = range
range = 1000-1fff
pattern = $prefix$:$range$::
```

## Important advice

Just keep in mind that the $prefix$ variable is just meant to be a snippet of a whole address or prefix definition and 
not as a whole prefix.
