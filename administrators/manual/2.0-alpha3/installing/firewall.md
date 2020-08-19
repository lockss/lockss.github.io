---
layout: page
title: Configuring Firewall and Network Access
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

Not all systems have an active firewall.  All unix systems have some support for iptables but newer systems use different firewall software. Microk8s like Kubernetes uses iptables by default to add firewall rules. This page will walk you through modifying your system firewall if it has been configured.

## Overview

This document will aide in modifying existing firewalls to permit microk8s to function.

1.  [Cleaning Up Iptables](#cleaning-up-iptables)
1.  [Modify Firewall Rules](#modify-firewall-rules)
1.  [Additional Documentation](#additional-documentation)

## Cleaning Up Iptables

On a dedicated host machine, it is best to flush your iptables to make certain that their are no blocking entries. While microk8s has no requirement for docker, if you do have docker installed make sure you stop it while flushing iptables.

```bash
sudo systemctl stop docker
sudo microk8s stop
sudo iptables --flush
sudo iptables -tnat --flush
sudo systemctl start docker
sudo microk8s start

sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
```

### Persisting IPtables

Iptables don't persist after reboots. Mircrok8s and docker will add the necessary rules when they are restarted. However, if your iptables contain other rules, you will need to save them.

To save the rules in Debian-based systems, enter:

```bash
sudo /sbin/iptables–save
```
To save the rules in RHEL systems, enter:

```bash
sudo /sbin/service iptables save
```  
 
## Modify Firewall Rules

### UFW: Ubuntu, Debian

The service ufw is enabled by default in Ubuntu.  If you are running ufw make sure to open the following ports by entering the listed commands:

```bash
sudo ufw allow 6443/tcp
sudo ufw allow 2379/tcp
sudo ufw allow 2380/tcp
sudo ufw allow 10250/tcp
sudo ufw allow 10251/tcp
sudo ufw allow 10252/tcp
sudo ufw allow 10255/tcp
sudo ufw allow in on cni0
sudo ufw allow out on cni0
sudo ufw default allow routed
sudo ufw reload
```

### Firewall-Cmd: Centos, RHEL

Firewalld is enabled in CentOS 7+ by default on the front-end. You need to open the following ports by entering the listed commands.

```bash
sudo firewall-cmd --permanent --add-port=6443/tcp
sudo firewall-cmd --permanent --add-port=2379-2380/tcp
sudo firewall-cmd --permanent --add-port=10250/tcp
sudo firewall-cmd --permanent --add-port=10251/tcp
sudo firewall-cmd --permanent --add-port=10252/tcp
sudo firewall-cmd --permanent --add-port=10255/tcp
sudo firewall-cmd --zone=trusted --add-masquerade --permanent
sudo firewall-cmd --zone=trusted --add-interface=cni0 --permanent
sudo firewall-cmd --reload
```

The containers need to access the host filesystem. SELinux needs to be set to permissive mode, which effectively disables its security functions.

```bash
sudo setenforce 0
sudo sed -i ‘s/^SELINUX=enforcing$/SELINUX=permissive/’ /etc/selinux/config
```

## Additional documentation:
	
A complete listing of all ports and the services used by microk8s can be found in the microk8s documentation:

https://microk8s.io/docs/ports.  
