---
layout: post
title: Debian and RedHat/CentOS stable repositories available
date: 2020-07-27 15:38:27
categories: packaging
permalink: /debian-and-redhat-centos-stable-repositories-available
---

Due to the outdated version of dhcpy6d available at Debian there is now an own dhcpy6d repository available, delivering the latest stable versions of Debian and RedHat/CentOS packages.


It works at least for **Debian 10** and **Ubuntu 20.04**.  
Add the following source to your Debian APT **sources**:


deb /files/repo/stable/debian/ /
Add the **[gpg key](/files/repo/stable/debian/key.gpg)** to your APT keyring:


wget -q -O - /files/repo/stable/debian/key.gpg | apt-key add -
To use the **RedHat/CentOS 8** repository simply add the following to your repository information:


[dhcpy6d-stable]
name=dhcpy6d-stable
baseurl=/files/repo/stable/centos/
gpgcheck=1
gpgkey=/files/repo/stable/centos/RPM-GPG-KEY-dhcpy6d
enabled=1
