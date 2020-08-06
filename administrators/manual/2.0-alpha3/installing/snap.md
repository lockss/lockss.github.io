---
layout: page
title: Installing Snap Package Manager
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

[Snap](https://snapcraft.io/) are app packages for desktop, cloud and IoT that are easy to install, secure, cross-platform and dependency-free.

To install the microk8s kubernetes cluster you will need to install snap. Most Ubuntu flavours of linux come with snap preinstalled.  However, for other systems you will need to follow the instructions for installing snap for your system below. More complete instructions can be found at [Snapd Install](https://snapcraft.io/docs/installing-snapd).

To determine if your operating system is already be equipped with a Snap client. Type:

```bash
    snap
```

You should see the snap help screen:

```text
The snap command lets you install, configure, refresh and remove snaps.
Snaps are packages that work across many different Linux distributions,
enabling secure delivery and operation of the latest apps and utilities.

Usage: snap <command> [<options>...]

Commands can be classified as follows:

         Basics: find, info, install, list, remove
        ...more: refresh, revert, switch, disable, enable
        History: changes, tasks, abort, watch
        Daemons: services, start, stop, restart, logs
       Commands: alias, aliases, unalias, prefer
  Configuration: get, set, unset, wait
        Account: login, logout, whoami
    Permissions: connections, interface, connect, disconnect
      Snapshots: saved, save, check-snapshot, restore, forget
          Other: version, warnings, okay, ack, known, model, create-cohort
    Development: run, pack, try, download, prepare-image

For more information about a command, run 'snap help <command>'.
For a short summary of all commands, run 'snap help --all'.
```

If Snap is already installed, you do not need to take any further action.

Otherwise, Snap can be installed from your operating system's software repositories.

## Snap on Arch Linux

The manual build process is the Arch-supported install method for AUR packages, and you’ll need the prerequisites installed before you can install any AUR package. You can then install snap with the following:

```bash
	git clone https://aur.archlinux.org/snapd.git
	cd snapd
	makepkg -si
```

Once installed, enable the systemd unit that manages the main snap communication socket:

```bash
    sudo systemctl enable --now snapd.socket
```

Enable classic snap support, by creating a symbolic link between /var/lib/snapd/snap and /snap:

```bash
	sudo ln -s /var/lib/snapd/snap /snap
```

Either log out and back in again, or restart your system, to ensure snap’s paths are updated correctly


## Snap on CentOS

<!-- #osversion -->
*CentOS 7 or better required*

Determine your centos release

```bash
    cat /etc/centos-release
```

Add the EPEL packages to your CentOS 7 distribution

```bash
	sudo yum install epel-release
```

Add the EPEL packages to your CentOS 8 distribution

```bash
	sudo dnf install epel-release
	sudo dnf upgrade
```

Use Yum to install Snap on CentOS:

```bash
    sudo yum install snapd
```

Once installed, enable the systemd unit that manages the main snap communication socket:

```bash
    sudo systemctl enable --now snapd.socket
```

Enable classic snap support, by creating a symbolic link between /var/lib/snapd/snap and /snap:

```bash
	sudo ln -s /var/lib/snapd/snap /snap
```

Either log out and back in again, or restart your system, to ensure snap’s paths are updated correctly

## Snap on Debian

<!-- #osversion -->
*Debian 9 (Stretch) required*

Use Apt to install Snap on Debian:

```bash
    sudo apt update
    sudo apt install snapd
```
Either log out and back in again, or restart your system, to ensure snap’s paths are updated correctly. After this, install the core snap in order to get the latest snapd.

```bash
	snap install core
	snap refresh core
```

## Snap on Fedora

<!-- #osversion -->
*Fedora 28 or better required*

Use DNF to install Snap on Fedora:

```bash
    sudo dnf install snapd
```

Enable classic snap support, by creating a symbolic link between /var/lib/snapd/snap and /snap:

```bash
	sudo ln -s /var/lib/snapd/snap /snap
```

Either log out and back in again, or restart your system, to ensure snap’s paths are updated correctly

## Snap on RHEL/Oracle Linux

<!-- #osversion -->
*RHEL/Oracle Linux 7 required*


Add the EPEL packages to your RHEL 7 distribution

```bash
	sudo rpm -ivh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
	sudo yum update
```

Add the EPEL packages to your RHEL 8 distribution

```bash
	sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
	sudo dnf upgrade
```

Use Yum to install Snap on CentOS:

```bash
    sudo yum install snapd
```

Once installed, enable the systemd unit that manages the main snap communication socket:

```bash
    sudo systemctl enable --now snapd.socket
```

Enable classic snap support, by creating a symbolic link between /var/lib/snapd/snap and /snap:

```bash
	sudo ln -s /var/lib/snapd/snap /snap
```

Either log out and back in again, or restart your system, to ensure snap’s paths are updated correctly
