---
layout: page
title: Python Style Guide
---

A page with a more detailed description of the LOCKSS Program's preferred Python style is under construction, but a brief summary is:

*    LOCKSS software written for Python 2 requires Python 2.7. *There is currently no precise guideline for which version of Python is required for LOCKSS software written in Python 3.*
*    Shebang must be `/usr/bin/env python2` or `/usr/bin/env python3`; `/usr/bin/env python` is not allowed because some distributions map this to Python 2 and others to Python 3.
*   No tab characters should be present, only spaces (but extant tab characters should be displayed as 8 space characters)
*   Indentation is 4 space characters

