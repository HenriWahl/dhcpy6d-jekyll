---
layout: page
title: Classes
permalink: /documentation/config/classes
parent: Configuration
grand_parent: Documentation
---

# Classes

## Basic class configuration

Class definition sections start with **\[class_\<class>]**. _\<class>_ is just an identifier and can be whatever you want. Here _clients_ is choosen as class identifier:

```ini
[class_clients]
```

The minimal attribute a class has to have is the definition of the address(es) belonging to it. Addresses are defined in [address](/documentation/config/addresses) sections.

In the class section the keyword for addresses is – surprisingly – **addresses**:

```ini
[class_clients]
addresses = client_local
```

A class can use several address definitions, if clients should have more than one address.

```ini
[class_clients]
addresses = client_local client_global
```

The same procedure applies to the definition of [prefixes](/documentation/config/prefixes). Simply add a **prefixes** line with just one previously defined prefix:

```ini
[class_clients]
prefixes = client_global
```

## Additional options for classes

Each class can have some additional options. These are

- **answer**
- **nameserver**
- **t1**
- **t2**
- **filter_hostname**
- **filter_mac**
- **filter_duid**
- **interface**
- **advertise**
- **call_up**
- **call_down**

Normally a client will get an **answer**, but if for whatever reason is a need to give it an _NoAddrAvail_ message back or completely ignore the client it can be set here. Valid answer types are _normal_, _noaddress_ and _none_:

```ini
[class_to_be_ignored]
answer = none
```

Nameservers can be specified individually for every class. This allows to use different nameservers e.g. for valid and invalid hosts. They are set by **nameserver**. More than one have to be separated by spaces.

```ini
[class_valid]
addresses = valid_global valid_local
nameserver = fd00:0:0:900d::53:1 fd00:0:0:900d::53:2

[class_invalid]  
addresses = invalid  
nameserver = fd00:0:0:bad::53:
```

NTP servers can be defined for every class separately. The **ntp_server** can be unicast addresses, multicast addresses or FQDNs following RFC 5908 for DHCPv6 option 56.

```ini
[class_valid]  
addresses = valid_global valid_local  
ntp_server = 2001:db8::123
```

Every class might have different **t1** and **t2** values. This might make sense for invalid clients which could have shorter refresh cycles to check if they are valid again.

```ini
[class_invalid]
addresses = invalid
t1 = 1200
t2 = 1500
```

Filters allow to configure clients by attributes and not by static configuration information. Filters use [Python regular expressions](https://docs.python.org/3/howto/regex.html). Possible keywords are **filter_hostname**, **filter_duid** and **filter_mac**. If for example all Windows clients hostnames start with _win_ a class could be created to use that information.

```ini
[class_windows]
addresses = valid_local
filter_hostname = win*
```

If multiple interfaces are configured, a class has to belong to at least one **interface**. If none is specified, all interfaces dhcpy6d listens to are used.

```ini
[class_clients]
addresses = clients
interface = eth0

[class_servers]  
addresses = servers  
interface = eth1
```

As default only addresses will be advertised . When only addresses or only prefixes should be used by this class, the option **advertise** defines which ones apply:

```ini
advertise = prefixes
```

When delegating prefixes, somewhere the route into the new prefix subnet has to be set. Either the dhcpy6d host routes too or some remote router does. In either case some external executable has to be called. The same applies when the prefix gets released. For this purposes the options **call_up** and **call_down** exist. Both are freely adjustable and can get the 3 variables _$prefix$_, _$length$_ and _$router$_. The last one contains the IPv6 address of the requesting client:

```ini
call_up = /usr/local/bin/update_route.sh $prefix$ $length$ $router$
call_down = /usr/local/bin/update_route.sh $prefix$ $length$ $router$
```

## Default class

The class _default_ always exists and applies to clients that do not match otherwise. It uses the address _default_ which has to be set in the **[address_default]** section. See [minimal configuration](https://dhcpy6d.ifw-dresden.de/documentation/config/minimal) for example.

If default clients need extra configuration edit **[class_default]**:

```ini
[class_default]
nameserver = fd00::bad:53
```

## Default classes when using multiple interfaces

If dhcpy6d listens on multiple interfaces one default class per interface can be defined. This will be useful to configure several subnets on different segments. A default class definition starts with **[class_default_\<interface>]**, which looks like this:

```ini
[class_default_eth1]
addresses = subnet1

[class_default_eth2]
addresses = subnet2
```

## Example for classes

Clients can be assigned to different classes. Lets assume there are 3 classes:

- known valid clients – class “**valid**“
- known invalid clients, e.g. with invalid antivirus patterns – class “**invalid**“
- unknown clients which per default belong to class “**default**“

Valid clients should get 2 addresses each, one unique local and one global address. The local address will be an ID-based one, the global one a random address for privacy. Let the local addresses be in subnet **fd00:0:0:900d::/64** and the global one in **2001:db8::/64**.

Invalid clients will get only one unique local address based on ID for easier identification of the host. The subnet shall be **fd00:0:0:bad::/64**.

Unknown clients also will get only one unique local address. Their MAC address should be included for easier tracing and the subnet might be **fd00:bad:dead:beef::/64**.

The addresses are defined like this:

```ini
# local address for valid clients  
[address_valid_local]  
category = id
pattern = fd00:0:0:900d::$id$  
  
# global address for valid clients  
[address_valid_global]  
category = random
pattern = 2001:db8::$random64$

# local address for invalid clients
[address_invalid]  
category = id  
pattern = fd00:0:0:bad::$id$  
  
# default address for unknown clients  
# the class "default" exists per default and there is no need  
# to define it here again, only if it needs some special options  
# because it automatically uses this address_default  
[address_default]  
category = mac  
pattern = fd00:bad:dead:beef::$mac$

# class for valid clients  
[class_valid]  
addresses = valid_local valid_global  
  
# class for invalid clients  
[class_invalid]  
addresses = invalid
```