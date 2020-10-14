---
layout: page
title: Disabling Packet Filters
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

Version 2.0-alpha3 of the LOCKSS system requires, in the short term, disabling the host operating system's `iptables`, `firewalld` or `ufw` packet filters. *See the [Security Considerations](../introduction/security) section for more about this short-term requirement.*

## Disabling `firewalld`

By default, **CentOS** comes with `firewalld`. To stop and disable it, type these commands:

```bash
sudo systemctl stop firewalld

sudo systemctl disable firewalld
```

You can verify that `firewalld` is not running with:

```bash
sudo firewall-cmd --state
```

You can re-enable and restart `firewalld` if needed with:

```bash
sudo systemctl enable firewalld

sudo systemctl start firewalld
```

## Disabling `ufw`

By default, **Ubuntu** comes with `firewalld`. To stop and disable it, type these commands:

```bash
sudo systemctl stop ufw

sudo systemctl disable ufw
```

You can verify that `ufw` is not running with:

```bash
sudo ufw status
```

You can re-enable and restart `ufw` if needed with:

```bash
sudo systemctl enable ufw

sudo systemctl start ufw
```
