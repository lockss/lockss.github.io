---
layout: page
title: Checking the LOCKSS System
---

*   **Previous: [Configuring DNS](dns)**
*   **Up: [Installing the LOCKSS System](.)**
*   **Next: [Configuring the LOCKSS System](../configuring)**

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

After [installing the LOCKSS system](index), you can confirm the status of installed components by running:

```bash
    sudo scripts/check-sys
```

in the `lockss-installer` directory.

The script will do its best to check for any missing elements and permissions needed to run the LOCKSS cluster on the host machine.

1.  Check for Snap
1.  Check for MicroK8s
1.  Check for a user `lockss`.
1.  Check user `lockss` has appropriate group memberships and permissions.
