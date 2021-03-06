---
layout: page
title: Plugin Version
---

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `plugin_version`

## Value Type

Value type: string (`<string>`), *not* integer

## Example

```xml
  <entry>
    <string>plugin_version</string>
    <string>7</string>
  </entry>
```
## Description

The plugin's version number.

The first release of a plugin is typically numbered 1, and the next revision 2, and so on, although the releases do not have to be numerically consecutive as long as they only go up with time.

Although only the numeric part is important, the integer can be followed by a hyphen and an arbitrary string, which is why this value type is a string and not an integer.
