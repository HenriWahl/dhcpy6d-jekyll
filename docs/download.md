---
layout: page
title: Download
permalink: /download
---

# Download

**Stable source** and **binary** packages for **Debian** and **Redhat/CentOS** are available at **[GitHub](https://github.com/HenriWahl/dhcpy6d/releases/tag/v1.0.7)**.

The current development version is available at **[GitHub latest](https://github.com/HenriWahl/dhcpy6d/releases/tag/latest)**.

## Debian repository

This Debian repository works at least for **Debian 10** and **Ubuntu 20.04**.  
Add the following source to your Debian APT **sources**:

```
deb https://dhcpy6d.de/repo/stable/debian/ /
```

Add the **[gpg key](https://dhcpy6d.de/repo/stable/debian/key.gpg)** to your APT keyring:

```terminal
# wget -q -O - https://dhcpy6d.de/repo/stable/debian/key.gpg | apt-key add -
```

After updating APT the latest stable version of dhcpy6d is ready to install:

```terminal
# apt update
# apt install dhcpy6d
```

## RedHat/CentOS repository

To use the **RedHat/CentOS 8** repository simply add the following to your repository information:

```ini
[dhcpy6d-stable]
name=dhcpy6d-stable
baseurl=https://dhcpy6d.de/repo/stable/centos/
gpgcheck=1
gpgkey=https://dhcpy6d.de/repo/stable/centos/RPM-GPG-KEY-dhcpy6d
enabled=1
```

Now dhcpy6d can be installed:

```terminal
# dnf install dhcpy6d
```

## GitHub repository

The **git repository** is hosted at GitHub at [https://github.com/HenriWahl/dhcpy6d](https://github.com/HenriWahl/dhcpy6d).

Get your clone:

```terminal
# git clone https://github.com/HenriWahl/dhcpy6d.git dhcpy6d
```