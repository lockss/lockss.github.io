---
layout: page
title: Using the LOCKSS Crawler Service
---

*This page is under construction. This information does not apply to the classic LOCKSS daemon (version 1.x).*

## Accessing the Web User Interface

In the LOCKSS 2.0 Alpha release, the main crawler runs as part of the [LOCKSS Poller Service](using-poller.md).

If you are already connected to the Web user interface (UI) of another component of the LOCKSS System, click *Crawler Service* in the top-left menu.

Alternatively, if your primary hostname is `${HOST}`, you can use your browser to connect to the LOCKSS Crawler Service Web user interface (UI) at:

    http://${HOST}:24651

Enter your Web UI username and password to login if prompted.

## Monitoring Crawl Status in the System

The Crawl Status of all configured AUs is available in the Archival Unit table

1.  In the top-right menu, click *Daemon Status*.
1.  Open the control in the middle of the screen that says *Overview* and select *Archival Units* from the drop down menu.
    * If prompted, enter your Username and Password again.
    * It will take a bit of time for the next screen to appear while the AU list is being built.
1.  The Archival Units screen lists statistics for each configured AU
    * the *Last Successful Crawl* column provides a timestamp of the most recent sucessful crawl.
    * the *Last Crawl Start* column provides a timestamp of the last attempted crawl.
    * the *Last Crawl Result* column provides the exit status of the last attempted crawl.

## Causing an Archival Unit to Crawl

Archival units (AUs) that have been added to the system for preservation crawl periodically, but you can cause an AU to crawl on demand:

1.  In the top-right menu, click *Debug Panel*.
1.  Select an AU in the *AU Actions: select AU* drop-down list.
1.  Click the *Start Crawl* button.
1.  If the AU has crawled recently, you will be prompted to confirm that you wish to override the usual recrawl interval by clicking on the *Force Start Crawl* button.

## Crawl Status Screen

To inspect the state of crawls, access the *Crawl Status* screen:

1.  In the top-right menu, click *Daemon Status*.
1.  In the center drop-down list, select *Crawl Status*. Alternatively, in the center overview, click on the second line, which says "*N active crawls*".

### Top-Level Crawl Information

The top left of the Crawl Status table contains the number of active, successful or failed crawls, and a countdown until the next time the system will look at the AUs being preserved and pick some that are ready to crawl or recrawl.

### Crawl Status Entry

Each line in the Crawl Status table contains:

*   The name of the AU
*   The type of crawl
*   The start time of the crawl
*   The duration of a finished or in-progress crawl
*   The status of the crawl
*   The number of bytes fetched over the network as part of the crawl
*   The number of URLs fetched as part of the crawl
*   The number of URLs parsed for more links
*   The number of URLs remaining to be fetched as part of this crawl
*   The number of URLs encountered as part of this crawl but excluded from being fetched
*   The number of URLs fetched as part of the crawl, that received an HTTP Not Modified response
*   The number of URLs that caused errors as part of this crawl
*   The number of different content types encountered as part of the crawl

Most of these values can be clicked to see a list of the corresponding objects.
