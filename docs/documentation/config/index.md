---
layout: page
title: Configuration
permalink: /documentation/config
parent: Documentation
has_children: true
has_toc: false
---

# Configuration

Configuration consists of two parts. The first is the configuration file that has to be given on commandline:

```terminal
# dhcpy6d -c dhcpy6d.conf
```

The second is either a [client config file](https://dhcpy6d.ifw-dresden.de/documentation/config/client/ "Clients") or a database on a MySQL server or in a SQLite file following the [database schemes](/documentation/sql/ "SQL"). This part is defined in the mentioned config file.

Dhcpy6d source code contains a config-example.conf as well as a clients-example.conf.

To get a SQLite database for volatile storage use the one coming in var/lib/volatile.sqlite or use sqlite commandline client with doc/volatile.sql:

```terminal
# sqlite volatile.sqlite < volatile.sql
```

The latter applies to MySQL databases:

```terminal
# mysql dhcpy6d < config.sql
# mysql dhcpy6d < volatile.sql
```

General and client configuration files are in RFC 822 style parsed by [Python ConfigParser](http://docs.python.org/2/library/configparser.html) module.

The general configuration file consists of 4 types of sections:

- **[dhcpy6d]** – general settings
- **[address_<address>]** – definition of one _<address>_ type, there can be many of
- **[prefix_\<prefix>]** – definition of one _\<prefix>_ type, there can be many of
- **[class_\<class>]** – definition of _\<class>_ of clients, also several are allowed, refers to address and prefix definitions

Find more information about these sections here:

- [General configuration](https://dhcpy6d.ifw-dresden.de/documentation/config/general/ "General")
- [Addresses](https://dhcpy6d.ifw-dresden.de/documentation/config/addresses/ "Addresses")
- [Prefixes](https://dhcpy6d.ifw-dresden.de/documentation/config/prefixes/)
- [Classes](https://dhcpy6d.ifw-dresden.de/documentation/config/classes/ "Classes")

See some example configuration files:

- [Minimal necessary](https://dhcpy6d.ifw-dresden.de/documentation/config/minimal/ "Minimal")
- [Full configuration](https://dhcpy6d.ifw-dresden.de/documentation/config/full/ "Full") to show all options

If clients are configured in a file instead of a database it might look like this:

- [Client configuration file](https://dhcpy6d.ifw-dresden.de/documentation/config/clients/ "Clients")