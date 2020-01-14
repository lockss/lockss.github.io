---
layout: page
title: AU Name
---

*This page is under construction.*

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `au_name`

## Value Type

Value type: string (`<string>`)

The value is a `printf` format string, which can use plugin configuration parameter keys (e.g. `base_url`, `journal_issn`, `volume_name`) as values.

## Description

A rule to generate a default name for each AU, based on the plugin name and the plugin parameters.

The rule is used to generate a name for the AU if it is not listed in the title database (AU inventory).

Conventionally, this is made of a comma-separated list of the plugin name (value from `plugin_name`) and the display name and value of each configuration parameter from more general (e.g. `base_url`) to more specific (e.g. `volume_name`).

## Example

```xml
  <entry>
    <string></string>
    <string></string>
  </entry>
```
