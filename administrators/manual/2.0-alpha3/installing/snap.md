---
layout: page
title: Installing Snap
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

[Snap](https://snapcraft.io/) is a Linux package manager maintained by [Canonical](https://canonical.com/), makers of [Ubuntu](https://ubuntu.com/).

Snap is needed to install [Microk8s](https://microk8s.io/) (a lightweight [Kubernetes](https://kubernetes.io/) environment used by the LOCKSS system), which is also maintained by Canonical (and therefore easiest to install via Snap).

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

### Installing Snap with Yum

Yum is the package manager on **CentOS 7**.

<!-- #packagemanagers -->
Use these Yum commands to install Snap:

```bash
sudo yum update

sudo yum install epel-release

sudo yum install snapd
```

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

*Reference: [Installing snap on openSUSE](https://snapcraft.io/docs/installing-snap-on-opensuse)*

## Enabling Classic Support

MicroK8s uses the so-called classic Snap format, which expects a top-level directory named `/snap` on your system. Nowadays this directory is located at `/var/lib/snapd/snap`. In order for Snap to install MicroK8s correctly, you need to create a symbolic link from `/snap` to `/var/lib/snapd/snap` with this command:

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

## Configuring Snap Updates

*FIXME*

The snap daemon will automatically update any installed snaps and by default it will check every four hours for updates.  For stability, you should consider adjusting the frequency in which snap checks and updates your snaps. To modify update schedules there are four system-wide options:

#### refresh.timer: 
Defines the refresh frequency and schedule

```bash
  sudo snap set system refresh.timer=<refresh-schedule>
```

where <refresh-schedule> is for example:
	
**mon,wed**: monday and wednesday at midnight
	
**fri5,23:00-01:00**: last friday of the month, between 11 pm and 1 am.
	
For a more complete list of formats see the snap documents:

[Snap Documentation: Managing updates](https://snapcraft.io/docs/keeping-snaps-up-to-date)
	
#### refresh.hold: 
Delays the next refresh until the defined time and date
 
```bash
  sudo snap set system refresh.hold="$(date --date=<somedate> +%Y-%m-%dT%H:%M:%S%:z)"
  sudo snap get system refresh.hold
```
where <somedate> is the date for which to hold updates
	
#### refresh.metered: 
Pauses refresh updates when network connection is metered, such as an LTE link with a limited data plan.

```bash
sudo snap set system refresh.metered=hold
```
To restore:

```bash
sudo snap set system refresh.metered=null
```
	
#### refresh.retain: 
Sets how many revisions of a snap are stored on the system

```bash
  sudo snap set system refresh.retain=3
```
This will limit older snaps to 3.
