---
layout: page
title: Installing Docker
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

[Docker](https://www.docker.com/) is a container runtime and orchestration engine. This page will walk you through the initial installation of the Docker engine and the [Local-Persist](https://github.com/MatchbookLab/local-persist) Docker volume plugin.

## Overview

To install Docker for the purposes of running the LOCKSS system:

1.  [Install Docker](#install-docker)
    *   [Docker on Arch Linux](#docker-on-arch-linux)
    *   [Docker on CentOS](#docker-on-centos)
    *   [Docker on Debian](#docker-on-debian)
    *   [Docker on Fedora](#docker-on-fedora)
    *   [Docker on Oracle Linux](#docker-on-oracle-linux)
    *   [Docker on Ubuntu](#docker-on-ubuntu)
1.  [Check the System Group](#check-the-system-group)
1.  [Start Docker](#start-docker)
1.  [Enable Docker at Startup](#enable-docker-at-startup)
1.  [Reconfiguring Docker](#reconfiguring-docker) (if required along the way)

## Install the Docker Engine

The LOCKSS system requires **Docker 18.09 or better**.

### Docker on Arch Linux

Simply use Arch's official software repositories to install Docker with Pacman:

```bash
    sudo pacman -S docker
```

### Docker on CentOS

<!-- #osversion -->
*CentOS 7 required*

Use Docker's official software repositories to install Docker with Yum: <https://docs.docker.com/install/linux/docker-ce/centos/> (the version of Docker available through the standard CentOS software repositories is not suitably recent).

### Docker on Debian

<!-- #osversion -->
*Debian 9 (Stretch) required*

Use Docker's official software repositories to install Docker with Apt: <https://docs.docker.com/install/linux/docker-ce/debian/> (the `docker` package available through the standard Debian software repositories is for an unrelated system tray application).

### Docker on Fedora

<!-- #osversion -->
*Fedora 28 or better required*

Use Docker's official software repositories to install Docker with DNF: <https://docs.docker.com/install/linux/docker-ce/fedora/> (the version of Docker available through the standard Fedora software repositories is not suitably recent).

### Docker on Oracle Linux

<!-- #osversion -->
*Oracle Linux 7 required*

Use Oracle's official software repositories to install Docker with Yum: <https://docs.oracle.com/cd/E52668_01/E87205/html/section_install_upgrade_yum_docker.html>.

### Docker on Ubuntu

<!-- #osversion -->
*Ubuntu 16.04 LTS (Xenial) or better required*

Use Docker's official software repositories to install Docker with Apt: <https://docs.docker.com/install/linux/docker-ce/ubuntu/> (the `docker` package available via the Ubuntu Universe software repository is for an unrelated desktop system tray application).

## Check the System Group

Installing Docker creates a new system group typically named `docker`. The command:

```bash
    groups lockss
```

will display the list of groups the `lockss` user is a member of, which should already include the `lockss` group. If the list of groups does not include the `docker` group, add the `lockss` user to the `docker` group with the following command:

```bash
    sudo usermod -G docker -a lockss
```

or with a similar user management command or tool.

## Start Docker

Start Docker with systemd:

```bash
    sudo systemctl start docker
```

Verify that Docker is running:

```bash
    sudo systemctl is-active docker
```

The output should say `active`.

## Enable Docker at Startup

Unless you are only trying out the LOCKSS system on a machine that will not be running it or Docker routinely, enable Docker to launch at startup with systemd:

```bash
    sudo systemctl enable docker
```

Verify that the operation succeeded with:

```bash
    sudo systemctl is-enabled docker
```

The output should say `enabled`.

## Check the Storage Driver

Verify that Docker is using the OverlayFS (`overlay2`) storage driver:

```bash
    sudo -u lockss docker info | grep 'Storage Driver:'
```

If the output is:

```text
    Storage Driver: overlay2
```

then Docker is running with the OverlayFS storage driver and you can move on to the next section.

If the output lists another storage driver than `overlay2` (for example `devicemapper`), see the [Reconfiguring Docker](#reconfiguring-docker) section below, add the key-value pair `"storage-driver":"overlay2"` to `/etc/docker/daemon.json`, and restart the Docker daemon.

## Reconfiguring Docker

This section describes what to do when Docker needs to be reconfigured. **You do not need to do anything unless one of the sections above sends you here.**

Edit or create the `/etc/docker/daemon.json` configuration file and input the required key-value pairs in a JSON object, separated by commas, typically one per line for clarity. Example:

```text
    {
        "storage-driver": "overlay2",
        "iptables": true
    }
```

After editing and saving the configuration file, restart the Docker daemon with systemd:

```bash
    sudo systemctl restart docker
```
