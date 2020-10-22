---
layout: page
title: Installing MicroK8s
---

*   **Previous: [Installing Snap](snap)**
*   **Up: [Installing the LOCKSS System](.)**
*   **Next: [Configuring DNS](dns)**

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

## Overview

[MicroK8s](https://microk8s.io/) is a lightweight Kubernetes environment. ([Kubernetes](https://kubernetes.io/) is a system for managing and deploying containerized applications like the LOCKSS system.) This page will walk you through the initial installation of MicroK8s.

The LOCKSS system requires **MicroK8s 1.18**.

All the commands on this page should be run as the `lockss` user.

## Installing MicroK8s

To install the MicroK8s Snap package, run this Snap command:

```bash
sudo snap install microk8s --classic --channel=1.18/stable
```

### Troubleshooting

In some flavors of Linux (including Debian 9), sometimes the above command fails. Try running the following command first:

```
sudo snap install core
```

then retry installing the MicroK8s Snap package.

## Joining the `microk8s` Group

MicroK8s creates a group to enable usage of commands which require admin privilege. To add your current user to the group and gain access to the .kube caching directory, run the following two commands:

```bash
sudo usermod -G microk8s -a lockss
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

If you see an error message instead (such as `bash: microk8s: command not found`), you need to ensure `/snap/bin` is on the `PATH`.

## Generating the Kubernetes Configuration

Generate the Kubernetes configuration file from MicroK8s using these commands:

```bash
mkdir -p ~/.kube

sudo chown -f -R lockss ~/.kube

microk8s config --use-loopback > ~/.kube/config
```

## Starting MicroK8s

Type the following command which will start MicroK8s and wait until it is fully ready.

```bash
microk8s status --wait-ready
```

It will then display the status of various MicroK8s subsystems:

```text
microk8s is running
addons:
dashboard: disabled
dns: disabled
...
```

----

#### Additional documentation:

*   [Using MicroK8s](../appendix/using-microk8s)

##### MicroK8s References

*   [Complete MicroK8s Documentation](https://microk8s.io/docs)
*   [MicroK8s Commands](https://microk8s.io/docs/commands) 
*   [Troubleshooting Guide](https://microk8s.io/docs/troubleshooting)

#### Kubectl References

*   [Kubectl commands](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)
*   [Kubectl Cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
