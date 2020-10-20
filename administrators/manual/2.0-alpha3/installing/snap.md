---
layout: page
title: Installing Snap
---

*   **Previous: [Downloading the LOCKSS Installer](lockss-installer)**
*   **Up: [Installing the LOCKSS System](.)**
*   **Next: [Installing MicroK8s](microk8s)**

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

[Snap](https://snapcraft.io/) is a Linux application package manager maintained by [Canonical](https://canonical.com/), makers of [Ubuntu](https://ubuntu.com/).

Snap is needed to install [MicroK8s](https://microk8s.io/) (a lightweight [Kubernetes](https://kubernetes.io/) environment used by the LOCKSS system), which is also maintained by Canonical (and therefore only installed via Snap).

More complete instructions can be found at "[Installing `snapd`](https://snapcraft.io/docs/installing-snapd)" on [Snapcraft](https://snapcraft.io/), Snap's home Web site, but we also provide some high level installation instructions below.

## Checking for Snap

Some Linux flavors come with Snap pre-installed, for instance **Ubuntu**. To determine if your operating system is already be equipped with Snap, type:

```bash
snap version
```

If you see something similar to the following:

```text
snap    2.46.1-1
snapd   2.46.1-1
series  16
kernel  5.8.13
```

then Snap is already installed and you do not need to take further action.

If you see an error message similar to the following:

```text
bash: snap: command not found
```

then you need to install Snap.

## Installing Snap

On many flavors of Linux, you can install Snap with the built-in package manager:

*   CentOS 7: Yum
*   CentOS 8: Dnf
*   Debian: Apt
*   Linux Mint: Apt
*   OpenSUSE: Zypper
*   RHEL 7: Yum
*   RHEL 8: Dnf
*   Ubuntu: Apt
<!-- #packagemanagers -->

### Installing Snap with Apt

<!-- #packagemanagers -->
Apt is the package manager on **Debian**, **Linux Mint** and **Ubuntu**.

#### Pre-Installing Snap on Linux Mint 20

Before you can install Snap on **Linux Mint 20**, you first need to type this command:

```bash
sudo rm /etc/apt/preferences.d/nosnap.pref
```

This step is not needed for Linux Mint 19.

#### Installing Snap on All Apt Systems

After taking pre-installation steps necessary for your particular Linux flavor, use these Apt commands to install Snap:

Use these Apt commands to install Snap:

```bash
sudo apt update

sudo apt install snapd
```

You can then proceed to the [next step](#enabling-classic-confinement).

### Installing Snap with Dnf

<!-- #packagemanagers -->
Dnf is the package manager on **CentOS 8** and **RHEL 8**.

#### Pre-Installing Snap on CentOS 8

Before you can install Snap on **CentOS 8**, you first need to type these Dnf commands:

```bash
sudo dnf update

sudo dnf install epel-release

sudo dnf upgrade
```

#### Pre-Installing Snap on RHEL 8

Before you can install Snap on **RHEL 8**, you first need to type these Dnf commands:

```bash
sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

sudo dnf upgrade
```

#### Installing Snap on All Dnf Systems

After taking pre-installation steps necessary for your particular Linux flavor, use this Dnf command to install Snap:

```bash
sudo dnf install snapd
```

You can then proceed to the [next step](#enabling-classic-confinement).

### Installing Snap with Yum

Yum is the package manager on **CentOS 7** and **RHEL 7**.

#### Pre-Installing Snap on CentOS 7

Before you can install Snap on **CentOS 7**, you first need to type these Yum commands:

```bash
sudo yum update

sudo yum install epel-release
```

#### Pre-Installing Snap on RHEL 7

Before you can install Snap on **RHEL 7**, you first need to type these commands:

```bash
sudo rpm -ivh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

sudo subscription-manager repos --enable "rhel-*-optional-rpms" --enable "rhel-*-extras-rpms"
```

#### Installing Snap on All Yum Systems

After taking pre-installation steps necessary for your particular Linux flavor, use this Yum command to install Snap:

```bash
sudo yum install snapd
```

You can then proceed to the [next step](#enabling-classic-confinement).

*References: [Installing snap on CentOS](https://snapcraft.io/docs/installing-snap-on-centos), [Installing snap on Red Hat Enterprise Linux (RHEL)
](https://snapcraft.io/docs/installing-snap-on-red-hat)*

### Installing Snap with Zypper

Zypper is the package manager on **OpenSUSE**.

<!-- #packagemanagers -->
First, use one of these Zypper commands (note the slight variation based on the exact version of your system):

```bash
# For OpenSUSE Leap 15.0:
sudo zypper addrepo --refresh https://download.opensuse.org/repositories/system:/snappy/openSUSE_Leap_15.0 snappy

# For OpenSUSE Leap 15.1:
sudo zypper addrepo --refresh https://download.opensuse.org/repositories/system:/snappy/openSUSE_Leap_15.1 snappy

# For OpenSUSE Leap 15.2:
sudo zypper addrepo --refresh https://download.opensuse.org/repositories/system:/snappy/openSUSE_Leap_15.2 snappy
```

Then use these Zypper commands to install Snap:

```bash
sudo zypper --gpg-auto-import-keys refresh

sudo zypper dup --from snappy

sudo yum install epel-release

sudo yum install snapd
```

You can then proceed to the [next step](#enabling-classic-confinement).

*References: [Installing snap on openSUSE](https://snapcraft.io/docs/installing-snap-on-opensuse)*

## Enabling Classic Confinement

MicroK8s uses Snap's so-called classic confinement model, which expects a top-level directory named `/snap` on your system. Nowadays this directory is located at `/var/lib/snapd/snap`. In order for Snap to install MicroK8s correctly, you need to create a symbolic link from `/snap` to `/var/lib/snapd/snap` with this command:

```bash
sudo ln -s /var/lib/snapd/snap /snap
```

(On some systems like Debian, `/snap` may already exist.)

## Enabling Snap

You can then enable Snap on your system with the following command:

```bash
sudo systemctl enable --now snapd.socket
```

## Logging Out and Back In

Log out and back in again (or restart your system) to ensure Snap's paths are updated correctly.

## Verifying Snap

Snap offers a way to verify that things work correctly, by installing and running the `hello-world` Snap package. Type this Snap command:

```bash
sudo snap install hello-world
```

and then verify that this command:

```bash
hello-world
```

outputs the greeting `Hello World!`.

## Configuring Snap Updates

The snap daemon will automatically update any installed Snap packages and by default it will check every four hours for updates.

For stability, you should adjust the frequency at which Snap checks and updates your Snap packages.

To adjust your update schedule to a year (the maximum allowed), use a refresh hold:

```bash
sudo snap set system refresh.hold="$(date --date='364 days' +%Y-%m-%dT%H:%M:%S%:z)"
```
