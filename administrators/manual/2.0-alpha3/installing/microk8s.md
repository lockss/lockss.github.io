---
layout: page
title: Installing Kubernetes with Microk8s
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

[Microk8s](https://microk8s.io/) is the smallest, fastest, fully-conformant Kubernetes that tracks upstream releases and makes clustering trivial. This page will walk you through the initial installation of Microk8s. 
## Overview

To install Microk8s for the purposes of running the LOCKSS system:

1.  [Install Microk8s](#install-microk8s)
1.  [Join the Group](#join-the-group)
1.  [Check the Status](#check-the-status)
1. 	 [Enable DNS](#enable-dns)
1.  [Setup Users Kubectl Config](#setup-users-kubectl-config)
1.  [Setup Alias](#setup-alias)
1.  [Access Kubernetes](#access-kubernetes)
1.  [Starting and Stopping](#starting-and-stopping)

The LOCKSS system requires **Microk8s 1.18 or better**.

## Install Microk8s

```bash
    sudo snap install microk8s --classic --channel=1.18/stable
```

## Join the Group
MicroK8s creates a group to enable usage of commands which require admin privilege. To add your current user to the group and gain access to the .kube caching directory, run the following two commands:

```bash
    sudo usermod -a -G microk8s $USER
    sudo chown -f -R $USER ~/.kube
```

You  need to re-enter the session for the group update to take place:

```bash
    su - $USER
```

## Check the Status
During installation, you can use the --wait-ready flag  on the status command to wait for the Kubernetes services to initialise:

```bash
     microk8s status --wait-ready
```
```text
	microk8s is running
	addons:
	dashboard: disabled
	dns: disabled
	metrics-server: disabled
	ambassador: disabled
	cilium: disabled
	fluentd: disabled
	gpu: disabled
	helm: disabled
	helm3: disabled
	host-access: disabled
	ingress: disabled
	istio: disabled
	jaeger: disabled
	knative: disabled
	kubeflow: disabled
	linkerd: disabled
	metallb: disabled
	multus: disabled
	prometheus: disabled
	rbac: disabled
	registry: disabled
	storage: disabled
```

## Configure Firewall

### Clean up existing iptables.

On a dedicated host machine it is best to flush your iptables to make certain that their are no blocking entries. While microk8s has no requirement for docker, if you do have docker installed make sure you stop it while flushing iptables.

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
Your iptables won't persist after reboots. 

To save the rules in Debian-based systems, enter:

```bash
sudo /sbin/iptables–save
```

To save the rules in RHEL systems, enter:

```bash
sudo /sbin/service iptables save
```  
 
### Modify any existing firewall rules to open the correct ports.

Ubuntu, Debian

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

Centos, RHEL

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

## Enable DNS
To be as lightweight as possible, MicroK8s only installs the basics of a usable Kubernetes install:

    * api-server
    * controller-manager
    * scheduler
    * kubelet
    * cni
    * kube-proxy

To run LOCKSS you will need to enable dns.  If you machine is behind a firewall you will first need to allow access through the firewall. See the firewall documentation for instructions.

```bash
    sudo microk8s enable dns    
```

By default it points to Google’s 8.8.8.8 and 8.8.4.4 servers for resolving
addresses. This can be changed by running the command:

```bash
	microk8s kubectl -n kube-system edit configmap/coredns
```

This will invoke the vim editor so that you can alter the configuration.

## Setup Users Kubectl Config

If you don’t have an existing install or ~/.kube directory

```bash
    mkdir -p ~/.kube
    microk8s config > ~/.kube/config
```

If you have a ~/.kube directory which has a config file you can either backup the existing config file or append the microk8s config onto it.


## Setup Alias
MicroK8s uses a namespaced kubectl command to prevent conflicts with any existing installs of kubectl. If you don’t have an existing kubernetes install, it is easier to add an alias to your shells aliases file like this:

```text
    alias kubectl='microk8s kubectl'
``` 

## Access Kubernetes
MicroK8s bundles its own version of kubectl for accessing Kubernetes. Use it to run commands to monitor and control your Kubernetes. Kubectl commands are prefixed by microk8s. 

For example to view your node:

```bash
     microk8s kubectl get nodes
```

To view the cluster info:

```bash
    microk8s kubectl cluster-info
```

To view everything currently running in the cluster


```bash
	microk8s kubectl get all --all-namespaces
```

To view running services in the default namespace:

```bash
     microk8s kubectl get services
```
* use `--all-namespaces` for all services in all namespaces
* use `-n kube-system` for the kubernetes system
* use `-n lockss` for lockss specific services

To get a list of commands:

```bash
     microk8s kubectl
```

For details about a specfic command

```bash
	microk8s kubectl <command> --help
```

## Starting and Stopping
MicroK8s will continue running until you decide to stop it. You can stop top MicroK8s and its services by typing the command:

```bash
    microk8s stop
```

You can restart by typing:

```bash
    microk8s start
```

## Additional documentation:
### Microk8s References
* [Complete Documentation](https://microk8s.io/docs)
* [Microk8s Commands](https://microk8s.io/docs/commands) 
* [Troubleshooting Guide](https://microk8s.io/docs/troubleshooting)

### Kubectl References
* [Kubectl commands](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)
* [Kubectl Cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)