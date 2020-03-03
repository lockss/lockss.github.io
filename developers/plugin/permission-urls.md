---
layout: page
title: Permission URLs
---

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `au_permission_url`

## Value Type

Value type: string (`<string>`), or list (`<list>`) of strings

The strings are `printf` format strings, accepting expressions made of plugin configuration parameter keys and a small language of functions modifying them (e.g. `url_host(...)` applied to a plugin configuration parameter of type URL, resulting in the host portion of the URL).

## Example

```xml
  <entry>
    <string>au_permission_url</string>
    <string>"%slockss.txt", base_url</string>
  </entry>
```

## Description

One or more URLs giving the LOCKSS software permission to crawl an AU, if permission is not given on the start URLs.
