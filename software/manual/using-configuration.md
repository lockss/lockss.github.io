---
layout: page
title: Using the LOCKSS Configuration Service
---

*This information does not apply to the classic LOCKSS daemon (version 1.x).*

## LOCKSS Configuration Service Web User Interface

If you are already connected to the Web user interface (UI) of another component of the LOCKSS System, click *Config Service* in the top-left menu.

Alternatively, if your primary hostname is `${HOST}`, you can use your browser to connect to the LOCKSS Configuration Service Web user interface (UI) at:

    http://${HOST}:24621

Enter your Web UI username and password to login if prompted.

## Concepts

### Archival Units

Content in the LOCKSS System is preserved in archival units (AUs) -- user-defined slices of data or Web crawls that represent a meaningful subdivision of preservable content. For serial content, for example scholarly journals, an AU might be a volume or a year of content.

### Title Database

The list of AUs available to be preserved, as well as their characteristics like cataloging/bibliographic information, which LOCKSS plugin is needed to process them, and the value of plugin-dependent parameters, is made available from the preservation network's title database. The title database is not really a database but rather a knowledge base.

## Adding Archival Units

To add AUs to the system for preservation:

1.  In the top-right menu, click *Journal Configuration*.
1.  In the center menu, click *Add AUs*.
1.  Select one or more title sets.
1.  Click the *Select AUs* button.
1.  Select one or more AUs.
1.  Click the *Add Selected AUs* button.

## Configuring a Crawl Proxy

If Web crawls must be routed through a Web proxy:

1.  In the top-right menu, click *Content Access Options*.
1.  In the center menu, click *Proxy Client Options*.
1.  Select the *Proxy crawls* checkbox.
1.  Enter the hostname and port of the Web proxy in the *HTTP Proxy host* and *Port* text areas, respectively.
1.  Click the *Update Proxy Client* button.
