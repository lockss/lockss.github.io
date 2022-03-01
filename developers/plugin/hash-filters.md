---
layout: page
title: Introduction to Hash Filters
---

*This page is under construction.*

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `<mediatype>_filter_factory` (for example `text/html_filter_factory`)

## Value Type

Value type: string (`<string>`)

The string is the fully-qualified name of a Java class implementing the `org.lockss.plugin.FilterFactory` interface.

## Description

To canonicalize content before comparison between nodes in the LOCKSS audit and repair protocol, a plugin can define a hash filter for each affected media type. The goal is to pre-process content so that it is fit for a **logical comparison** between nodes, even if different nodes do not have byte-identical versions. This occurs frequently in HTML content that has personalizations ("You are logged in as..."), advertising, and other variable content ("You may also be interested in...", "Top 10 viewed articles this week...", "Recently added articles...") other than the main content. It can be needed for other media types like PDF and RIS because of dynamic timestamping, and other server behaviors.

The `org.lockss.plugin.FilterFactory` interface defines a `createFilteredInputStream` method that accepts an `org.lockss.plugin.ArchivalUnit` object, an `InputStream` of the URL's raw content, and a string representing the byte encoding, and returns an `InputStream` of the canonicalized byte stream, which does not need to be a valid object of that media type (it is only used to compute a checksum).

The LOCKSS plugin framework offers a variety of utility classes specifically for [HTML](html-filters) and [PDF](pdf-filters) filtering, as part of its general content filtering framework.

## Example

```xml
  <entry>
    <string></string>
    <string></string>
  </entry>
```
