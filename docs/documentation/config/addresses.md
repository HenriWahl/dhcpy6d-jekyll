---
layout: page
title: Function
permalink: /documentation/config/addresses
parent: Configuration
---

# Addresses

## Basic address options

Addresses are defined in **[address_<address>]** sections. _<address>_ is just an identifier and can be whatever you want. In this example _client_local_ is arbitrarily chosen as type for the address:

```
[address_client_local]
```

Addresses belong to one of these categories:

- **mac** – uses MAC address from client request as part of address
- **id** – uses ID given to client in configuration file or database as one octet of address, should be in range 0-FFFF
- **range** – generate addresses of given ranges
- **random** – created randomly
- **fixed** – use only fixed addresses from client configuration
- **dns** – get address from DNS

These will discussed in the following paragraphs.

Every address definition therefore needs an **category** option and a **pattern** option for its automatic generation. The dynamic part of the address is represented by a placeholder referring to the category and enclosed by **$**:

category = some_category
pattern = 2001:db8::$some_category$

If an address should include the client MAC address transformed into 3 octets like 01:02:03:04:05:06 to fd00::0102:0304:0506 it belongs to category **mac**. Its definition is:

\[address_client\]
category = mac
pattern = fd00::$mac$

If clients have some IDs configured as attribute this ID can be used in the address. A client with ID 1000 will get the address 2001:db8::1000 when category **id** is defined like this:

\[address_client\]
category = id
pattern = 2001:db8::$id$

Addresses can be given in ranges too. If this option is used there is an extra option **range** that defines one. Ranges can range from 0-FFFF and form the last octet of an IPv6 address. Addresses from this example range from 2001:db8::1000 to 2001:db8::1fff.

\[address_client\]
category = range
range = 1000-1fff
pattern = 2001:db8::$range$

As privacy measure clients can get random addresses. At the moment the generated random part takes the whole 64 bit of the host identifier part of the address. Therefore the placeholder for category **random** is **$random64$** – there might be shorter ones in the future. The resulting address looks like 2001:db8::349a:49f2:9dc2:b3a0.

\[address_global\]
category = random
pattern = 2001:db8::$random64$

If addresses should not be created dynamically, but fixed, just use the **fixed** category. Addresses then must be supplied in clients configuration file or database:

\[address\_local\_fixed\]
category = fixed

If addresses should be managed centrally by your DNS they can be obtained by DNS queries instead of being generated or configured with the **dns** category. Therefore a nameserver has to be configured in global dhcpy6d options:

\[address\_from\_dns\]
category = dns

If  the –prefix argument is used when calling dhcpy6, one can use the $prefix$ variable in a pattern definition, which will be substituted by the given prefix. This might be especially usefull when using changing prefixes given by an ISP:

\[address\_global\_dynamic\]
category = random
pattern = $prefix$::$random64$

## Additional options for addresses

Addresses can have these additional options:

- **ia_type**
- **preferred_lifetime**
- **valid_lifetime**
- **dns_update**
- **dns_zone**
- **dns\_rev\_zone**

IA type of most addresses will be non-temporary – “na”. If temporary addresses are expected to be requested by clients **ia_type** can be set to temporary “ta”:

ia_type = ta

Addresses will per default have the lifetimes set by [general settings](https://dhcpy6d.ifw-dresden.de/documentation/config/general/ "General"), but **preferred_lifetime** and **valid_lifetime** can be modified:

preferred_lifetime = 900
valid_lifetime = 1200

If DNS should be updated the flag **dns_update** has to be set true. At the moment this only works for Bind DNS servers which must be configuref in [general settings](https://dhcpy6d.ifw-dresden.de/documentation/config/general/ "General").

dns_update = yes

For DNS updates the zones to update have to be set as configured in DNS. The zone information is set by **dns_zone** and **dns\_rev\_zone**:

dns_zone = example.com
dns\_rev\_zone = 0.0.d.f.ip6.arpa