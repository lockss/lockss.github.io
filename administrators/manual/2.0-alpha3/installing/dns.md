---
layout: page
title: Downloading the LOCKSS Installer
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

After MicroK8s is up and running, adjustments need to be made to the MicroK8s DNS settings. In this section, you will first make use of the LOCKSS Installer you downloaded from GitHub a few sections ago. While in the `lockss-installer` directory and as the `lockss` user, run the following script:

```bash
scripts/configure-dns
```

You may be prompted for the `lockss` password for `sudo`, and under some circumstances, you may be prompted for a semicolon-separated list of IP addresses of upstream DNS servers your host machine should use.

Successful output from a run not requiring IP addresses of upstream DNS servers will look something like the following:

```text
Enabling DNS
Applying manifest
serviceaccount/coredns created
configmap/coredns created
deployment.apps/coredns created
service/kube-dns created
clusterrole.rbac.authorization.k8s.io/coredns created
clusterrolebinding.rbac.authorization.k8s.io/coredns created
Restarting kubelet
DNS is enabled
[2020-10-12T15:48:55-0700]: configure-dns:Updating  CoreDNS ConfigMap to use /etc/resolv.conf...
configmap/coredns configured
[2020-10-12T15:48:56-0700]: --------------------------------------------------------------------
[2020-10-12T15:48:56-0700]: configure-dns:  Successfully changed CoreDNS ConfigMap
[2020-10-12T15:48:56-0700]: --------------------------------------------------------------------
```

## Frequently Asked Questions

**Under what circumstances will IP addresses of upstream DNS servers be needed?**

If your system is such that DNS resolution includes a loopback address, `configure-dns` will need to prompt you for a semicolon-separated list of IP addresses of upstream DNS servers. This can happen if `/etc/resolv.conf` or `/run/systemd/resolve/resolv.conf` (if your system uses `systemd-resolved`) contain `nameserver` lines for `localhost`, `::1`, `127.0.0.1`, or other loopback addresses.
