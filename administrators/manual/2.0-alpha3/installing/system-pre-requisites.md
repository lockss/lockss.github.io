---
layout: page
title: System Pre-Requisites
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

## Machine

The LOCKSS system runs on a **64-bit Linux** host (physical or virtual), with **4 cores** (8 or more preferable) and **8 GB of memory** (16 GB or more preferable) and **50GB of diskspace**.

## Operating System

The LOCKSS system requires a **64-bit Linux** host running [**systemd**](https://www.freedesktop.org/wiki/Software/systemd/), an operating system which supports [**Snap**](https://snapcraft.io/docs/installing-snapd), and the lightweight Kubernetes runtime [**MicroK8s**](https://microk8s.io/). Some examples we have experience with include:

*   [CentOS](https://www.centos.org/) 7, version 7.6 or later. (Snap is not available on CentOS 7.5 or earlier.)

## User

The LOCKSS system runs under a system user named `lockss`, who is under a group named `lockss`, and who is capable of using `sudo`.

<!-- #osversion -->
### How to Do It on CentOS or RHEL

```bash
sudo adduser --system --user-group --create-home --shell=/bin/false --groups=wheel lockss
```

This will create the system user `lockss`, the group `lockss`, and the home directory `/home/lockss`; ensure nobody can log in as `lockss` except `root` and `sudo` users; and give the `lockss` user `sudo` access which by default on this OS is equated with membership in the `wheel` group.

### How to Do It on Debian or Ubuntu

Add the user lockss, as root or using sudo. You will be prompted for a password.

```bash
sudo adduser lockss
```

Add user lockss to sudo group.

```bash
sudo usermod -aG sudo lockss
```
