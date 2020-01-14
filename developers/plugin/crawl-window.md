---
layout: page
title: Crawl Window
---

*This page is under construction.*

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `au_crawlwindow`, `au_crawlwindow_ser`

## Value Type

`au_crawlwindow` value type: string (`<string>`) representing a fully-qualified class name implementing the `org.lockss.plugin.definable.DefinableArchivalUnit.ConfigurableCrawlWindow` interface, which is a factory for the `org.lockss.daemon.CrawlWindow` interface.

`au_crawlwindow_ser` value type: a serialized `org.lockss.daemon.CrawlWindow` object.

## Description

A crawl window controls what times of day or days of the week crawls against the preservation target are allowed; by default an AU is eligible to crawl at any time.

## Example

```xml
  <entry>
    <string></string>
    <string></string>
  </entry>
```
