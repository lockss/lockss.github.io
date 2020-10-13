---
layout: page
title: System Pre-Requisites
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

## Machine

The LOCKSS system runs on a **64-bit Linux host** (physical or virtual), with **4 cores** (8 or more preferable) and **8 GB of memory** (16 GB or more preferable) and **50GB of diskspace** (100 GB or more preferable).

## Operating System

The LOCKSS system requires a **64-bit Linux** host compatible with [**Systemd**](https://www.freedesktop.org/wiki/Software/systemd/), [**Snap**](https://snapcraft.io/docs/installing-snapd), and the lightweight Kubernetes runtime [**MicroK8s**](https://microk8s.io/).

Some examples we have experience with include:

*   [CentOS](https://www.centos.org/) 7, version 7.6 or later. (**Please note:** Snap is not available on CentOS 7.5 or earlier.)
*   [CentOS](https://www.centos.org/) 8.

Savvy users will probably succeed at installing LOCKSS 2.0-alpha3 on other Linux flavors. However, some examples we do not currently recommend include:

*   [Arch Linux](https://www.archlinux.org/). Although several members of the LOCKSS Team are very fond of Arch Linux and use it daily, the MicroK8s Kubernetes environment does not work very well with it. References: [MicroK8s issue 1034](https://github.com/ubuntu/microk8s/issues/1034).
