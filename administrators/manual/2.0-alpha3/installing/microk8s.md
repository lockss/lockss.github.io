---
layout: page
title: Installing Kubernetes with Microk8s
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

## Overview

[Microk8s](https://microk8s.io/) is a lightweight Kubernetes environment. ([Kubernetes](https://kubernetes.io/) is a system for managing and deploying containerized applications.) This page will walk you through the initial installation of Microk8s.

The LOCKSS system requires **MicroK8s 1.18**.

## Installing Microk8s

```bash
sudo snap install microk8s --classic --channel=1.18/stable
```

## Joining the `microk8s` Group

MicroK8s creates a group to enable usage of commands which require admin privilege. To add your current user to the group and gain access to the .kube caching directory, run the following two commands:

```bash
sudo usermod -a -G microk8s lockss
```

## Logging Out and Back In

Log out and back in again (or restart your system) for the group update to take place.

After you log back in as `lockss`, try:

```bash
microk8s --help
```

to check that MicroK8s is on your `PATH`. You should see a help message similar to the following:

```text
Available subcommands are:
	add-node
	cilium
	config
...
```

If you see an error message instead (such as `bash: microk8s: command not found`), you need to ensure `/var/lib/snapd/snap/bin` is on the `PATH`.

## Generating the Kubernetes Configuration

Generate the Kubernetes configuration file from MicroK8s using these commands:

```bash
mkdir -p ~/.kube
microk8s config > ~/.kube/config
```

## Checking the Status of MicroK8s

Type the following command which will start MicroK8s and wait until it is fully ready. It will then display the status of various MicroK8s subsystems:

```bash
microk8s status --wait-ready
```

Output will look something like the following:

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

## Adjust the Firewall

If your system is using a firewall you will need to open the necessary ports for your systems firewall.  See the firewall documentation for help in configuring your system for access.

The containers will need to speak to each other and to both send and receive messages.
If you are using a firewall or iptables you will need to insure it.  See the firewall document to make necessary adjustments:  [Configuring Firewalls](firewall)

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