---
layout: page
title: Recrawl Interval
---

*This page is under construction.*

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `au_def_new_content_crawl`

## Value Type

Value type: long integer (`<long>`)

## Description

The amount of time before an AU that has previously been crawled successfully is eligible to attempt crawling again.

Sample values:

*   `31449600000` for 52 weeks (364 days)
*   `1209600000` for 2 weeks (the most typical value in the Global LOCKSS Network)
*   `604800000` for 1 week
*   `86400000` for 24 hours day

## Example

```xml
  <entry>
    <string></string>
    <string></string>
  </entry>
```
