---
layout: page
title: Checking the LOCKSS system.
---

*This information applies to version 2.0-alpha2 of the LOCKSS system.*

After [installing the LOCKSS system](installing) and [downloading the LOCKSS Installer](installing/lockss-installer), prepare  the system for running by typing:

    scripts/check_sys

The script will do its best to install any missing elements needed to run the LOCKSS cluster on the host machine. 
See the document [].

 1. Check for  Docker and install if missing.
 1. Check for the local-persist volume plugin for Docker and install if missing.
 1. Ensure Docker swarm is inited and running.
 1. Check for a user `lockss` and create the lockss user and group if missing.
