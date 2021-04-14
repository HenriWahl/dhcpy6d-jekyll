---
layout: page
title: Prefixes
permalink: /documentation/config/prefixes
parent: Configuration
grand_parent: Documentation
---

# Prefixes

## Basic prefix options

Prefixes are defined in **[prefix_\<prefix>]** sections. _\<prefix>_ is just an identifier and can be whatever you want. In this example _client_local_ is arbitrarily chosen as type for the prefix:

```ini
[prefix_client_local]
```

Prefixes at the moment only can have one sensible category:

- **range** – generate prefix of given ranges

Every prefix definition therefore needs an **category** option and a **pattern** option for its automatic generation. The dynamic part of the prefix is represented by a placeholder referring to the category and enclosed by **$**:

```ini
category = range
pattern = 2001:db8:$range$::
```

A range need an extra option **range** that defines it. Ranges can range from 0-FFFF and contrary to ranges in addresses need to be part of the network definition. In this example ranges range from 2001:db8:1000::/64 to 2001:db8:1fff::/64.

```ini
[prefix_client]
category = range
range = 1000-1fff
pattern = 2001:db8:$range$::
```

The default prefix length is 64 but can be adjusted too by the **length** option. With a given length of 48 the prefixes will range from 2001:db8:2000::/48 to 2001:db8:4fff::/48.

```ini
[prefix_client]
category = range
range = 2000-4fff
pattern = 2001:db8:$range$::
length = 48
```

## Additional options for prefixes

Addresses can have these additional options:

- **preferred_lifetime**
- **valid_lifetime**

Prefixes will per default have the lifetimes set by [general settings](/documentation/config/general "General"), but **preferred_lifetime** and **valid_lifetime** can be modified:

```ini
preferred_lifetime = 900
valid_lifetime = 1200
```

If the routing to the delegated prefix should be done via the Link Local Address of the requesting host, the option **route_link_local** must be set:

```ini
route_link_local = yes
```