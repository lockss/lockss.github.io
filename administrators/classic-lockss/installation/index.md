---
layout: page
title: Installing The Classic LOCKSS System 
---

To get back to the Classic LOCKSS Homepage use [this link](../index.md)

### Linux:

The deployment of LOCKSS box starts with the installation of an RHEL7 Linux Variant (minimal install group or better) and the attachment of one or more dedicated data storage filesystems. The amount of RAM and disk space needed depends on the LOCKSS network that the LOCKSS box is deployed into. If your institution has a standard RHEL 7 (or variant) Linux image, go ahead and use that. RHEL 8 is currently being tested and not recommended at this time

### Network:

For network planning purposes, it’s important to know that the LOCKSS application is a peer-to-peer application which needs to accept inbound network connections from the internet.  A dedicated IP address should be assigned to the LOCKSS box and all inbound and outbound traffic should use the dedicated IP address.  Use of NAT is supported as long as the dedicated external IP address is used for both inbound and outbound network traffic.

### LOCKSS Integration:

The LOCKSS team provides a LOCKSS integration script to run to enable your Linux deployment to run the LOCKSS software.  Integration scripts are available for both RHEL6 and RHEL7 variants. Contact LOCKSS Support team for a copy of the integration scripts.




## News

*   **2019-05-13** - **LOCKSS 2.0-Alpha Available for Testing** - The LOCKSS Program is pleased to announce that LOCKSS 2.0-alpha is now available for testing. [**Read more...**](releases/2.0-alpha)

*   **2019-04-05** - **LOCKSS 2.0-Alpha Technology Preview** - At the 2019 LOCKSS Alliance Meeting, the LOCKSS engineering team presented a Technology Preview of the upcoming LOCKSS 2.0-alpha release. [**Read more...**](releases/2.0-alpha-preview)
