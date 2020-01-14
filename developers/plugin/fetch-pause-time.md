---
layout: page
title: Fetch Pause Time
---

*This page is under construction.*

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `au_def_pause_time`

## Value Type

Value type: long integer (`<long>`)

## Description

The minimum amount of time between two fetches of consecutive URLs in the crawl of an AU, in milliseconds.

The most common value in the Global LOCKSS Network is `3000` for no more frequently than every 3 seconds.

## Example

```xml
  <entry>
    <string></string>
    <string></string>
  </entry>
```
