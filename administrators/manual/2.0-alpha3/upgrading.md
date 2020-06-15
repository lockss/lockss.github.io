---
layout: page
title: Upgrading From LOCKSS 2.0-alpha1
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

If you have been using version 2.0-alpha1 of the LOCKSS system, an upgrade path has been provided to version 2.0-alpha3.

## Pre-Requisites

See [installing the LOCKSS system](installing). Additionally you will need to
[install OpenJDK8](installing/openjdk8) on the host machine[<sup>1</sup>](#n1).

## Update `lockss-installer`

On the command line in the `lockss-installer` directory, type:

```bash
    git checkout master

    git pull
```

to update to the latest version of `lockss-installer` from GitHub.

## Run the Upgrade Command

On the command line in the `lockss-installer` directory, type:

```bash
    sudo scripts/upgrade-alpha1-to-alpha3
```

The script will perform a number of system-level changes and need to be root.

These adjustments include renaming `config.info` to `system.cfg`, shutting down a running system stack, renaming storage directories, updating database names, run the Solr upgrader tool from 2.0-alpha1 to 2.0-alpha3 (which is a long running process; please be patient), and change file ownerships, all of which to align the system with the 2.0-alpha3 environment.

## Re-Configure the System

Upon successful completion, you will prompted to run [`scripts/configure-lockss`](configuring). **Be advised that the configuration process will prompt you for the Postgres database password.**

----

#### Footnotes

<a name="n1" id="n1">[1]</a> This dependency on Java is temporary for 2.0-alpha3. It is necessary to run the Solr upgrader tool. In 2.0-alpha3, the process will be packaged in such a way that it does not depend on Java on the host machine.
