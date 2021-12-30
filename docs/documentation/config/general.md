---
layout: page
title: General
permalink: /documentation/config/general
parent: Configuration
grand_parent: Documentation
---

# General

For a minimal set of options to get dhcpy6d running see [minimal settings](/documentation/config/minimal/).

Boolean settings can be done with 1/0, on/off or yes/no values.

## The Section `[dhcpy6d]`

The section `[dhcpy6d]` in the configuration file contains all general options. This section will be discussed here.

#### Example:

```ini
[dhcpy6d]
```

## General Settings

### Setting `really_do_it`

Let dhcpy6d **really_do_it** and respond to client requests – might be of use for debugging and testing.

#### Example:

```ini
really_do_it = yes
```

### Setting `interface`

The interfaces the server listens on is defined with keyword **interface**. Multiple interfaces have to be separated by spaces or comma.

#### Example:

```ini
interface = eth0 eth1
```

### Setting `exclude_interface`

The interfaces the server does not listen on. Multiple interfaces have to be separated by spaces or comma.
All interfaces not mentioned here will be used for listening. Added in version 1.2.0.

#### Example:

```ini
exclude_interface = eth1
```

### Setting `serverduid`

The server DUID should be configured with **serverduid**. If there is none dhcpy6d creates a new one at every startup. Windows clients might run a little bit wild when server DUID changed. You are free to compose your own as long as it follows [RFC 3315](http://tools.ietf.org/html/rfc3315). Please note that it has to be in hexadecimal format – no octals, no “-“, just like in the example below.  
On Debian/Ubuntu systems when installed as package the DUID is noted in _/etc/default/dhcpy6d_.  
The example here is a DUID-LLT (Link-layer Address Plus Time) even if it should be a DUID-TLL as timestamp comes first. It is composed of DUID-type(LLT=1) + Hardware-type(Ethernet=1) + Unixtime-in-hex + MAC-address what makes a 0001 + 0001 + 11fb5dc9+01023472a6c5 = 0001000111fb5dc901023472a6c5:

#### Example:

```ini
serverduid = 0001000111fb5dc901023472a6c5
```

### Setting `server_preference`

Determines the priority of the server. Setups with failover capability might have use for it. The maximum value is 255 which means highest priority.

#### Example:

```ini
server_preference = 255
```

### Settings `user` and `group`

For security reasons dhcpy6d can be run as non-root user and group. Both IDs can be set with **user** and **group**:

#### Example:

```ini
user = dhcpy6d
group = dhcpy6d
```

### Setting `nameserver`

Nameservers to be replied to request option 23 are defined with **nameserver**. If more than one is needed they have to be separated by spaces or comma.

#### Example:

```ini
nameserver = fd00::53:1 fd00::53:2
```

### Setting `domain`

The domain to be used with FQDN hostnames for option 39.

#### Example:

```ini
domain = example.com
```

### Setting `domain_search_list`

Domain search lists to be used with option 24. If none is given the value of **domain** above is used. Multiple domains have to be separated by space or comma.

#### Example:

```ini
domain_search_list = foo.com bar.com
```

### Setting `ntp_server`

Can be unicast addresses, multicast addresses or FQDNs following RFC 5908 for DHCPv6 option 56.  Multiple NTP servers have to be separated by space or comma.

#### Example:

```ini
ntp_server = 2001:db8::123
```

### Settings `log`, `log_console` and `log_file`

Logging is set by **log**, **log_console** and **log_file**.

* **log** triggers logging.
* **log_console** simply prints log messages on that console where dhcpy6d has been started.
* The logfile defined by **log_file**  has to be created by the user manually in advance before starting the server.

#### Example:

```ini
log = yes
log_console = no
log_file = /path/to/dhcpy6d/log/file
```

### Settings `log_syslog`, `log_syslog_destination` and `log_syslog_facility`

Logging via syslog is possible with **log_syslog** being set. An UDP syslog server may be used if **log_syslog_destination** points to it. Optionally a port other than default 514 can be set when adding **:** to the destination. The default syslog facility is “daemon” but can be set with **log_syslog_facility**.

### Example:

```ini
log_syslog = yes
log_syslog_destination = syslogserver
log_syslog_facility = local1
```

### Setting `log_mac_llip`

Logging of discovered MAC/LLIP pairs of clients might be pretty verbose in larger setups and with disabled MAC/LLIP pair caching, this it is configurable with **log_mac_llip**:

```ini
log_mac_llip = no
```

### Settings `store_config` and `store_file_config`

Configuration of clients can be stored in a file or in a database. The SQL databases MySQL, PostgreSQL and SQLite are supported at the moment, thus possible values are “file”, “mysql” and “sqlite”. To disable any client configuration source it has to be “none”. If **store_config** is set to “file” a file has to be set to get client configuration with **store_file_config**.

#### Example:

```ini
store_config = file
store_file_config = /path/to/client/conf/file
```

### Settings `store_volatile` and `store_sqlite_volatile`

Volatile data like leases and the mapping between Link Local Addresses and MAC addresses can be stored in a MySQL, PostgreSQL or SQLite database, so the possible values for **store_volatile** are “mysql”, “postgresql” and “sqlite”. If set to “sqlite” a SQLite database file must be given.

#### Example:

```ini
store_volatile = sqlite
store_sqlite_volatile = volatile.sqlite
```

### Setting `store_sqlite_config`

If **store_config** is set to “sqlite” a SQLite file must be set as source for client configuration.

#### Example:

```ini
store_config = sqlite
store_sqlite_config = /path/to/sqlite/config/file
```

### Database Settings `store_db_host`, `store_db_db`, `store_db_user` and `store_db_password`

##### Volatile Data

If **store_volatile** is set to “mysql” or “postgresql” the connection data for the according SQL database must be set.

##### Example:

```ini
store_volatile = mysql
store_db_host = localhost
store_db_db = dhcpy6d_db
store_db_user = dhcpy6d_user
store_db_password = dhcpy6d_password
```

#### Client Config Data

If the client configuration should be stored in a MySQL or PostgreSQL database as well, the same database needs to be used. Accordingly the same MySQL or PostgreSQL settings are used and only need to be set once.

###### Example:

```ini
store_config = mysql
store_volatile = mysql
store_db_host = localhost
store_db_db = dhcpy6d_db
store_db_user = dhcpy6d_user
store_db_password = dhcpy6d_password
```

## Client Configuration

The configured clients will be identified by at least one attribute. Attributes are

- MAC
- DUID
- Hostname

### Setting `identification`

Has to be at least one of “mac”, “duid”, “hostname”.

#### Example:

```ini
identification = mac hostname
```
### Setting `identification_mode

If more than one identification attribute has been set, **identification_mode** can be one of “match_all” or “match_some”. The first means that all attributes have to match to identify a client and the latter is more tolerant. This might be interesting if there are some dualboot clients whose MAC addresses match but their DUIDs don’t.

#### Example:

```ini
identification_mode = match_all
```

### Setting `ignore_mac`

If serving only for delivering addresses regardless of classes (e.g. on PPP interface) MACs do not need to be investigated, thus **ignore_mac** can be enabled.

#### Example:

```ini
ignore_mac =yes
```

### Setting `dns_update`

Dhcpy6d allows to update DNS dynamically with **dns_update**. This works at the moment only with Bind DNS, but might be extended to others, maybe via call of an external command.
Here the general settings like which server and credentials are to be used. Details like updates zones belong to address configuration.

#### Example:

```ini
dns_update = yes
```

### Settings `dns_update_nameserver`, `dns_rndc_key` and `dns_rndc_secret`

When connecting to a Bind DNS server its address and RNDC data must be set with **dns_update_nameserver**, **dns_rndc_key** and **dns_rndc_secret**.

#### Example:

```ini
dns_update_nameserver = fd00::53:1
dns_rndc_key = rndc-key
dns_rndc_secret = VDE8dje4sWsd93SKksdkk==
```

### Setting `dns_use_rndc`

Alternatively if no RNDC is used it might be omitted by disabling it via **dns_use_rndc**.

#### Example:

```ini
dns_update_nameserver = fd00::53:1
dns_use_rndc = no
```

### Setting `dns_ignore_client`

Clients may request that they update DNS. If these wishes shall be ignored **dns_ignore_client** is the right switch.

#### Example:

```ini
dns_ignore_client = yes
```

### Setting `dns_use_client_hostname`

For DNS updates dhcpy6d can use the hostname supplied by the client or the one configured for the client in the database, set by **dns_use_client_hostname**.

#### Example:

```ini
dns_use_client_hostname = no
```

### Settings `preferred_lifetime`. `valid_lifetime`, `t1` and `t2`

The various lifetimes an address has can be configured globally for all addresses, but if needed, they could get extra settings. Here are the general **preferred_lifetime**. **valid_lifetime**, **t1** and **t2**.

#### Example:

```ini
preferred_lifetime = 43200
valid_lifetime = 64800
t1 = 21600
t2 = 32400
```

### Setting `information_refresh_time`

The lifetime of information given to clients after an information-request message is set with **information_refresh_time**:

#### Example:

```ini
information_refresh_time = 7200
```
