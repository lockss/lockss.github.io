---
layout: page
title: LOCKSS Glossary
---

Each heading has a URL that is derived from the corresponding title heading:

*   Plugin -> http://lockss.github.io/glossary#plugin
*   Archival Unit -> http://lockss.github.io/glossary#archival-unit

## Archival Unit

Abbreviation: **AU**

Content in the LOCKSS system is grouped into archival units (AUs). AUs are user-defined subdivisions of content, preferably finite in scope, that delineate a meaningful grouping of items or data being preserved together. For instance, if the content to be preserved is serial scholarly content from an academic journal, an AU may be defined as a volume or a year's worth of content.

Because the LOCKSS system first arose in the context of preserving Web-based scholarly content, AUs are still arranged in titles, which are arranged in publishers. One can think of publishers as naming the content-producing entity (publisher, institution...), titles as naming a collection (publication, type of content...), and AUs as naming tranches of content in that collection (volume, year, range...).

Each AU is governed by a LOCKSS [plugin](#plugin) and listed in the [title database](#title-database).

## Plugin

A LOCKSS plugin is a bundle of descriptors, rules and code loaded into the LOCKSS software, describing how to harvest and process a preservation target.

References:

*   [LOCKSS Plugin Developer Manual](/developers/plugin)
*   [Plugin Concepts](/developers/plugin/plugin-concepts) section of the [LOCKSS Plugin Developer Manual](/developers/plugin)

## Title Database

The list of [archival units](#archival-unit) (AUs) available to be preserved, as well as their characteristics like cataloging/bibliographic information, which LOCKSS [plugin](#plugin) is needed to process them, and the value of plugin-dependent parameters, is made available from the preservation network's title database.

The title database is not really a database but rather a knowledge base. Currently, the LOCKSS software consumes it in the form of one or more XML files called title database XML files. There are different techniques to generate these title database XML files. The LOCKSS Team represents AU information in text files called TDB files, which are then translated into XML. The MetaArchive Cooperative keeps AU information in a Web application called the Conspectus Database, which generates XML. Other entities developed their own tools to produce XML.
