---
layout: page
title: System Pre-Requisites
---

*This information applies to version 2.0-alpha2 of the LOCKSS system.*

## Machine

The LOCKSS system runs on a **64-bit Linux** host (physical or virtual), with **4 cores** (8 or more preferable) and **8 GB of memory** (16 GB or more preferable).

## Operating System

The LOCKSS system requires a **64-bit Linux** host running [**systemd**](https://www.freedesktop.org/wiki/Software/systemd/) and **[Docker](https://www.docker.com/) 18.09 or better**.

Many Linux distributions have systemd and can run Docker 18.09 or better. To name a few that are commonly used with the LOCKSS system:

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

To check installed pre-requisites, use the script [`scripts/check_sys`](check-sys), which will attempt to find and install missing elements.
