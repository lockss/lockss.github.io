---
layout: page
title: LOCKSS Plugin Concepts
---

*This page is under construction.*

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin).**

This page describes some of the concepts associated with LOCKSS plugins.

## Introduction

A **LOCKSS plugin** is a bundle of descriptors, rules and code loaded into the LOCKSS software, describing how to harvest and process a preservation target.

A preservation target might be an individual Web site, or a family of related Web sites (for instance all Web sites powered by the same content publishing platform), or a corpus of Web-accessible resources discovered through some interface (for example an OAI-PMH server, or a service with an API).

In almost all cases, the preservation target is preserved in plugin-defined slices called **archival units** (or **AUs** for short). What these slices are depends on the situation, but generally the goal is to split the preservation target into slices of manageable size that are expected to become unchanging eventually, for instance time-bound slices. For example, in a LOCKSS plugin for a preservation target that consists of serial publications, an AU could be equated with one volume or one year of one publication.

A LOCKSS plugin leaves placeholders in rules and code called **plugin configuration parameters**. An AU is identified by which plugin it uses, and by values for each of the parameters the plugin defines. When the parameter values for an AU are substituted for the placeholders in the plugin's rules and code, the result is rules and code suited for that specific AU.

Typical plugin parameters include a URL prefix or URL fragment (e.g. base URL, directory name, publication code...), a year or a date range, an identifier (e.g. ISSN of a journal, ISBN of a book, database identifier of an object...), a part number (e.g. volume number, numbered subdivision...), and more.

A LOCKSS plugin is expressed as a mapping from keys to values. Except for rare exceptions that are built into the LOCKSS software, LOCKSS plugins consist of an XML file and optional Java class files (compiled Java code), bundled together in a JAR file (a Zip file of Java class files and associated files).

### Plugin Complexity

A simplistic plugin will likely have at minimum:

*   Identifying elements, including configuration parameters.
*   Start URLs, an optionally, additional permission URLs.
*   Crawl rules.

If the preserved content contains variable or personalized HTML Web pages, it will likely need:

*   HTML filters

If extracting metadata from the preserved content into the LOCKSS metadata database is desired, the plugin will likely also need:

*   Metadata extraction elements, including an article iterator.

All other components are optional. Their use arises from either a preservation obstacle or a need specific to the preservation target. This manual gives some guidance about when certain components are needed and to what purpose.

### Plugins in the Classic LOCKSS System and in the Rearchitected LOCKSS System

Conceptually, LOCKSS plugins are the same in the classic LOCKSS system (LOCKSS 1.x) and in the rearchitected LOCKSS system (LOCKSS 2.x), although future features will only be developed for the rearchitected LOCKSS system without being backported to the classic LOCKSS system.

## Identifying Elements

All plugins define a number of identifying elements:

*   **Plugin identifier**: a unique identifier for the plugin.
*   **Plugin name**: a user-friendly name for the plugin.
*   **Plugin version**: the plugin's version number.
*   **Plugin configuration parameters**: a list of configuration parameter descriptors, defining the placeholders in use in the plugin's rules and code.
*   **AU name**: a rule to generate a default name for each AU, based on the plugin name and the plugin parameters.

## Crawl Control

The following plugin elements are involved in controlling how content is crawled:

*   **Start URLs**: one or more URLs from which the crawl of an AU begins.
*   **Crawl seed**: in lieu of a list of start URLs, a piece of code called a crawl seed can compute the starting points of the crawl of an AU, for instance by interacting with an API.
*   **Permission URLs**: one or more URLs giving the LOCKSS software permission to crawl an AU, if permission is not given on the start URLs.
*   **Crawl rules**: sequential rules determining if a URL discovered during the crawl of an AU should in turn be fetched as part of the AU or not.
*   **Crawl window**: a crawl window controls what times of day or days of the week crawls against the preservation target are allowed; by default an AU is eligible to crawl at any time.
*   **Recrawl interval**: the amount of time before an AU that has previously been crawled successfully is eligible to attempt crawling again.
*   **Fetch pause time**: the minimum amount of time between two fetches of consecutive URLs in the crawl of an AU.
*   **Crawl rate limiters**: crawl rate limiters define, at a finer grain than with the pause time alone, how fast a preservation target can be crawled.
*   **Response handlers**: custom actions taken if fetching a URL results in certain error conditions or HTTP response codes.
*   **URL normalizer**: a piece of code that normalizes URL variants into canonical URLs.
*   **Link extractors**: pieces of code that extract or extrapolate URLs from the processed content, other than those that would be extracted through standard means for a given media type.

## Crawl Validation

A plugin can optionally define elements that help verify that the crawl is obtaining the content it is supposed to:

*   **Login page checker**: determines if a URL fetched successfully (HTTP 200) is in fact a login page or some other undesirable substitute for the intended content.
*   **Content validators**: pieces of code that determines if certain URLs pass a validation test, most often a media type check or format validation test.
*   **Substance patterns**: pattern rules to check that at least one URL processed during the crawl of an AU is substantive (non-trivial), for example to verify that at least one substantive object was processed rather than just tables of contents.

## Content Filters

Many plugins designed to harvest and preserve Web-native content need to go to some lengths to enable the nodes in a LOCKSS network preserving the same AU to compare the URLs they have apples to apples. This is because fetching a given URL is likely to result in non-identical results from node to node, or from fetch to fetch on the same node, due to a raft of causes:

*   Advertising banners.
*   Personalization: "You are logged in as...", "Downloaded by..."
*   Time-variable content: current date, news ticker...
*   Location-variable content: content distribution network (CDN) URLs.
*   Related content widgets: "You may also be interested in..."
*   Reverse citations and pingbacks: "This page has been referenced by..."
*   Debugging information in the page source left behind by the Web publishing platform.
*   Tracking data and watermarking embedded in the content.
*   Temporary system messages: "The site will be down for maintenance from..."

and more. Some of these variations now appear outside HTML in media types like PDF or Microsoft PowerPoint files.

To canonicalize content before comparison between nodes in the LOCKSS audit and repair protocol, a plugin can define pieces of code called **content filters** for each affected media type. The LOCKSS plugin framework offers a variety of utility classes specifically for **HTML** and **PDF** filtering, as part of its general content filtering framework.

## Metadata Extraction

The LOCKSS plugin framework enables the extraction of metadata from ingested content, through an extensible metadata extraction framework; a plugin can optionally define:

*   **Article iterator**: a piece of code that traverses the AU and enumerates all the logical items (journal articles, electronic books, electronic theses and dissertations, repository objects...) found in it, as bundles of related URLs.
*   **Article metadata extractor**: a piece of code that extracts metadata from the logical items enumerated by the article iterator using file metadata extractors, and that post-processes and stores the extracted metadata in the LOCKSS metadata database.
*   **File metadata extractors**: pieces of code that extract metadata from a given file type.

## Web Replay

A plugin can define optional elements that are applied by the embedded ServeContent Web replay engine:

*   **Link rewriter**: a piece of code that intercepts certain links at ServeContent replay time and applies transformations to them, to improve the usability of some replayed Web-native content.

## References

*   Definition of [archival unit](/glossary#archival-unit) in the [LOCKSS Glossary](/glossary)
*   Definition of [plugin](/glossary#plugin) in the [LOCKSS Glossary](/glossary)
