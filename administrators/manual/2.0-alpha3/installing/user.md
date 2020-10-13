---
layout: page
title: Creating the `lockss` User
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

The LOCKSS system runs under a system user named `lockss`, who is under a group named `lockss`, and who is capable of using `sudo`. *See the [Security Considerations](../introduction/security) section for more about this short-term requirement.*

<!-- #osversion -->
## How to Do It on CentOS or RHEL

Type these commands:

```bash
sudo useradd --system --user-group --create-home --shell=/bin/false --groups=wheel lockss

sudo passwd lockss
```

By default on CentOS, `sudo` privileges and membership in the `wheel` group are equated. Adjust the above commands accordingly if your CentOS system has `sudo` configured differently.

## How to Do It on Debian or Ubuntu

*FIXME*

Add the user lockss, as root or using sudo. You will be prompted for a password.

```bash
sudo adduser lockss
```

Add user lockss to sudo group.

```bash
sudo usermod -aG sudo lockss
```
