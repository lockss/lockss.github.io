---
layout: page
title: LOCKSS Program Web Harvest Guidelines
---


_Version: Sept 2025_

_Archived: [https://lockss.github.io/clockss-web-harvest-guidelines](https://lockss.github.io/clockss-web-harvest-guidelines)_
<!--![CLOCKSS Logo](/images/clockss-logo.png)-->


## Overview

The LOCKSS software can use web harvesters to programmatically discover and collect content from your website. In order to support this method of preservation, the following general conditions must be met:



1. Programmatically-discoverable permission statements for each base host used for substantive content.
2. Programatically discoverable finite sets of content. Preservation is based on collecting a unit of content with components that cease to grow at some point. This could be a volume or year of articles for one journal, or a single book with all its chapters, or all the datasets deposited over a certain period of time.
3. A website that enables a preservation crawler to discover and collect all the items in the defined set of content at static URIs. This could be through a browsable website that uses a logical consistent link structure and in which every item to be preserved can be reached through at least one static text link even if site behavior is enhanced with dynamic elements. Alternatively, this could be through the use of an access API, such as OAI-PMH, that allows the crawler to generate a list of access points for all the items to be preserved.
4. Programmatically-discoverable metadata for each preserved item that can be used to identify the preserved contents.


## Details


### Permission statements

In the majority of cases, there must be a permission statement for each domain serving substantive content. 
The permission statement(s) need not be visible and could be an html comment embedded in an appropriate web page.
The permission statement(s) should appear conditionally depending on if the crawler has access to content.

The standard CLOCKSS permission statement is:

*  CLOCKSS system has permission to ingest, preserve, and serve this Archival Unit

The open access CLOCKSS permission statement is:

*  CLOCKSS system has permission to ingest, preserve, and serve this open access Archival Unit

The standard Global LOCKSS Network permission statement is:

*  LOCKSS system has permission to collect, preserve, and serve this Archival Unit

The open-access Global LOCKSS Network permission statement is:

*  LOCKSS system has permission to collect, preserve, and serve this open access Archival Unit


Note:

*  No permission statement is required for CDN support for auxiliary files.

*  For open access content, the permission statement could be a legal Creative Commons license including the ‘rel=“license”’ attribute.

*  When all the content at the site is open access or available for preservation, it is 
sufficient to have one permission statement somewhere under the domain instead of at the starting point
for each set or volume or year of content.


### Defined content sets and starting points for collection

For harvest, the crawler needs to be able to collect content and have a point in time at which that collection is complete with a repeatable, defined set of components. The crawler needs to be able to determine a start URI or URIs for this content based on information unique to the content. This might be a URI defined by the domain, the journal identifier, and a particular volume or year, such as:

*   https://www.publisher.com/journals/xyz/12
*   https://www.publisher.journalid.com/content?year=2017
*   https://www.publisher.com/ebooks/isbn/97811111111
*   https://www.publisher.com/ebooks?search&year=2017&order=newest_first

In some cases, such as when the website does not normally provide content in defined units, the start page might be an artificial manifest page provided for the purposes of preservation, such as:



*   https://www.publisher.com/xyz/lockss_manifest?volume=27

Or, if the website supports an API, the crawler can generate a request that returns and XML response that can be parsed for a list of all the article URIs associated with a given set of content, such as:



*   https://www.publisher.com/api/search?type=data_sets&publication_start=2019-03-01&publication_end=2019-04-01


### Site behavior



*   Make your content discoverable by a crawler by building your site with a logical link structure. Every page should be reachable from at least one static text link or have consistent identifiable tags in the html from which links can be generated. You can use a text browser, such as Lynx, to examine your site. If dynamic web features or server side processing keep you from accessing your entire site in a text browser, then preservation is likely to be impaired.
*   Use unchanging canonical links for content even if the content is served through single-use redirection. Preservation requires that the same URI will serve equivalent content in the future.
*   Use HTTP codes as expected: 5xx codes to indicate temporary errors that should be retried soon, 4xx codes to indicate permanent errors that should not be retried for some time, and 3xx redirects for each URI to its new location in the event that you need to move content.
*   Use if-modified-since headers so new content is identified and preserved.
*   Content from CDNs should have a stable URI.


### Required metadata



*   For scholarly publication content, such as articles or books, please provide basic bibliographic metadata in a non-proprietary machine-readable format, such as the HTML metadata tags, RIS, or XML files.
*   The metadata for scholarly content should include: DOI, publication, publication date, ISSN or ISBN and as appropriate: publication title, item title, series title, volume, issue and page number.
*   For items other scholarly published content, the metadata should provide enough information to uniquely identify the item - DOI if applicable or proprietary identifier, provider and so forth.


### IP Addresses

The following CLOCKSS IP addresses need to be enabled to access the full text of the content to be preserved:


*   171.66.236.0/24 (i.e. 171.66.236.0 through 171.66.236.255) Stanford University
*   128.42.174.11 Rice University
*   128.42.174.12 Rice University
*   128.42.151.15 Rice University
*   128.42.151.16 Rice University
*   156.56.241.164 Indiana University
*   156.56.241.166 Indiana University
*   129.215.128.111 University of Edinburgh
*   129.215.128.112 University of Edinburgh
*   129.215.128.113 University of Edinburgh
*   129.215.128.114 University of Edinburgh


Note: If you use the IP Registry to manage IP access to your site, please enable access to two organizations: LOCKSS Program and CLOCKSS Archive. "LOCKSS Program" contains the range at Stanford University from which most of our operations occur, and "CLOCKSS Archive" contains the other necessary IP addresses located at our network nodes. To be clear, content will only be included in the CLOCKSS Archive.

