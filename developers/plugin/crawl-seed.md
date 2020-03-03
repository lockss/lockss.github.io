---
layout: page
title: Crawl Seed
---

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `plugin_craw_seed_factory`

## Value Type

Value type: string (`<string>`)

The string is the fully-qualified name of a Java class implementing the `org.lockss.crawler.CrawlSeedFactory` interface.

## Example

```xml
  <entry>
    <string>plugin_craw_seed_factory</string>
    <string>edu.example.plugin.publisherx.PublisherXCrawlSeedFactory</string>
  </entry>
```

## Description

In lieu of a list of start URLs, code called a crawl seed can compute the starting points of the crawl of an AU, for instance by interacting with an API.

*This section is under construction.*
