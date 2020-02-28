---
layout: page
title: Required Daemon Version
---

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `required_daemon_version`

## Value Type

Value type: string (`<string>`)

## Example

```xml
  <entry>
    <string>required_daemon_version</string>
    <string>1.74.7</string>
  </entry>
```

## Description

The release number of the earliest version of the LOCKSS software that supports all the features required by the plugin.

In the classic LOCKSS system (1.x), this is a string like `1.74.7` (version 1.74.7 or higher) or `1.74.0` (version 1.74.x or higher). In the rearchitected LOCKSS system (2.x), this is currently only `2.0-alpha1` or `2.0-alpha2`.
