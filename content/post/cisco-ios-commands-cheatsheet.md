+++
categories = ["Netops"]
date = "2015-06-25T22:42:57+02:00"
description = "Various Cisco IOS Commands"
tags = ["cisco", "ios", "network", "cheatsheet"]
title = "Cisco IOS commands cheatsheet"

+++

## Escape sequence

If the console hangs:

```
[Ctrl]+[Shift]+6
```

## Configuration modes

You can view and change the configuration of a Cisco router only while in privileged
mode, and you enter it via the enable command like this:

```
Switch>enable
Switch#
Switch#disable
Switch>
```

You can type logout from either mode to exit the console:

```
Switch>logout
```

## Show various info and details of a switch:

```
# show ip interface brief
# show vlan
# show ip int brief
# show interfaces f0/15 description
# show interfaces description
# show interfaces f0/15 status
# show interfaces status
# show running-config interface Gi0/39
# sh cdp neighbors
# sh cdp neighbors detail
# show cdp entry * protocol
# show cdp entry * version
# show lldp
```


## Manage Configuration

### show running configuration

```
# sh running-config
# sh run
```

Grep from configuration output:

```
#sh run | begin interface
```

### show startup configuration

```
# sh startup-config
# sh start
```

### Wite running configuration to startup configuration

Obsolete:

```
# write memory
# write mem
```

Prefer `copy`, which is more versatile:

```
# copy runnning-config startup-config
# copy run start
```

### Display Configuration history

```
# show configuration history
```

### Backup

#### Manually backup running configuration

```
# copy running-config flash:/running-config.backup
```

### Archive and configure

#### Archive

Start by creating the archive directory that wiil hold the various archive files:

```
#mkdir flash:/archives/
```

#### Configure archive

```
# configure terminal
# archive
# path flash:/archives/$h$t (archive will be saved in /archives dir, with a filename of type HOSTNAME-TIMESTAMP)
# write-memory (auto archive at configuration saving)
# end
```
#### Create an archive from running-config (this doesn't copy running-config to startup-config):

```
# archive config
```

#### Show archives:

```
# show archive
```

### Show archives differences

By default, `differences` sub-command uses running-config and startup-config, so the following commands are equivalent:

```
# show archive config differences
# show archive config differences nvram:startup-config
# show archive config differences system:running-config nvram:startup-config
```

`incremental-diffs` sub-command only compares to running-config, and needs a configuration path as argument:

```
# show archive config incremental-diffs nvram:startup-config
```

You can of course use `incremental-diffs` to compare running-config to any file, an archive...:

```
# show archive config incremental-diffs flash:/archives/Router1-Apr-24-20-43-12.910-4
```

`differences` is more flexible, you can mix and match file,a rchive,...:

```
# show archive config differences flash:/archives/Router1-Apr-24-20-49-35.215-7 flash:/archives/Router1-Apr-24-20-43-12.910-4
# show archive config differences flash:/archives/Router1-Apr-24-20-43-12.910-4 nvram:startup-config
# show archive config differences flash:/archives/Router1-Apr-24-20-43-12.910-4
```

## Rollback

### Manual Rollback of running configuration:

```
# configure replace nvram:startup-config
# configure replace flash:/archives/Router1-Apr-24-20-43-12.910-4 
```

### Auto rollback after n minutes

Auto rollback changes done to running-config in five minutes, from a file...:

```
# configure replace <source-file> force time 5
```

..., or from the terminal:

```
# configure terminal revert timer 5
```

Show the current timer:

```
#show archive config rollback timer
#show clock
```

If things gone wrong, don't wait for the timer to rollback, rollback manually now:

```
# configure revert now
```

If everything ok, cancel timer rollback, and confirm changes made to runnin-config:

```
# configure confirm
```

You still need to write you running-config changes to the startup-config:

```
# copy run start
```

