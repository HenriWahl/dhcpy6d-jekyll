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

The second is either a [client config file](/documentation/config/client) or a database on a MySQL or PostgreSQL server or in a SQLite file following the [database schemes](/documentation/sql). This part is defined in the mentioned config file.

Dhcpy6d source code contains a [dhcp6d-example.conf](https://github.com/HenriWahl/dhcpy6d/blob/master/doc/dhcpy6d-example.conf) as well as a [clients-example.conf](https://github.com/HenriWahl/dhcpy6d/blob/master/doc/clients-example.conf).

Since version 1.0 the volatile leases database is created **automatically**, so you would need the following steps only for the configuration database.

To get a SQLite database for volatile storage use the one coming in var/lib/volatile.sqlite or use sqlite commandline client with doc/volatile.sql:

```terminal
# sqlite volatile.sqlite < volatile.sql
```

The latter applies to MySQL databases:

```terminal
# mysql dhcpy6d < config.sql
# mysql dhcpy6d < volatile.sql
```

General and client configuration files are in RFC 822 style parsed by [Python ConfigParser](http://docs.python.org/3/library/configparser.html) module.

The general configuration file consists of 4 types of sections:

- **[dhcpy6d]** – general settings
- **[address_<address>]** – definition of one _<address>_ type, there can be many of
- **[prefix_\<prefix>]** – definition of one _\<prefix>_ type, there can be many of
- **[class_\<class>]** – definition of _\<class>_ of clients, also several are allowed, refers to address and prefix definitions

Find more information about these sections here:

- [General configuration](/documentation/config/general)
- [Addresses](/documentation/config/addresses)
- [Prefixes](/documentation/config/prefixes)
- [Classes](/documentation/config/classes)

See some example configuration files:

- [Minimal necessary](/documentation/config/minimal)
- [Full configuration](/documentation/config/full) to show all options

If clients are configured in a file instead of a database it might look like this:

- [Client configuration file](/documentation/config/clients)