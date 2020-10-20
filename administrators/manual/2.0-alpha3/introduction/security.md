---
layout: page
title: Security Considerations
---

*   **Previous: [System Prerequisites](prerequisites)**
*   **Up: [Introduction](.)**
*   **Next: [Installing the LOCKSS System](../installing)**

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

**LOCKSS 2.0-alpha3 is a technology preview, not yet suitable for production environments.** Although the LOCKSS software itself and especially the LOCKSS peer-to-peer protocol remain as secure as ever, the operating environment for alpha versions of LOCKSS 2.0 is still being hardened. Please read about the security considerations below that are relevant as of LOCKSS 2.0-alpha3.

## Networking

LOCKSS 2.0-alpha3 is the first version of the LAAWS (LOCKSS Architected As Web Services) initiative deployed in a Kubernetes environment. The Kubernetes networking model is sophisticated and requires complex interactions with the host operating system's network and firewall stacks. LOCKSS 2.0-alpha3, for the purposes of demonstrating basic functionality, requires **disabling the host operating system's packet filters** (`iptables`, `firewalld` or `ufw`); integration with these packet filters will arrive in LOCKSS 2.0-alpha4.

## System Privileges

Likewise, to demonstrate basic functionality, LOCKSS 2.0-alpha3 runs as a dedicated `lockss` system user **with `sudo` privileges**. This requirement will be relaxed in future versions as we integrate better with the underlying operating system.
