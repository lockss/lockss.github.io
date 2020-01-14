---
layout: page
title: URL Normalizer
---

*This page is under construction.*

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `au_url_normalizer`

## Value Type

Value type: string (`<string>`)

The value is a fully-qualified class name that implements the `org.lockss.plugin.UrlNormalizer` interface.

## Description

A URL normalizer maps URL variants to a canonical representation, for example by re-arranging equivalent URL query strings into a canonical order, removing extraneous URL substrings (for instance session IDs), canonicalizing the case (for instance to lowercase), etc. so that equivalent variants are stored only once under the canonical name.

## Example

```xml
  <entry>
    <string></string>
    <string></string>
  </entry>
```
