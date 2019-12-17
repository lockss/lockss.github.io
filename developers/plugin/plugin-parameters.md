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

Defining the necessary configuration parameters for a given plugin comes mostly from studying the URL structure of the preservation target, finding patterns, and identifying the parts of those patterns that differ between Archival Units.

Each plugin configuration parameter is represented by a `<org.lockss.daemon.ConfigParamDescr>` stanza that looks like this.  Only `<key>` and `<type>` are required.

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>...</key>
        <type>...</type>
        <displayName>...</displayName>
        <description>...</description>
        <size>...</size>
        <definitional>...</definitional>    <!-- default: true -->
        <defaultOnly>...</defaultOnly>      <!-- default: false -->
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

Specified as a comma-separated list of strings, with whitespace surrounding strings trimmed, and empty strings discarded. The string `{`*n*`,`*m*`}`, where *n* and *m* are integers, will be replaced by all the integers between *n* and *m*, inclusive.  *Eg*, the set `{2002-2005}, 2003Supp, 2004Supp` is equivalent to `2002, 2003, 2003Supp, 2004, 2004Supp, 2005`.

#### Boolean

*   Type code: `5`

The canonical values are `true` or `false`, although `yes`, `on` and `1` are recognized as `true` and `no`, `off` and `0` are recognized as `false`. All these value strings are case-insensitive.

## Built-In Definitional Parameters

The LOCKSS software defines a number of built-in definitional plugin configuration parameters.

Definitional parameters give an AU its identity -- change the value for a definitional parameter and you will be describing a different slice of content (different year, different directory, etc.).

### Commonly Used

#### Base URL

*   Parameter key: `base_url`
*   Parameter type: URL (`3`)

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

*   Parameter key: `base_url2`
*   Parameter type: URL (`3`)

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

*   Parameter key: `year`
*   Parameter type: year (`4`)

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

*   Parameter key: `volume`
*   Parameter type: non-negative integer (`6`)

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

*   Parameter key: `issue_range`
*   Parameter type: string range (`7`)

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

*   Parameter key: `num_issue_range`
*   Parameter type: numeric range (`7`)

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

*   Parameter key: `issue_set`
*   Parameter type: set (`9`)

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

*   Parameter key: `journal_dir`
*   Parameter type: string (`1`)

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

*   Parameter key: `journal_abbr`
*   Parameter type: string (`1`)

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

*   Parameter key: `journal_id`
*   Parameter type: string (`1`)

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

*   Parameter key: `journal_issn`
*   Parameter type: string (`1`)

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

*   Parameter key: `publisher_name`
*   Parameter type: string (`1`)

**Deprecated.** Use of this parameter is not recommended. It is unlikely the publisher name will appear in URLs, as opposed to a publisher abbreviation or code.

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

*   Parameter key: `oai_request_url`
*   Parameter type: URL (`3`)

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

*   Parameter key: `oai_spec`
*   Parameter type: string (`1`)

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

### Built-In Non-Definitional Parameters

The LOCKSS software also defines a number of non-definitional plugin configuration parameters.

Non-definitional parameters are necessary as placeholders in plugin rules and code, but they do not contribute to the AU's identity -- you may need to change the value of a non-definitional parameter but it will not change which slice of content the AU corresponds to.

Some non-definitional parameters might be listed in the plugin itself, like the `user_pass` parameter for user credentials, if all AUs are expected to supply a value for the parameter, but most others are involved in the lifecycle of any AU and need not be listed in the plugin, like the `pub_down` parameter for AUs that are not currently allowed to crawl.

#### Username and Password

*   Parameter key: `user_pass`
*   Parameter type: user credentials (`10`)
*   Definitional: false

Some harvesting processes may require user credentials (username and password). A non-definitional parameter is needed because the username and password might be different for different harvesting nodes, or may change over time, without changing the identity of the AU (for instance its year).

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>user_pass</key>
        <type>10</type>
        <displayName>Username:Password</displayName>
        <description>Colon-separated username and password string, e.g. myuser:mypass</description>
        <size>30</size>
        <definitional>false</definitional>
        <defaultOnly>false</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

#### AU Down

*   Parameter key: `pub_down`
*   Parameter type: boolean (`5`)
*   Definitional: false
*   Default-only: true

This non-definitional parameter is used routinely in the title database files of LOCKSS networks, but does not need to appear explicitly in plugins.

When this parameter value is supplied as `true` for an AU, the AU is considered to be "down", meaning that it is currently unavailable from its source and should not attempt to crawl or recrawl.

The name `pub_down`, for "publisher down", reflects the idea that the entire publisher site (content provider) might be unavailable, but this parameter is used routinely to mark individual AUs as being down outside the context of an entire content provider being unavailable.

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>pub_down</key>
        <type>5</type>
        <displayName>Pub Down</displayName>
        <description>If true, AU is no longer available from the publisher</description>
        <size>4</size>
        <definitional>false</definitional>
        <defaultOnly>true</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

#### AU Off-Limits

*   Parameter key: `pub_never`
*   Parameter type: boolean (`5`)
*   Definitional: false
*   Default-only: true

This non-definitional parameter is used routinely in the title database files of LOCKSS networks, but does not need to appear explicitly in plugins.

When this parameter value is supplied as `true` for an AU, the AU is considered to be "off-limits", meaning that the LOCKSS software will not satisfy a proxy request for a URL it determines to be in this AU from the original Web site.

<!-- TODO but does this also have the effect of pub_down in terms of crawls? -->

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>pub_never</key>
        <type>5</type>
        <displayName>Pub Never</displayName>
        <description>If true, don't try to access any content from publisher</description>
        <size>4</size>
        <definitional>false</definitional>
        <defaultOnly>true</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

#### AU Closed

*   Parameter key: `au_closed`
*   Parameter type: boolean (`5`)
*   Definitional: false
*   Default-only: true

This non-definitional parameter is used routinely in the title database files of LOCKSS networks, but does not need to appear explicitly in plugins.

When this parameter value is supplied as `true` for an AU, the AU is marked as "closed", meaning it is considered that no more content will be added to it in the future.

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>au_closed</key>
        <type>5</type>
        <displayName>AU Closed</displayName>
        <description>If true, AU is complete, no more content will be added</description>
        <size>4</size>
        <definitional>false</definitional>
        <defaultOnly>true</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

<!-- TODO does this have a  concrete effect? -->

#### Crawl Proxy

*   Parameter key: `crawl_proxy`
*   Parameter type: string (`1`)
*   Definitional: false
*   Default-only: true

This non-definitional parameter is used routinely in the title database files of LOCKSS networks, but does not need to appear explicitly in plugins.

When this parameter value is supplied as a host:port pair (for example `proxy.myuniversity.edu:8080`) for an AU, crawls of the AU will be proxied through the given proxy. When this parameter value is supplied as the special value `DIRECT` for an AU, crawls of the AU will not be proxied, even if the LOCKSS node is configured to routinely use a crawl proxy.

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>crawl_proxy</key>
        <type>1</type>
        <displayName>Crawl Proxy</displayName>
        <description>If set to host:port, crawls of this AU will be proxied. If set to DIRECT, crawls will not be proxied, even if the LOCKSS node has been configured with a default crawl proxy.</description>
        <size>40</size>
        <definitional>false</definitional>
        <defaultOnly>true</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

#### New Content Crawl Interval

*   Parameter key: `nc_interval`
*   Parameter type: time interval (`12`)
*   Definitional: false
*   Default-only: true

This non-definitional parameter is used routinely in the title database files of LOCKSS networks, but does not need to appear explicitly in plugins.

When this parameter value is supplied as a time interval for an AU, crawls of the AU will be attempted with the given requested interval rather than the LOCKSS node's default new content crawl interval.

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>nc_interval</key>
        <type>12</type>
        <displayName>Crawl Interval</displayName>
        <description>The interval at which the AU should crawl the publisher site.</description>
        <size>10</size>
        <definitional>false</definitional>
        <defaultOnly>true</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```

#### Crawl Test Substance Threshold

*   Parameter key: `crawl_test_substance_threshold`
*   Parameter type: string (`1`)
*   Definitional: false
*   Default-only: true

This non-definitional parameter is used in special circumstances, for networks set up to perform abbreviated test crawls.

```xml
      <org.lockss.daemon.ConfigParamDescr>
        <key>crawl_test_substance_threshold</key>
        <type>1</type>
        <displayName>Crawl Test Substance Threshold</displayName>
        <description>Minimum number of substance URLs necessary for successful abbreviated crawl test.</description>
        <size>20</size>
        <definitional>false</definitional>
        <defaultOnly>true</defaultOnly>
      </org.lockss.daemon.ConfigParamDescr>
```
