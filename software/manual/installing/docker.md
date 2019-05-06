---
layout: page
title: Installing Docker
---

*This information does not apply to the classic LOCKSS daemon (version 1.x).*

## Overview

Docker is a containerization and orchestration engine.

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
1.  [Check the Storage Driver](#check-the-storage-driver)
1.  [Initialize Swarm Mode](#initialize-swarm-mode)
1.  [Enable Docker at Startup](#enable-docker-at-startup)
1.  [Reconfiguring Docker](#reconfiguring-docker) (if required along the way)

## Install the Docker Engine

The LOCKSS system requires **Docker 18.09 or better**.

### Docker on Arch Linux

Simply use Arch's official software repositories to install Docker with Pacman:

    sudo pacman -S docker

### Docker on CentOS

*CentOS 7 or better required*

Use Docker's official software repositories to install Docker with Yum: [https://docs.docker.com/install/linux/docker-ce/centos/](https://docs.docker.com/install/linux/docker-ce/centos/) (the version of Docker available through the standard CentOS software repositories is not suitably recent).

### Docker on Debian

*Debian 9 (Stretch) or better required*

Use Docker's official software repositories to install Docker with Apt: [https://docs.docker.com/install/linux/docker-ce/debian/](https://docs.docker.com/install/linux/docker-ce/debian/) (the `docker` package available through the standard Debian software repositories is for an unrelated system tray application).

### Docker on Fedora

*Fedora 28 or better required*

Use Docker's official software repositories to install Docker with Yum: [https://docs.docker.com/install/linux/docker-ce/fedora/](https://docs.docker.com/install/linux/docker-ce/fedora/) (the version of Docker available through the standard Fedora software repositories is not suitably recent).

### Docker on Oracle Linux

*Oracle Linux 7 or better required*

Use Oracle's official software repositories to install Docker with Yum: [https://docs.oracle.com/cd/E52668_01/E87205/html/section_install_upgrade_yum_docker.html](https://docs.oracle.com/cd/E52668_01/E87205/html/section_install_upgrade_yum_docker.html).

### Docker on Ubuntu

*Ubuntu 16.04 LTS (Xenial) or better required*

Use Docker's official software repositories to install Docker with Apt: [https://docs.docker.com/install/linux/docker-ce/ubuntu/](https://docs.docker.com/install/linux/docker-ce/ubuntu/) (the `docker` package available via the Ubuntu Universe software repository is for an unrelated desktop system tray application).

## Check the System Group

Installing Docker creates a new system group typically named `docker`. The command:

    groups lockss

will display the list of groups the `lockss` user is a member of, which should already include the `lockss` group. If the list of groups does not include the `docker` group, add the `lockss` user to the `docker` group with the following command:

    sudo usermod -G docker -a lockss

or with a similar user management command or tool.

## Start Docker

Start Docker with systemd:

    sudo systemctl start docker

Verify that Docker is running:

    sudo systemctl is-active docker

The output should say `active`.

## Check the Storage Driver

Verify that Docker is using the OverlayFS (`overlay2`) driver:

    sudo -u lockss docker info | grep 'Storage Driver:'

If the output is:

    Storage Driver: overlay2

then Docker is running with the OverlayFS driver and you can move on to the next section. If the output lists another storage driver than `overlay2`, see the [Reconfiguring Docker](#reconfiguring-docker) section below to add the key-value pair `"storage-driver":"overlay2"` to `/etc/docker/daemon.json` and restart the Docker daemon.

## Initialize Swarm Mode

Verify that Docker is using Swarm mode:

    sudo -u lockss docker info | grep 'Swarm:'

If the output is:

    Swarm: active

then Docker is running in Swarm mode and you can move on to the next section. If the output is empty or if the Swarm is not listed as active, initialize Swarm mode with this command:

    sudo -u lockss docker swarm init

If the output looks like this:

    Swarm initialized: current node (bvz81updecsj6wjz393c09vti) is now a manager.

    To add a worker to this swarm, run the following command:

        docker swarm join \
        --token SWMTKN-1-3pu6hszjas19xyp7ghgosyx9k8atbfcr8p2is99znpy26u2lkl-1awxwuwd3z9j1z3puu7rcgdbx \
        xx.xx.xx.xx:2377

    To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.

where `xx.xx.xx.xx` is the IP address of the machine, then the Swarm initialization was successful and you can move on to the next section. If the output contains an error message that looks like this:

    Error response from daemon: could not choose an IP address to advertise since this system has multiple addresses on interface eth0 (xx.xx.xx.xx and yy.yy.yy.yy) - specify one with --advertise-addr

or:

    Error response from daemon: could not choose an IP address to advertise since this system has multiple addresses on different interfaces (xx.xx.xx.xx on eth0 and yy.yy.yy.yy on eth1) - specify one with --advertise-addr

then Docker was not able to automatically select an IP address among the several it discovered. Identify the desired IP address of the machine, for example `xx.xx.xx.xx`, and enter the modified command:

    sudo -u lockss docker swarm init --advertise-addr xx.xx.xx.xx

## Enable Docker at Startup

Unless you are only trying out the LOCKSS system on a machine that will not be running it or Docker routinely, enable Docker to launch at startup with systemd:

    sudo systemctl enable docker

Verify that the operation succeeded with:

    sudo systemctl is-enabled docker

The output should say `enabled`.

## Reconfiguring Docker

This section describes what to do when Docker needs to be reconfigured. **You do not need to do anything unless one of the sections above sends you here.**

Edit or create the `/etc/docker/daemon.json` file and input the required key-value pairs in a JSON object, separated by commas, typically one per line for clarity. Example:

    {
        "storage-driver": "overlay2",
        "iptables": true
    }
