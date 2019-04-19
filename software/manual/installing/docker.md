---
layout: page
title: Installing Docker
---

*This page is under construction. This information does not apply to the classic LOCKSS daemon (version 1.x).*

Docker is a container runtime and orchestration engine.

## Overview

To install Docker for the purposes of running the LOCKSS system:

*   [Install the Docker Engine](#install-the-docker-engine)
*   [Check the System Group](#check-the-system-group)
*   [Start Docker](#start-docker)
*   [Verify the Docker Configuration](#verify-the-docker-configuration)
*   [Initialize Swarm Mode](#initialize-swarm-mode)
*   [Enable Docker at Startup](#enable-docker-at-startup)
*   [Reconfiguring Docker](#reconfiguring-docker) (if other sections require it)

## Install the Docker Engine

The LOCKSS system requires Docker version 18.09 or better.

### Arch Linux

Use Pacman to install Docker:

    sudo pacman -S docker

### CentOS

*CentOS 7 or better*

The version of Docker available through the standard CentOS software repositories is not suitably recent.

Use Docker's own software repositories to install Docker with Yum: [https://docs.docker.com/install/linux/docker-ce/centos/](https://docs.docker.com/install/linux/docker-ce/centos/)

### Debian

*Debian 9 (Stretch) or better*

The `docker` package available through the standard Debian software repositories is for an unrelated system tray.

Use Docker's own software repositories to install Docker with Apt: [https://docs.docker.com/install/linux/docker-ce/debian/](https://docs.docker.com/install/linux/docker-ce/debian/)

### Fedora

*Fedora 28 or better*

The version of Docker available through the standard Fedora software repositories is not suitably recent.

Use Docker's own software repositories to install Docker with Yum: [https://docs.docker.com/install/linux/docker-ce/fedora/](https://docs.docker.com/install/linux/docker-ce/fedora/)

### Oracle Linux

*This section is under construction.*

### Ubuntu

*Ubuntu 16.04 LTS (Xenial) or better*

The `docker` package available via the Ubuntu Universe software repository is for an unrelated desktop system tray.

*(Recommended)* Use Docker's own software repositories to install Docker with Apt: [https://docs.docker.com/install/linux/docker-ce/ubuntu/](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

*(Alternative)* Or you can use Apt to install Docker from the Ubuntu Universe Updates software repository:

    sudo apt-get install docker.io

## Check the System Group

The user running the LOCKSS system must be a member of the same group (usually `docker`) as the Docker system user (usually `docker`).

*This section is under construction.*

## Start Docker

Start Docker with Systemd:

    sudo systemctl start docker

Verify that Docker is running:

    sudo systemctl is-active docker

The output should say `active`.

*This section is under construction.*

## Verify the Docker Configuration

### Storage Driver

The LOCKSS system works with the Docker OverlayFS (`overlay2`) storage driver. In the output of:

    docker info

look for the line:

    Storage Driver: overlay2

If another value than `overlay2` is listed, add the key-value pair `"storage-driver":"overlay2"` to `/etc/docker/daemon.json` and restart the Docker daemon; see the instructions from the [Reconfiguring Docker](#reconfiguring-docker) section below for details.

### Iptables Management

Some Linux systems (e.g. Oracle Linux) seem to deliver Docker with `iptables` management turned off. If this is the case, add the key-value pair `"iptables":true` to `/etc/docker/daemon.json` and restart the Docker daemon; see the instructions from the [Reconfiguring Docker](#reconfiguring-docker) section below for details.

## Initialize Swarm Mode

The LOCKSS system works with Docker in Swarm mode. In the output of:

    docker info

look for the line:

    Swarm: active

If the line is missing or if the Swarm is not listed as active, initialize Swarm mode with this command:

    docker swarm init

and verify that Swarm mode is active via `docker info`.

## Enable Docker at Startup

Unless you are only trying out the LOCKSS system on a machine that will not be running it or Docker routinely, enable Docker to launch at startup with Systemd:

    sudo systemctl enable docker

Verify that the operation succeeded with:

    sudo systemctl is-enabled docker

The output should say `enabled`.

## Reconfiguring Docker

This section describes what to do when Docker needs to be reconfigured according to one of the sections above.

Edit or create the `/etc/docker/daemon.json` file and input the required key-value pairs in a JSON object, separated by commas, typically one per line for clarity. Example:

    {
        "storage-driver": "overlay2",
        "iptables": true
    }
