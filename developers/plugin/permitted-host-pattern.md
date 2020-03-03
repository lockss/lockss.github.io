---
layout: page
title: Permitted Host Pattern
---

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `au_permitted_host_pattern`

## Value Type

Value type: string (`<string>`), or list (`<list>`) of strings

## Example

```xml
  <entry>
    <string>au_permitted_host_pattern</string>
    <string>"cdnjs\.cloudflare\.com|fast\.fonts\.net"</string>
  </entry>
```

## Description

Pattern rules to allow collection from hosts that cannot explicitly grant permission, such as content distribution network hosts used to distribute standard components used by Web sites, such as Javascript libraries.

*This section will be expanded to better explain how to use this feature with crawl rules.*
