---
layout: page
title: Replaying Web Content with Pywb
---

*This information applies to version 2.0-alpha2 of the LOCKSS system.*

## Accessing the Pywb User Interface

Given that your primary hostname is `${HOST}`, you can use your browser to connect to the LOCKSS Pywb user interface (UI) at:

    http://${HOST}:8080

## Replaying a URL from the Pywb Interface

To view a URL from Pywb:

1.  The Pywb screen provides a list of links to available collections.  Click on the top-most collection which should be */lockss*.
1.  Enter the URL you want to replay in the URL search box.
1.  Click the *Search* button.
1.  Replay the most recent URL by clicking on the topmost entry of the third column.

## Finding a URL from an AU to replay

There are multiple ways to discover URLs belonging to an AU in the Configuration Service UI:

1.  Obtaining a URL by clicking on "pages fetched" inside of crawl status
    *  In the top-right menu, click *Daemon Status*.
    *  Open the control in the middle of the screen that says *Overview* and select *Crawl Status* from the drop down menu.
    *  Picking an AU from the active crawls, click on the number associated with *Pages Fetched* to bring up a list of URLs that have been crawled.
    *  Copy one of the URLs and paste it in the Pywb Interface as described previously.

1.  Obtaining a Substance URL
    *  In the top-right menu, click *Daemon Status*.
    *  Open the control in the middle of the screen that says *Overview* and select *Archival Units* from the drop down menu.  If prompted, enter your Username and Password again.  It will take a bit of time for the next screen to appear while the AU list is being built.
    *  Select an AU by clicking on the AU title in the first column.
    *  Open the *Substance URLs* link
    *  Copy one of the URLs and paste it in the Pywb Interface as described previously.

