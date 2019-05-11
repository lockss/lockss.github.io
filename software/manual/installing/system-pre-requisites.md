---
layout: page
title: System Pre-Requisites
---

*This information does not apply to the classic LOCKSS daemon (version 1.x).*

## Machine

The LOCKSS system runs on a **64-bit Linux** host (physical or virtual), with **4 cores** (8 or more preferable) and **8 GB of memory** (16 GB or more preferable).

## Operating System

The LOCKSS system requires a **64-bit Linux** host running [**systemd**](https://www.freedesktop.org/wiki/Software/systemd/) and **[Docker](https://www.docker.com/) 18.09 or better**.

Many Linux distributions have systemd and can run Docker 18.09 or better. To name a few that are commonly used with the LOCKSS system:

<!-- #osversion -->
*   [Arch Linux](https://www.archlinux.org/)
*   [CentOS](https://www.centos.org/) 7
*   [Debian](https://www.debian.org/) 9 (Stretch)
*   [Fedora](https://getfedora.org/) 28 or better
*   [Oracle Linux](https://www.oracle.com/linux/) 7
*   [Ubuntu](https://www.ubuntu.com/) 16.04 LTS (Xenial) or better

## User

The LOCKSS system runs under a system user named `lockss` under a group named `lockss`, which you will need to create.

<!-- FIXME -->
*This section is under construction.*
