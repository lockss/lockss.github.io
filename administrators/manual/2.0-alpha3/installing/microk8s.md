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
1.  [Access Kubernetes](#check-the-status)
1.  [Setup Alias](#setup alias)
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
You  to re-enter the session for the group update to take place:
```bash
    su - $USER
```

## Check the Status
During installation you can use the --wait-ready flag  on the status command to wait for the Kubernetes services to initialise:
```bash
     microk8s status --wait-ready
```

## Access Kubernetes
MicroK8s bundles its own version of kubectl for accessing Kubernetes. Use it to run commands to monitor and control your Kubernetes. Kubectl commands are prefixed by microk8s. For example to view your node:
```bash
     microk8s kubectl get nodes
```
To view running services:
```bash
     microk8s kubectl get services
```
## Turn on the feature-gate ExternalPolicyForExternalIP 
```bash
  echo '--feature-gates="ExternalPolicyForExternalIP=true"' | sudo tee -a /var/snap/microk8s/current/args/kube-proxy   
  sudo systemctl restart snap.microk8s.daemon-proxy.service
```
## Setup users kubectl config
If you don’t have an existing install or ~/.kube directory
```
    mkdir ~/.kube
    microk8s config > ~/.kube/config
```
## Setup Alias
MicroK8s uses a namespaced kubectl command to prevent conflicts with any existing installs of kubectl. If you don’t have an existing install, it is easier to add an alias (append to ~/.bash_aliases) like this:
```
    alias kubectl='microk8s kubectl'
``` 
## Starting and Stopping
MicroK8s will continue running until you decide to stop it. You can stop top MicroK8s and its services by typing the command:
```bash
    microk8s stop
```
You can start again any time by typing:
```bash
    microk8s start
```

