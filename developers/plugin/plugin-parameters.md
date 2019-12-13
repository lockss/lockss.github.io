---
layout: page
title: Plugin Configuration Parameters
---

*This page is under construction.*

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `plugin_config_props`

## Value Type

Value type: list (`<list>`) of `<org.lockss.daemon.ConfigParamDescr>` stanzas

## Description

A plugin's rules and code (start and permission URLs, crawl rules, substance patterns...) are made general by identifying placeholders for AU-specific values and substituting them later. These placeholders for variable values are called plugin configuration parameters.

Defining the necessary configuration parameters for a given plugin comes mostly from studying the URL structure of the preservation target and identifying patterns.

Each plugin configuration parameter is represented by a `<org.lockss.daemon.ConfigParamDescr>` stanza that looks like this:

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>...</key>
        <type>...</type>
        <displayName>...</displayName>
        <description>...</description>
        <size>...</size>
        <definitional>...</definitional>
        <defaultOnly>...</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

Each `<org.lockss.daemon.ConfigParamDescr>` contains the following important elements:

*   `<key>`: the **parameter key**, an identifier for the configuration parameter, standing in as a placeholder for the AU-specific value in rules and code.
*   `<type>`: the **parameter type**, an integer describing the type of value the configuration parameter represents (string, integer, etc.). See the [Parameter Types](#parameter-types) section below for details.
*   `<definitional>`: whether the parameter is a **definitional parameter**, expressed as the boolean strings `true` or `false`. Most parameters are definitional (`true`), meaning the parameter is part of the set of parameters that together form the unique identity of the AU.
*   `<defaultOnly>`: set to `false` in almost all cases.

The other elements play a role in the manual AU creation screen in the LOCKSS Web user interface:

*   `<displayName>`: the **parameter display name**, a user-friendly name for the parameter in the LOCKSS Web user interface.
*   `<description>`: the **parameter description**, a user-friendly text string describing the parameter and giving an example value in the LOCKSS Web user interface.
*   `<size>`: the parameter display size in characters in the LOCKSS Web user interface.

## Parameter Types

The following plugin configuration parameter types are defined in the LOCKSS software.

### Character Strings

#### String

*   Type code: `1`

A non-empty string.

#### URL

*   Type code: `3`

Used most frequently as a URL prefix. This must be a valid URL string according to [Java's `java.net.URL` constructor](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html#URL(java.lang.String)).

#### User Credentials

*   Type code: `10`

A colon-separated username and password.

### Numeric

#### Integer

*   Type code: `2`

The integer can be negative. Represented internally as a 32-bit integer.

#### Non-Negative Integer

*   Type code: `6`

The integer can be zero but cannot be negative. Represented internally as a 32-bit integer.

#### Long Integer

*   Type code: `11`

The value can be negative. Represented internally as a 64-bit integer.

### Time

#### Year

*   Type code: `4`

A four-digit year, or the special value `0` to denote an unspecified year.

#### Time Interval

*   Type code: `12`

Specified as a long integer followed by a suffix indicating a time unit: `ms` for milliseconds, `s` for seconds, `m` for minutes, `h` for hours, `d` for days, `w` for weeks (7 days), `y` for years (365 days). If there is no suffix, the default interpretation is milliseconds. The time unit suffixes are case-insensitive. <!-- TODO: pointer to Javadoc -->

### Ranges

#### String Range

*   Type code: `7`

The range is specified with two strings separated by a dash (`-`) and is inclusive. If there is a single string with no dash, the range is interpreted to contain only that string.

#### Numeric Range

*   Type code: `8`

The range is specified with two integers separated by a dash (`-`). If there is a single integer, the range is interpreted to contain only that integer.

### Other

#### Set

*   Type code: `9`

Specified as a comma-separated list of strings, with empty strings between commas discarded, and whitespace between the commas and the beginnings and ends of strings trimmed. <!-- TODO: set macros -->

#### Boolean

*   Type code: `5`

The canonical values are `true` or `false`, although `yes`, `on` and `1` are recognized as `true` and `no`, `off` and `0` are recognized as `false`. All these value strings are case-insensitive.

## Built-In Plugin Configuration Parameters

The LOCKSS software defines a number of built-in plugin configuration parameters.

### Commonly Used

#### Base URL

*   Key: `base_url`
*   Type: URL (`3`)

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>base_url</key>
        <type>3</type>
        <displayName>Base URL</displayName>
        <description>Usually of the form http://&lt;journal-name&gt;.com/</description>
        <size>40</size>
        <definitional>true</definitional>
        <defaultOnly>false</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

#### Second Base URL

*   Key: `base_url2`
*   Type: URL (`3`)

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>base_url2</key>
        <type>3</type>
        <displayName>Second Base URL</displayName>
        <description>Use if AU spans two hosts</description>
        <size>40</size>
        <definitional>true</definitional>
        <defaultOnly>false</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

#### Year

*   Key: `year`
*   Type: year (`4`)

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>year</key>
        <type>4</type>
        <displayName>Year</displayName>
        <description>Four digit year (e.g., 2004)</description>
        <size>4</size>
        <definitional>true</definitional>
        <defaultOnly>false</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

### Useful for Serials

#### Volume Number

*   Key: `volume`
*   Type: non-negative integer (`6`)

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>volume</key>
        <type>6</type>
        <displayName>Volume No.</displayName>
        <description>Numeric volume number, e.g. 7</description>
        <size>8</size>
        <definitional>true</definitional>
        <defaultOnly>false</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

#### Volume Name

*  Key: `volume_name`
*  Type: string (`1`)

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>volume_name</key>
        <type>1</type>
        <displayName>Volume Name</displayName>
        <description>Volume name, e.g. 23A</description>
        <size>20</size>
        <definitional>true</definitional>
        <defaultOnly>false</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

#### Issue Range

*   Key: `issue_range`
*   Type: string range (`7`)

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>issue_range</key>
        <type>7</type>
        <displayName>Issue Range</displayName>
        <description>A Range of issues in the form: aaa-zzz</description>
        <size>20</size>
        <definitional>true</definitional>
        <defaultOnly>false</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

#### Numeric Issue Range

*   Key: `num_issue_range`
*   Type: numeric range (`7`)

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>issue_range</key>
        <type>7</type>
        <displayName>Issue Range</displayName>
        <description>A Range of issues in the form: aaa-zzz</description>
        <size>20</size>
        <definitional>true</definitional>
        <defaultOnly>false</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

#### Issue Set

*   Key: `issue_set`
*   Type: set (`9`)

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>issue_set</key>
        <type>9</type>
        <displayName>Issue Set</displayName>
        <description>A comma delimited list of issues. (eg issue1, issue2)</description>
        <size>20</size>
        <definitional>true</definitional>
        <defaultOnly>false</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

#### Journal Directory

*   Key: `journal_dir`
*   Type: string (`1`)

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>journal_dir</key>
        <type>1</type>
        <displayName>Journal Directory</displayName>
        <description>Directory name for journal content (i.e. 'american_imago').</description>
        <size>40</size>
        <definitional>true</definitional>
        <defaultOnly>false</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

#### Journal Abbreviation

*   Key: `journal_abbr`
*   Type: string (`1`)

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>journal_abbr</key>
        <type>1</type>
        <displayName>Journal Abbreviation</displayName>
        <description>Abbreviation for journal (often used as part of file names).</description>
        <size>10</size>
        <definitional>true</definitional>
        <defaultOnly>false</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

#### Journal Identifier

*   Key: `journal_id`
*   Type: string (`1`)

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>journal_id</key>
        <type>1</type>
        <displayName>Journal Identifier</displayName>
        <description>Identifier for journal (often used as part of file names).</description>
        <size>40</size>
        <definitional>true</definitional>
        <defaultOnly>false</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

#### Journal ISSN

*   Key: `journal_issn`
*   Type: string (`1`)

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>journal_issn</key>
        <type>1</type>
        <displayName>Journal ISSN</displayName>
        <description>International Standard Serial Number.</description>
        <size>20</size>
        <definitional>true</definitional>
        <defaultOnly>false</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

#### Publisher Name

*   Key: `publisher_name`
*   Type: string (`1`)

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>publisher_name</key>
        <type>1</type>
        <displayName>Publisher Name</displayName>
        <description>Publisher Name for Archival Unit</description>
        <size>40</size>
        <definitional>true</definitional>
        <defaultOnly>false</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

### Useful for OAI-PMH

#### OAI Request URL

*   Key: `oai_request_url`
*   Type: URL (`3`)

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>oai_request_url</key>
        <type>3</type>
        <displayName>OAI Request URL</displayName>
        <description>Usually of the form http://&lt;journal-name&gt;.com/</description>
        <size>40</size>
        <definitional>true</definitional>
        <defaultOnly>false</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

#### OAI Spec

*   Key: `oai_spec`
*   Type: string (`1`)

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>oai_spec</key>
        <type>1</type>
        <displayName>OAI Spec</displayName>
        <description>Spec for journal in the OAI crawl</description>
        <size>40</size>
        <definitional>true</definitional>
        <defaultOnly>false</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```
