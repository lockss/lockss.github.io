---
layout: page
title: Upgrading From LOCKSS 2.0-alpha2
---

*   **Previous: [Security Considerations](../introduction/security)**
*   **Up: [Introduction](.)**
*   **Next: [Installing the LOCKSS System](../installing)**

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

## Recommended Approach

If you have been using [LOCKSS 2.0-alpha2](../../../releases/2.0-alpha2) (or [LOCKSS 2.0-alpha1](../../../releases/2.0-alpha1), or the [LOCKSS 2.0-alpha technology preview](../../../releases/2.0-alpha-preview)), we thank you for helping us bring LOCKSS 2.0 closer to fruition through your testing and feedback.

Although there is an upgrade path from LOCKSS 2.0-alpha2, [LOCKSS 2.0-alpha3](../../../releases/2.0-alpha3) is organized significantly differently than prior alpha releases, and we recommend [installing LOCKSS 2.0-alpha3 from scratch](../installing) when possible.

## Upgrade Path

If you intend to upgrade a LOCKSS 2.0-apha2 system, please read this section.

### Updating the LOCKSS Installer

On the command line, in the `lockss-installer` directory, type:

```bash
git checkout master
git pull
```

to update to the latest version of `lockss-installer` from GitHub.

### Running the Upgrade Command

On the command line in the updated `lockss-installer` directory, type:

```bash
sudo scripts/upgrade-alpha2-to-alpha3
```

The script will purge your Docker environment of components, configuration files and images used by the LOCKSS system.

### Installing Snap and MicroK8s

The LOCKSS system's containers are no longer orchestrated by Docker Swarm and no longer require Docker to run. The system now uses **MicroK8s**, a lightweight Kubernetes environment. To install the MicroK8s application package, you will need to install and use **Snap**. See [Installing Snap](../installing/snap) and [Installing MicroK8s](../installing/microk8s).

### Modifying the Environment

In order for LOCKSS 20.-alpha3 to work properly, you will need to disable frontends to `iptables` like `firewalld` or `ufw`, and configure MicroK8s to use DNS in a way that avoids loopback addresses. See [Disabling Packet Filters](firewall) and [Configuring DNS](../installing/dns) for details.

### Reconfiguring the System

Upon successful completion, you will prompted to run [`scripts/configure-lockss`](../configuring). **Be advised that the configuration process will prompt you for the PostgreSQL database password.**

### Starting LOCKSS

Once configuration is complete you can run lockss as usual with [`scripts/start-lockss`](../running)
