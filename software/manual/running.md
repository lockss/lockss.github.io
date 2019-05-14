---
layout: page
title: Running the LOCKSS System
---

*This information does not apply to the classic LOCKSS daemon (version 1.x).*

After [configuring the LOCKSS system] and anytime after updating the LOCKSS Installer to a new version and stopping your LOCKSS stack:

1.  Run `scripts/generate-lockss`. This script takes your configuration data and turns into into a set of configuration files containing the right values.

1.  Run `scripts/assemble-lockss`. This script puts the configuration files and puts them in the right places, and ensures that all storage volumes are ready for use (creating them if necessary).

1.  Run `scripts/deploy-lockss`. This script deploys your LOCKSS stack by invoking Docker.
