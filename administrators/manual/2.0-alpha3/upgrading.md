---
layout: page
title: Upgrading From LOCKSS 2.0-alpha2
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

If you have been using version 2.0-alpha2 of the LOCKSS system, an upgrade path has been provided to version 2.0-alpha3. 

## Install Microk8s
The LOCKSS daemon no longer runs in Docker Swarm or requires Docker.  It now runs in a packaged version of kubernetes, **Microk8s**. You will need to install Microk8s before updating. See [installing the LOCKSS system](installing/microk8s).

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
    sudo scripts/upgrade-alpha2-to-alpha3
```

The script will perform a number of system-level changes and need to be root.


## Re-Configure the System

Upon successful completion, you will prompted to run [`scripts/configure-lockss`](configuring). **Be advised that the configuration process will prompt you for the Postgres database password.**

## Start LOCKSS

Once configuration is complete you can run lockss as usual. [`scripts/start-lockss`](configuring)

