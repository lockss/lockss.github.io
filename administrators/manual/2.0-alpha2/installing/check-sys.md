---
layout: page
title: Checking the LOCKSS system
---

*This information applies to version 2.0-alpha2 of the LOCKSS system.*

After [installing the LOCKSS system](index) and [downloading the LOCKSS Installer](installing/lockss-installer), prepare  the system for running by typing:

```bash
    scripts/check_sys
```

in the `lockss-installer` directory.

The script will do its best to install any missing elements needed to run the LOCKSS cluster on the host machine. See the  [System Pre-Requisites](system-pre-requisites) document for required system elements.

1.  Check for Docker and install if missing.
1.  Check for the Local-Persist Docker volume plugin and install if missing.
1.  Ensure Docker Swarm is initialized and running.
1.  Check for a user `lockss` and create the `lockss` user and group if missing.