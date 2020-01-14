---
layout: page
title: Crawl Seed
---

*This page is under construction.*

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `plugin_craw_seed_factory`

## Value Type

Value type: string (`<string>`)

The string is the fully-qualified name of a Java class implementing the `org.lockss.crawler.CrawlSeedFactory` interface, which is a factory for the `org.lockss.crawler.CrawlSeed` interface.

## Description

In lieu of a list of start URLs, code called a crawl seed can compute the starting points of the crawl of an AU, for instance by interacting with an API.

## Example

```xml
  <entry>
    <string></string>
    <string></string>
  </entry>
```
