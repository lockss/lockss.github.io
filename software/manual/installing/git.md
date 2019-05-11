---
layout: page
title: Installing Git
---

*This information does not apply to the classic LOCKSS daemon (version 1.x).*

[Git](https://git-scm.com/) is a version control system, used to interact with code repositories.

The LOCKSS Installer is available from [GitHub](https://github.com), and you will need a Git client to download it.

Your operating system may already be equipped with a Git client. Type:

    git --version

If the output is a version number, for example:

    git version 2.21.0

then Git is already installed and you do not need to take any further action.

Otherwise, Git can be installed from your operating system's software repositories.

## Git on Arch Linux

Use Pacman to install Git on Arch Linux:

    sudo pacman -S git

## Git on CentOS

<!-- #osversion -->
*CentOS 7 required*

Use Yum to install Git on CentOS:

    sudo yum install git

## Git on Debian

<!-- #osversion -->
*Debian 9 (Stretch) required*

Use Apt to install Git on Debian:

    sudo apt-get install git

## Git on Fedora

<!-- #osversion -->
*Fedora 28 or better required*

Use DNF to install Git on Fedora:

    sudo dnf install git

## Git on Oracle Linux

<!-- #osversion -->
*Oracle Linux 7 required*

Use Yum to install Git on Oracle Linux:

    sudo yum install git

## Git on Ubuntu

<!-- #osversion -->
*Ubuntu 16.04 LTS (Xenial) or better required*

Use Apt to install Git on Ubuntu:

    sudo apt-get install git
