+++
categories = ["Netops"]
date = "2015-06-24T21:42:57+02:00"
description = "Various Junos Commands"
tags = ["juniper", "junos", "network", "cheatsheet"]
title = "Juniper Junos commands cheatsheet"

+++

## Modes

### Operational mode: 

Manage and monitor device operations. For
example, monitor the status of the device interfaces, check chassis
alarms, and upgrade and downgrade the device’s operating
system.

#### Configuration mode

Configure the device and its interfaces. These
include user access, interfaces, protocols, security services, and
system hardware properties


## File listing

Listing your homedir:
```
> file list
```

Show the content of a file in your homedir:
```
> file show router-config-150601
```

## Various commands to show info and details
```
> show interfaces terse
> show interfaces descriptions
> show interfaces detail
> show route descriptions
> show route detail
> show route terse
```

## Manage configuration / backup / restore

Active configuration: currently running configuration.

Candidate configuration: modified configuration that needs to be
commited to become the candidate configuration.

### Show candidate configuration

```
# show
```

### Show active configuration

```
# show configuration
# show configuration | display detail
```

### Manually backup candidate configuration in your homedir

```
# save router-config-150601
```

### Manually backup active configuration in your homedir

```
# run show configuration | save Tuesday-archive
```

### Copy the current active configuration file (/config/juniper.conf.gz) as backup.gz to the device’s /var/home/user directory:

```
# file copy /config/juniper.conf.gz /var/home/user/backup.gz
```

### Create a rescue configuration of a known working configuration.

If the active configuration is corrupted, the device will automatically load the filenamed rescue.gz
in the ```/config``` directory as the active configuration:

```
# file copy /config/juniper.conf.gz /config/rescue.gz
```

### Define a remote backup host:

```
# set system archival configuration archive-sites ftp://jadmin:password@remote/archives
```

### Auto backup of configuration once a day (1440 minutes) to remote backup machine:

```
# set system archival configuration transfer interval 1440
```

## Auto backup of configuration to remote backup machine on every commit:

```
# set system archival configuration transfer-on-commit
```

### Completely replace the current candidate configuration with a previously stored file. 

You must enter the load override command from the top of the configuration mode:

```
# load override /var/tmp/router-config
# commit
```

### Apply some configuration snippets:

#### From a file:

```
# load merge partial-conf.txt
# commit
```

#### From terminal:

```
# load merge terminal
[Type ^D at a new line to end input]
...
# commit
```

### Check configuration before a commit:

```
# commit check
```

### Commit candidate version

```
# commit
```

### Commit candidate version during X minutes

You need to confirm with a ```commit```, or modification will be rollback after X minutes.

```
# commit confirmed X
```

### Show pending auto commits (and commits history):

```
# show system commit
```

### Auto commit at a particular time:

```
# commit at 02:00:00
# show system commit
```

### Delete pending auto commit:

```
> clear system commit
```

### Rollback

#### Show rollabcks

```
# rollback ?
```

#### Compare active config with rollback X

```
# show | compare rollback X
```

#### Compare candidate config with active configuration

```
# show  | compare
```

```rollback 0``` references the active configuration, so the following command is equivalent to the previous one:

```
# show  | compare
```

#### Replace candidate configuration with rollback X:

We start by loading rollback X

```
# rollback X
```

Checking everything is fine

```
# show
# show | compare
```

If everything is fine:

```
# commit
```
