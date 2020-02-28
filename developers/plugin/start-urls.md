---
layout: page
title: Start URLs
---

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `au_start_url`

## Value Type

Value type: string (`<string>`), or list (`<list>`) of strings

The strings are `printf` format strings, accepting expressions made of plugin configuration parameter keys and a small language of functions modifying them (e.g. `url_host(...)` applied to a plugin configuration parameter of type URL, resulting in the host portion of the URL).

## Example

```xml
  <entry>
    <string>au_start_url</string>
    <string>"%s%s/vol%s/index.html", base_url, journal_id, volume_name</string>
  </entry>
```

## Description

One or more URLs from which the crawl of an AU begins.
