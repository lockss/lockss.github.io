---
layout: page
title: Creating the lockss User
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

The LOCKSS system runs under a system user named `lockss`, which is in a group named `lockss`, and which is capable of using `sudo`. The 'lockss' user's password will be needed at various points during installation, both by explicit invocations of 'sodu', and in some cases by 'miscrok8s' commands. *See the [Security Considerations](../introduction/security) section for more about this short-term requirement.*

<!-- #osversion -->
## Creating the User on CentOS

Type these commands:

```bash
sudo useradd --system --user-group --create-home --shell=/bin/false --groups=wheel lockss

sudo passwd lockss
```

By default on **CentOS**, `sudo` privileges and membership in the `wheel` group are equated. Adjust the above commands accordingly if your CentOS system has `sudo` configured differently.

## Creating the User on Debian and Ubuntu

Type these commands:

```bash
sudo useradd --system --user-group --create-home --shell=/bin/false --groups=sudo lockss

sudo passwd lockss
```

By default on **Debian** and **Ubuntu**, `sudo` privileges and membership in the `sudo` group are equated. Adjust the above commands accordingly if your CentOS system has `sudo` configured differently.

## Obtaining a shell running as 'lockss'

All commands shown in this document except those that explicitly invoke 'sudo' should be issued from a shell running as the 'lockss' user. Depending on your preference, you may login as 'lockss', or switch to the 'lockss' user with this command:

```bash
sudo -i -u lockss /bin/bash
```
