---
layout: page
title: Downloading the LOCKSS Installer
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

You can download the LOCKSS Installer from GitHub using a [Git](git) command, as the `lockss` user:

```bash
git clone https://github.com/lockss/lockss-installer
```

You can then enter the `lockss-installer` directory:

```bash
cd lockss-installer
```
## Frequently Asked Questions

**How do I become the `lockss` user to type this command?**

We recommend this command:

```bash
sudo -u lockss /bin/bash
```

Also, we recommend issuing this command:

```bash
cd
```

before any others, to change to the `lockss` user's home directory, which is likely to be where the LOCKSS Installer is located.
