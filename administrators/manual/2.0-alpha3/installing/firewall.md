---
layout: page
title: Disabling Packet Filters
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

Version 2.0-alpha3 of the LOCKSS system requires, in the short term, disabling the host operating system's `iptables`, `firewalld` or `ufw` packet filters. *See the [Security Considerations](../introduction/security) section for more about this short-term requirement.*

## How to Do It on CentOS

By default, CentOS comes with `firewalld`. To disable it, type:

```bash
sudo systemctl disable firewalld
```

You can verify that `firewalld` is not running with `sudo firewall-cmd --state`, and you can re-enable `firewalld` if needed with `sudo systemctl enable firewalld`.

## How to Do It on Ubuntu/Debian

*TODO*
