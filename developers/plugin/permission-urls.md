---
layout: page
title: Permission URLs
---

*This page is under construction.*

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `au_permission_url`

## Value Type

Value type: string (`<string>`) or list (`<list>`) of strings.

The strings are `printf` format strings, accepting expressions made of plugin configuration parameter keys and a small language of functions modifying them (e.g. `url_host(...)` applied to a plugin configuration parameter of type URL, resulting in the host portion of the URL).

## Description

One or more URLs giving the LOCKSS software permission to crawl an AU, if permission is not given on the start URLs.

## Example

```xml
  <entry>
    <string></string>
    <string></string>
  </entry>
```
