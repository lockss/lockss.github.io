---
layout: page
title: Plugin Name
---

*This page is under construction.*

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin).**

## Key

Key: `plugin_name`

## Value Type

Value type: string

## Description

A user-friendly string of text naming the plugin.

## Example

In the Global LOCKSS Netowrk (GLN), the plugin to process volumes of journals by Oxford University Press (OUP) hosted on the Silverchair platform has the name `Oxford University Press Plugin`.

```xml
  <entry>
    <string>plugin_name</string>
    <string>Oxford University Press Plugin</string>
  </entry>
```

*Find this plugin's source code at [https://github.com/lockss/lockss-daemon/blob/master/plugins/src/org/lockss/plugin/silverchair/oup/OupSilverchairPlugin.xml](https://github.com/lockss/lockss-daemon/blob/master/plugins/src/org/lockss/plugin/silverchair/oup/OupSilverchairPlugin.xml)*
