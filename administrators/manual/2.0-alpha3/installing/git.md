---
layout: page
title: Installing Git
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

## Overview

[Git](https://git-scm.com/) is a version control system, used to interact with code repositories.

The LOCKSS Installer is available from [GitHub](https://github.com), and you will need a Git client to download it.

## Checking for Git

Your operating system may already be equipped with a Git client. Type:

```bash
git --version
```

If the output is a version number, for example:

```text
git version 2.28.0
```

then Git is already installed and you do not need to take further action.

If you see an error message similar to the following:

```text
bash: git: command not found
```

then you need to install Git.

## Installing Git

On most flavors of Linux, you can install Git from official package repositories.

### How to Do It on CentOS 7

<!-- #osversion -->
Use Yum to install Git on CentOS 7:

```bash
sudo yum install git
```

### How to Do It on CentOS 8

<!-- #osversion -->
Use Dnf to install Git on CentOS 8:

```bash
sudo dnf install git
```

### Git on Debian

<!-- #osversion -->
*Debian 9 (Stretch) required*

Use Apt to install Git on Debian:

```bash
    sudo apt-get install git
```

### Git on Fedora

<!-- #osversion -->
*Fedora 28 or better required*

Use Dnf to install Git on Fedora:

```bash
    sudo dnf install git
```

### Git on Ubuntu

<!-- #osversion -->
*Ubuntu 16.04 LTS (Xenial) or better required*

Use Apt to install Git on Ubuntu:

```bash
    sudo apt-get install git
```
