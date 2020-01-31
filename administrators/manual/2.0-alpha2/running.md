---
layout: page
title: Running the LOCKSS System
---

*This information applies to version 2.0-alpha2 of the LOCKSS system.*

After [configuring the LOCKSS system] and anytime after updating the LOCKSS Installer to a new version and stopping your LOCKSS stack:

#### Starting the LOCKSS system
* Run `scripts/start-lockss`: This script will calls in turn:

    *  `scripts/generate-lockss`. This script takes your configuration data and turns into into a set of configuration files containing the right values.
    *  `scripts/assemble-lockss`. This script puts the configuration files and puts them in the right places, and ensures that all storage volumes are ready for use (creating them if necessary).
    *  `scripts/deploy-lockss`. This script deploys your LOCKSS stack by invoking Docker.


#### Shutting down the LOCKSS system

*  `scripts/shutdown-lockss`

#### To restart a running or shut down LOCKSS 2.0-alpha2 cluster:
*  `scripts/restart-lockss`

#### To remove all configurations, volumes and networks installed by LOCKSS from Docker.
* Run `scripts/uninstall-lockss`: Remove all lockss elements from docker. This will **not** remove files from the persistent store.