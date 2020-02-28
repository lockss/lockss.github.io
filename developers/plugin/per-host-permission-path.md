---
layout: page
title: Per-Host Permission Path
---

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `plugin_per_host_permission_path`

## Value Type

Value type: string (`<string>`)

## Example

```xml
  <entry>
    <string>plugin_per_host_permission_path</string>
    <string>/lockss.txt</string>
  </entry>
```

## Description

Path where a permission statement may be found on hosts not listed in start URLs or permission URLs. Useful for sites such as Internet Archive that have banks of similar hosts with unpredictable names, but with a predictable path to the permission URL on each.
