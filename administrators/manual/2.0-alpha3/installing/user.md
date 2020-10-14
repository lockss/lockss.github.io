---
layout: page
title: Creating the lockss User
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

The LOCKSS system runs under a system user named `lockss`, who is under a group named `lockss`, and who is capable of using `sudo`. *See the [Security Considerations](../introduction/security) section for more about this short-term requirement.*

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
