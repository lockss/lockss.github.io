---
layout: page
title: Upgrading to Java 8
---

*To get back to the Classic LOCKSS Homepage use [this link](./index.md)*

**Beginning with version 1.75, the classic LOCKSS daemon requires Java 8.** This page outlines the process to upgrade from Java 7 to Java 8.

## Upgrade instructions

*This document outlines the upgrade process for CentOS/RHEL 7 only. For CentOS/RHEL 6 and below these instructions will not work. Please email lockss-support@lockss.org for further instructions.*

1.  Check the currently installed Java version:
    
        java -version
    
    If the output indicates a version number beginning with 1.8, Java 8 is already installed, no further action is needed. Example:
    
        openjdk version "1.8.0_265"
        OpenJDK Runtime Environment (build 1.8.0_265-b01)
        OpenJDK 64-Bit Server VM (build 25.265-b01, mixed mode)
    
    If the output indicates a version number beginning with 1.7, Java 7 needs to be uninstalled and Java 8 installed. Example:
    
        java version "1.7.0_261"
        OpenJDK Runtime Environment (IcedTea 2.6.22) (Arch Linux build 7.u261_2.6.22-1-x86_64)
        OpenJDK 64-Bit Server VM (build 24.261-b02, mixed mode)

2.  Login as root (or gain root privilege)

3.  Stop the LOCKSS daemon:
    
        systemctl stop lockss

4.  Uninstall Java 7; the two versions can live alongside each other but we recommend uninstalling Java 7:
    
        yum remove java-1.7.0-openjdk
        yum remove java-1.7.0-openjdk-headless
    
    If you installed the Java 7 JDK, remove it too:
    
        yum remove java-1.7.0-openjdk-devel

5.  Install the Java 8 JRE:
    
        yum install java-1.8.0-openjdk

6.  Verify that Java 8 is installed by checking the version number:
    
        java -version

7.  Restart the LOCKSS daemon:

        systemctl start lockss
