---
layout: page
title: System Pre-Requisites
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

## Machine

The LOCKSS system runs on a **64-bit Linux** host (physical or virtual), with **4 cores** (8 or more preferable) and **8 GB of memory** (16 GB or more preferable) and **20GB of diskspace**.

## Operating System

The LOCKSS system requires a **64-bit Linux** host running [**systemd**](https://www.freedesktop.org/wiki/Software/systemd/), an operating system which supports [**snapd**](https://snapcraft.io/docs/installing-snapd), and the lightweight kubernetes runtime [**microk8s**](https://microk8s.io/).

Many Linux distributions have systemd and can run Snapd. To name a few commonly used with the LOCKSS system:

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

<!-- #osversion -->
*Ubuntu/Debian*

Add the user lockss, as root or using sudo. You will be prompted for a password.

```bash
sudo adduser lockss
```

Add user lockss to sudo group.

```bash
sudo usermod -aG sudo lockss
```

<!-- #osversion -->
*RHEL/Oracle/Centos*

Add the user lockss, as root or using sudo.

```bash
sudo adduser lockss
sudo passwd lockss
```

Add superuser privileges by assigning lockss to wheel:

```bash
visudo
```

Scroll through the configuration file until you see the following entry:

```text
## Allows people in group wheel to run all commands

# %wheel        ALL=(ALL)       ALL
```
If the second line begins with the # sign, it has been disabled and marked as a comment. Just delete the # sign at the beginning of the second line so it looks like the following:

```text
%wheel        ALL=(ALL)       ALL
```

Now add lockss to the group wheel

```bash
sudo usermod –aG wheel lockss
```
