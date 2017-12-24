---
categories: ["Devops"]
date: "2015-07-05T14:08:41+02:00"
tags: ["debian", "jessie", "wheezy", "update", "upgrade", "apt", "dpkg"]
title: "How to upgrade from Debian 7 Wheezy to Debian 8 Jessie"
---

## Some notes about upgrading from Debian 7 Wheezy to Debian 8 Jessie.

We start by creating some environment variables, that will be useful:

```
$ OLD="wheezy"
$ NEW="jessie"
```

Upgrade your Debian Wheezy to the latest packages:

```
$ apt-get clean
$ apt-get update
$ apt-get upgrade
$ apt-get dist-upgrade
```

Then, update every Apt repository file to Debian Jessie:

```
$ sed -i s/${OLD}/${NEW}/g /etc/apt/sources.list /etc/apt/sources.list.d/*.list
```

Update your packages list:

```
$ apt-get update
```

Before updating the whole system, we start by updating the core Apt packages:

```
$ apt-get install dpkg apt aptitude libc6
```

Then, do a simple upgrade:

```
$ apt-get upgrade
```

If everything looks good, continue with:

```
$ apt-get dist-upgrade
```

Reboot after your system has been upgraded:

```
$ reboot
```

Then check your *"newly"* system:

```
$ cat /etc/debian_version
8.1
```
