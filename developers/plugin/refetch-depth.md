---
layout: page
title: Refetch Depth
---

*This page is under construction.*

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `au_refetch_depth`

## Value Type

Value type: integer (`<int>`)

## Description

Number of links away from a start URL that will be fetched by normal crawls. Deep crawls may be used to cause all URLs in an AU to be refetched (subject to `If-Modified-Since`).

## Example

```xml
  <entry>
    <string></string>
    <string></string>
  </entry>
```
