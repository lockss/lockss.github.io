---
layout: page
title: Contributing
---

Thank you for your interest in being a contributor to the [LOCKSS Program](https://www.lockss.org/).

## Code of Conduct

The LOCKSS Program has adopted the [Contributor Covenant](https://www.contributor-covenant.org/) code of conduct, to foster welcoming, diverse, and inclusive community spaces. By participating in this project you agree to abide by its terms.

*   [Contributor Covenant website](https://www.contributor-covenant.org/)
*   [Contributor Covenant version 1.4.1](https://www.contributor-covenant.org/version/1/4/code-of-conduct)
*   [Contributor Covenant translations](https://www.contributor-covenant.org/translations)
*   [Contributor Covenant frequently asked questions](https://www.contributor-covenant.org/faq)

## Software License

The LOCKSS Program's software is released under a [3-Clause BSD License](https://opensource.org/licenses/BSD-3-Clause). Copyright (c) 2000-2019, Board of Trustees of Leland Stanford Jr. University.

## Git Layout

The LOCKSS Program's Git repositories use a simplified Git Flow layout.

*   Stable releases are recorded on the `master` branch
*   Settled contributions are recorded on the `develop` branch, which should build successfully as close as feasible to all the time
*   In-progress development takes place off of the `develop` branch on feature branches with names beginning with `feature-`

*A page with a more detailed description of the LOCKSS Program's preferred Git layout is under construction.*

## Java Style Guide

A page with a more detailed description of the LOCKSS Program's preferred Java style is under construction, but a brief summary is:

*   LOCKSS software written in Java must be compatible with Java 8. *The classic LOCKSS daemon (version 1.x) must be compatible with Java 7.*
*   No tab characters should be present, only spaces (but extant tab characters should be displayed as 8 space characters)
*   Indentation is 2 space characters
*   Mandatory Egyptian-style curly braces

## Python Style Guide

A page with a more detailed description of the LOCKSS Program's preferred Python style is under construction, but a brief summary is:

*    LOCKSS software written for Python 2 requires Python 2.7. *There is currently no precise guideline for which version of Python is required for LOCKSS software written in Python 3.*
*    Shebang must be `/usr/bin/env python2` or `/usr/bin/env python3`; `/usr/bin/env python` is not allowed because some distributions map this to Python 2 and others to Python 3.
*   No tab characters should be present, only spaces (but extant tab characters should be displayed as 8 space characters)
*   Indentation is 4 space characters
