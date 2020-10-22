---
layout: page
title: System Prerequisites
---

*   **Previous: [Introduction](.)**
*   **Up: [Introduction](.)**
*   **Next: [Security Considerations](security)**

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

## Machine

The LOCKSS system runs on a **64-bit Linux host** (physical or virtual), with at least **4 cores** (8 or more preferable), at least **8 GB of memory** (16 GB or more preferable) and at least **50 GB of disk space** (100 GB or more preferable).

## Operating System

The LOCKSS system requires a **64-bit Linux** host compatible with [**Systemd**](https://www.freedesktop.org/wiki/Software/systemd/), [**Snap**](https://snapcraft.io/docs/installing-snapd) and [**MicroK8s**](https://microk8s.io/).

Flavors of Linux we have tested include:

*   [CentOS](https://www.centos.org/) 8.2, 8.1, 8.0, 7.8, 7.6. **Recommended.** *Please note: Snap is not available on CentOS 7.5 or earlier; version 7.6 or later is required.*
*   [Debian](https://www.debian.org/) 10.6, 10.5, 10.4, 10.3, 10.2, 10.1, 10.0, 9.13, 9.12, 9.9, 9.6, 9.5, 9.4, 9.3, 9.2, 9.1, 9.0.
*   [Linux Mint](https://linuxmint.com/) 20.0, 19.3, 19.2, 19.1, 19.0, 18.3, 18.2. *Please note: Snap is not available on Linux Mint 18.1 or earlier; version 18.2 or later is required.*
*   [OpenSUSE](https://www.opensuse.org/) Leap 15.2, 15.1, 15.0.
*   [RHEL](https://www.redhat.com/) 8.2, 7.8.
*   [Ubuntu](https://ubuntu.com/) 20.04 LTS, 19.10, 19.04, 18.10, 18.04 LTS, 17.10, 17.04, 16.10, 16.04 LTS.

LOCKSS 2.0-alpha3 can probably be installed successfully on slightly different versions of the operating systems above, for instance CentOS 7.7 or Debian 9.11. Additionally, savvy users will likely succeed at installing LOCKSS 2.0-alpha3 on other Linux flavors.

*Currently, we do not recommend [Arch Linux](https://www.archlinux.org/) or [Fedora Linux](https://getfedora.org/) 32, because MicroK8s 1.18.9, the currently available version in the required 1.18 series, does not seem to work on these platforms as documented. This highlights an inconvenience of the default Snap-only distribution of MicroK8s that we hope to address in 2.0-alpha4.*
