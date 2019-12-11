---
layout: page
title: Installing Pystache
---

*This information applies to version 2.0-alpha1 of the LOCKSS system.*

[Pystache](http://defunkt.io/pystache/) is the reference implementation of the [Mustache](https://mustache.github.io/) templating language in Python. This page will walk you through the simple process of installing Pystache. The Pystache Python module depends on the Setuptools Python module.

You can install Pystache from [PyPI](https://pypi.org/) using Pip:

    sudo pip install setuptools pystache

Verify that Pystache is installed correctly:

    pystache --help

You should see a help message about Pystache, for example:

    Usage: pystache [-h] template context

    Render a mustache template with the given context.

    positional arguments:
      template    A filename or template string.
      context     A filename or JSON string.

    Options:
      -h, --help  show this help message and exit
