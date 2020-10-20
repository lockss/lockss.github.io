---
layout: page
title: Disabling Packet Filters
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

Version 2.0-alpha3 of the LOCKSS system requires, in the short term, disabling any of the user-friendly wrappers around `iptables`, such as`firewalld` or `ufw`, which can interfere with Kubernetes' iptables manipulations. *See the [Security Considerations](../introduction/security) section for more about this short-term requirement.*

## Disabling `firewalld`

By default, **CentOS**, **OpenSUSE** and **RHEL** come with `firewalld`. You can check whether `firewalld` is running with:

```bash
sudo firewall-cmd --state
```

If it is running, stop and disable it with this command:

```bash
sudo systemctl disable --now firewalld
```

## Disabling `ufw`

By default, **Ubuntu** comes with `ufw`. You can chech wheter that `ufw` is running with:

```bash
sudo ufw status
```

If it is running, stop and disable it with this command:

```bash
sudo systemctl disable --now ufw
```
