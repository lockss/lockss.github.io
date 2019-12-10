---
layout: page
title: Plugin Configuration Parameters
---

*This page is under construction.*

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin).**

## Key

Key: `plugin_config_props`

## Value Type

Value type: list of `<org.lockss.daemon.ConfigParamDescr>` stanzas

## Description

A plugin's rules and code (start and permission URLs, crawl rules, substance patterns...) are made general by identifying placeholders for AU-specific values and substituting them later. These placeholders for variable values are called plugin configuration parameters.

Defining the necessary configuration parameters for a given plugin comes mostly from studying the URL structure of the preservation target and identifying patterns.

Each plugin configuration parameter is represented by a `<org.lockss.daemon.ConfigParamDescr>` stanza that looks like this:

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>base_url</key>
        <displayName>Base URL</displayName>
        <description>Usually of the form http://&lt;journal-name&gt;.com/</description>
        <type>3</type>
        <size>40</size>
        <definitional>true</definitional>
        <defaultOnly>false</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

Each `<org.lockss.daemon.ConfigParamDescr>` contains the following important elements:

*   `<key>`: an identifier for the configuration parameter, appearing as the placeholder in rules and code.
*   `<type>`: an integer describing the type of value the configuration parameter represents. See below for details.

## Configuration Parameter Types

The valid integer values for a configuration parameter type (`<type>` element) are:

*   `1` for a non-empty **string**.
*   `2` for an **integer**. The integer can be negative. This is represented internally as a 32-bit integer.
*   `3` for a **URL**. Used most frequently as a URL prefix. This must be a valid URL string (as adjudicated by Java's `java.net.URL` constructor).
*   `4` for a four-digit **year**, or `0` for an unspecified year.
*   `5` for a **boolean**. The canonical values are `true` or `false`, although `yes`, `on` and `1` are recognized as `true` and `no`, `off` and `0` are recognized as `false`. All these strings are case-insensitive.
*   `6` for a **non-negative integer**. The integer can be zero but cannot be negative.
*   `7` for a **string range**. The range is specified with two strings separated by a dash (`-`). If there is a single string with no dash, the range is interpreted to be over that single string only.
*   `8` for a **numeric range**. The range is specified with two integers separated by a dash (`-`). If there is a single integer, the range is interpreted to contain that single integer only.
*   `9` for a **set**. The set is specified as a comma-separated list of strings, with empty strings between commas discarded, and whitespace between the commas and the beginnings and ends of strings trimmed. <!-- Todo: set macros -->
*   `10` for a colon-separated **username and password**.
*   `11` for a long integer. The value can negative. This is represented internally as a 64-bit integer.
*   `12` for a time interval (duration). Specified as a long integer followed by a suffix indicating a time unit: `ms` for milliseconds, `s` for seconds, `m` for minutes, `h` for hours, `d` for days, `w` for weeks (7 days), `y` for years (365 days). If there is no suffix, the default interpretation is milliseconds. The time unit suffixes are case-insensitive.

## Example

```xml
  <entry>
    <string>plugin_version</string>
    <string>7</string>
  </entry>
```

## See Also

<!-- TODO feature version map -->
