---
layout: page
title: Installing The Classic LOCKSS System 
---

To get back to the Classic LOCKSS Homepage use [this link](../index.md)

### Linux:

The deployment of LOCKSS box starts with the installation of an RHEL7 or RHEL8 Linux Variant (minimal install group or better) and the attachment of one or more dedicated data storage filesystems. The amount of RAM and disk space needed depends on the LOCKSS network that the LOCKSS box is deployed into. If your institution has a standard RHEL7 or RHEL8 (or variant) Linux image, go ahead and use that. RHEL9 is currently being tested and not recommended at this time.

### Network:

For network planning purposes, it’s important to know that the LOCKSS application is a peer-to-peer application which needs to accept inbound network connections from the internet.  A dedicated IP address should be assigned to the LOCKSS box and all inbound and outbound traffic should use the dedicated IP address.  Use of NAT is supported as long as the dedicated external IP address is used for both inbound and outbound network traffic.

### LOCKSS Integration:

The LOCKSS team provides a LOCKSS integration script to run to enable your Linux deployment to run the LOCKSS software.  Integration scripts are available for both RHEL7 and RHEL8 variants. Contact LOCKSS Support team for a copy of the integration scripts.

