---
layout: page
title: System Prerequisites
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

## Machine

The LOCKSS system runs on a **64-bit Linux host** (physical or virtual), with at least **4 cores** (8 or more preferable), at least **8 GB of memory** (16 GB or more preferable) and at least **50 GB of diskspace** (100 GB or more preferable).

## Operating System

The LOCKSS system requires a **64-bit Linux** host compatible with [**Systemd**](https://www.freedesktop.org/wiki/Software/systemd/), [**Snap**](https://snapcraft.io/docs/installing-snapd), and the lightweight Kubernetes runtime [**MicroK8s**](https://microk8s.io/).

Some examples we have experience with include:

*   [CentOS](https://www.centos.org/) 7, version 7.6 or later. **Recommended.** (Please note: Snap is not available on CentOS 7.5 or earlier. Version 7.6 or later is required.)
*   [CentOS](https://www.centos.org/) 8.
*   [Debian](https://www.debian.org/) 10 (Buster).
*   [Linux Mint](https://linuxmint.com/) 19
*   [OpenSUSE](https://www.opensuse.org/) Leap 15.
*   [RHEL](https://www.redhat.com/) 8.
*   [Ubuntu](https://ubuntu.com/) 20.04 LTS (Focal Fossa).

LOCKSS 2.0-alpha3 can probably be installed successfully on slightly different versions of the operating systems above with ease. Additionally, savvy users will likely succeed at installing LOCKSS 2.0-alpha3 on other Linux flavors.

*Currently, we do not recommend [Arch Linux](https://www.archlinux.org/) or [Fedora Linux](https://getfedora.org/) 32, because MicroK8s 1.18.9, the currently available version in the required 1.18 series, does not seem to work on these platforms as documented. This highlights an inconvenience of the default Snap-only distribution of MicroK8s that we hope to address in 2.0-alpha4.*
