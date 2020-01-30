---
layout: page
title: Installing OpenJDK 8
---

*This information applies to version 2.0-alpha2 of the LOCKSS system.*


## Installing OpenJDK 8 Runtime

### <a name="jdk8_ubuntu" id="jdk8_ubuntu"></a>Debian, Ubuntu, _etc._

On the command line, type:

> **$** sudo apt-get install openjdk-8-jre

### <a name="jdk8_fedora" id="jdk8_fedora"></a>Fedora, Oracle Linux, Red Hat Enterprise Linux, _etc._

On the command line, type:

> **$** su -c "yum install java-1.8.0-openjdk"

### <a name="jdk8_macos" id="jdk8_macos"></a>MacOS using Homebrew

On the command line, type:

> **$** brew cask install adoptopenjdk8

Set JAVAHOME to /Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk
