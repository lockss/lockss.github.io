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
1. 	[Enable DNS](#enable-dns)
1.  [Setup Users Kubectl Config](#setup-users-kubectl-config)

The LOCKSS system requires **Microk8s 1.18 or better**.

## Install Microk8s

```bash
    sudo snap install microk8s --classic --channel=1.18/stable
```

## Join the Group
MicroK8s creates a group to enable usage of commands which require admin privilege. To add your current user to the group and gain access to the .kube caching directory, run the following two commands:

```bash
    sudo usermod -a -G microk8s lockss
```

### You need to log off and log back in or re-enter the session for the group update to take place:

```bash
    su - lockss
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
If your system is using a firewall you will need to open the necessary ports for your systems firewall.  See the firewall documentation for help in configuring your system for access:

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


## Additional documentation:
* [Configuring Firewalls](firewall)
* [Using Microk8s](using-microk8s)

### Microk8s References
* [Complete MicroK8s Documentation](https://microk8s.io/docs)
* [Microk8s Commands](https://microk8s.io/docs/commands) 
* [Troubleshooting Guide](https://microk8s.io/docs/troubleshooting)

### Kubectl References
* [Kubectl commands](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)
* [Kubectl Cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)