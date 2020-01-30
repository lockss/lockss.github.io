---
layout: page
title: Upgrading a LOCKSS 2.0 alpha1 System
---

*This information applies to version 2.0-alpha2 of the LOCKSS system.*

If you have been using version 2.0-alpha1 of the LOCKSS system an upgrade path
has been provided to version 2.0-alpha2.

### Prerequisites
See [installing the LOCKSS system](installing). Additionally you will need to
[install OpenJDK8](installing/openjdk8)

### Download the latest release from the master branch of lockss-installer
On the command line in your lockss-installer directory, type:

> **$** git checkout master

> **$** git pull

### Run the upgrade command
On the command line, type:

> **$** sudo ./scripts/upgrade-alpha1-to-alpha2

#### The script will perform a number of system level changes and must be made as root.
1. Load the existing config.info and rewrite with new properties system.cfg
2. Shutdown any running stack(s)
3. Rename the old persistent data storage directories.
4. Update the sql database with new database names.
5. Remove any old installed docker configurations, volumes or networks.  This will
not remove any docker secrets and will not remove the persistent data store.
6. Update alpha1 SOLR to alpha2 SOLR.  This is a long running process that needs to update the schema and reindex. Please be patient.
7. Restore file ownership.

#### Upon successful completion

You will prompted to run [./configure-lockss](configuring) to check and if necessary update configuration values.

