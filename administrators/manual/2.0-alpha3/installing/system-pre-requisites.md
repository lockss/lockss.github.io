---
layout: page
title: System Pre-Requisites
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

## Machine

The LOCKSS system runs on a **64-bit Linux** host (physical or virtual), with **4 cores** (8 or more preferable) and **8 GB of memory** (16 GB or more preferable).

## Operating System

The LOCKSS system requires a **64-bit Linux** host running [**systemd**](https://www.freedesktop.org/wiki/Software/systemd/), an operating system which supports [**snapd**](https://snapcraft.io/docs/installing-snapd), and the lightweight kubernetes runtime [**microk8s**](https://microk8s.io/).

Many Linux distributions have systemd and can run Docker 18.09 or better. To name a few commonly used with the LOCKSS system:

*   [Arch Linux](https://www.archlinux.org/)
<!-- #osversion -->
*   [CentOS](https://www.centos.org/) 7
<!-- #osversion -->
*   [Debian](https://www.debian.org/) 9 (Stretch)
<!-- #osversion -->
*   [Fedora](https://getfedora.org/) 28 or better
<!-- #osversion -->
*   [Oracle Linux](https://www.oracle.com/linux/) 7
<!-- #osversion -->
*   [Ubuntu](https://www.ubuntu.com/) 16.04 LTS (Xenial) or better

## User

The LOCKSS system runs under a system user named `lockss` under a group named `lockss`, which you will need to create.
## Snap
To install the microk8s kubernetes cluster you will need to install snapd. Most Ubuntu flavours of linux come with snap preinstalled.  However, for other systems you will need to follow the instructions for installing snap for that system found at [Snapd Install](https://snapcraft.io/docs/installing-snapd)
