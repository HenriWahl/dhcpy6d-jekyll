---
layout: page
title: Installation
permalink: /documentation/installation
parent: Documentation
---

# Installation

To get dhcpy6d running some requirements have to be fulfilled. On a Linux installation the package names may vary but will be similar to those on Debian and Redhat/CentOS:

- **Python** from [http://www.python.org](http://www.python.org)
    - **Python3** comes as default on Debian 10 and Redhat/CentOS 8
    - **python-3.8.6p0** on OpenBSD 6.8
    - **python39** on FreeBSD and NetBSD

- **dnspython** from [http://www.dnspython.org](http://www.dnspython.org)
    - **python3-dnspython** in Debian
    - **python3-dns** in Redhat/CentOS 
    - **py3-dnspython** in OpenBSD
    - **py39-dnspython** in FreeBSD
    - **py39-dns** in NetBSD

- **PyMySQL** from [https://pypi.org/project/PyMySQL/](https://pypi.org/project/PyMySQL/) or py
    - **python3-mysqldb** in Debian
    - **python3-PyMySQL** in Redhat/CentOS
    - **py3-pymysql** in OpenBSD
    - **py39-pymysql** in FreeBSD
    - **py39-pymysql** in NetBSD

- SQLite support in FreeBSD and NetBSD needs additional **py39-sqlite3** package

- Optional: sqlite commandline client
    - **sqlite3** in Debian and *BSD
    - **sqlite** in Redhat/CentOS