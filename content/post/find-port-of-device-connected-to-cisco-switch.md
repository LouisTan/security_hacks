+++
categories = ["Netops"]
date = "2015-06-26T22:42:57+02:00"
description = "Finding a device connected to a Cisco switch"
tags = ["cisco", "ios", "network"]
title = "How to find on which port a device is connected to a Cisco Switch"

+++

First, you need to get the MAC address of the device you are looking for.
From a Cisco, if you know th IP of the device, you can query for it's MAC like this:

```
# show ip arp 192.168.0.10
```

Then, display on which port is connected the MAC retrieved:

```
# show mac address-table address 123a.f74d.9999
```

Show info about the port the device is connected to:

```
# show running-config interface f0/1
```

If the info shows that it's connected to another switch (mode trunk), show info about this neighbor device:

```
# show cdp neighbors f0/1 detail
```

Rinse and repeat, as necessary.
