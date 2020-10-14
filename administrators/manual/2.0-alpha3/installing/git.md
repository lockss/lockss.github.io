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

On many flavors of Linux, you can install Git with the built-in package manager:

*   CentOS 7: Yum
*   CentOS 8: Dnf
*   Debian: Apt
*   Ubuntu: Apt
<!-- #packagemanagers -->

### Installing Git with Apt

<!-- #packagemanagers -->
Apt is the package manager on **Debian** and **Ubuntu**.

Use these Apt commands to install Git:

```bash
sudo apt update

sudo apt install git
```

### Installing Git with Dnf

<!-- #packagemanagers -->
Dnf is the package manager on **CentOS 8**.

Use this Dnf command to install Git:

```bash
sudo dnf install git
```

### Installing Git with Yum

Yum is the package manager on **CentOS 7**.

<!-- #packagemanagers -->
Use these Yum commands to install Git:

```bash
sudo yum update

sudo yum install git
```