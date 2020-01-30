---
layout: page
title: Using the LOCKSS Configuration Service
---

*This page is under construction.*

*This information applies to version 2.0-alpha2 of the LOCKSS system.*

## Accessing the Web User Interface

If you are already connected to the Web user interface (UI) of another component of the LOCKSS System, click *Config Service* in the top-left menu.

Alternatively, if your primary hostname is `${HOST}`, you can use your browser to connect to the LOCKSS Configuration Service Web user interface (UI) at:

    http://${HOST}:24621

Enter your Web UI username and password to login if prompted.

## Adding Archival Units

To add AUs to the system for preservation:

1.  In the top-right menu, click *Journal Configuration*.
1.  In the center menu, click *Add AUs*.
1.  Select one or more collections of AUs by selecting the checkbox next to the appropriate collection.
1.  Click the *Select AUs* button.
    * It may take a bit of time (60+ seconds) for the next screen to appear, while the list of AUs is built.
1.  Select one or more AUs from the AU list. You may click *Select All* if you'd like to select all AUs.
    * If you choose to use *Select All* then please note that the next step may take some time.
1.  Click the *Add Selected AUs* button.
    * The time it takes for the page to refresh depends on the number of AUs added. Give the LOCKSS Daemon some time to load the AUs and reload the page before moving on.
1. A screen will show a list of added AUs. Crawling of these new AUs will start automatically - no further action is necessary.

## Configuring a Crawl Proxy

If Web crawls must be routed through a Web proxy:

1.  In the top-right menu, click *Content Access Options*.
1.  In the center menu, click *Proxy Client Options*.
1.  Select the *Proxy crawls* checkbox.
1.  Enter the hostname and port of the Web proxy in the *HTTP Proxy host* and *Port* text areas, respectively.
1.  Click the *Update Proxy Client* button.

## Managing Access to the Web User Interfaces

*This section is under construction.*


