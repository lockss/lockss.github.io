---
layout: page
title: Plugin Identifier
---

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `plugin_identifier`

## Value Type

Value type: string (`<string>`)

## Example

```xml
  <entry>
    <string>plugin_identifier</string>
    <string>edu.example.plugin.publisherx.PublisherXPlugin</string>
  </entry>
```

## Description

A unique identifier for the plugin.

The plugin identifier uniquely identifies the plugin. It is used as part of AUIDs (the unique identifier of each AU) and to name a Java package where the plugin's Java code lives. As such, the plugin identifier is really a **fully-qualified Java class name**, which consists of a Java package name and a Java class name.

Just like a file path such as `/home/jsmith/documents/myfile.txt` is a hierarchical path from more general directories (`home`) to more specific directories (`jsmith`, then `documents`) and ending with a file name (`myfile.txt`), a fully-qualified Java class name is a hierarchical path starting with the institution responsible for the plugin (conventionally by reversed Internet domain name), for example `edu.stanford.library` for library.stanford.edu), followed by more levels (typically the next one `plugin`, and then another to identify the plugin family or individual plugin), and finally ending with a "file name". The separators are periods.

**Example**

In the Global LOCKSS Network (GLN), the plugin to process volumes of journals by Oxford University Press (OUP) hosted on the Silverchair platform has the identifier `org.lockss.plugin.silverchair.oup.OupSilverchairPlugin`.

*   `org.lockss` is the reverse of lockss.org
*   `plugin` is the root level of all plugins maintained by the LOCKSS Program
*   `silverchair` is a level grouping all Silverchair-based plugins
*   `oup` is the most specific level identifying the OUP plugin
*   `OupSilverchairPlugin` is the class name.

```xml
  <entry>
    <string>plugin_identifier</string>
    <string>org.lockss.plugin.silverchair.oup.OupSilverchairPlugin</string>
  </entry>
```

*Find this plugin's source code at [https://github.com/lockss/lockss-daemon/blob/master/plugins/src/org/lockss/plugin/silverchair/oup/OupSilverchairPlugin.xml](https://github.com/lockss/lockss-daemon/blob/master/plugins/src/org/lockss/plugin/silverchair/oup/OupSilverchairPlugin.xml)*

### Note

The plugin identifier translates into a file path like so:

`org.lockss.plugin.silverchair.oup.OupSilverchairPlugin` -> `org/lockss/plugin/silverchair/oup/OupSilverchairPlugin.xml`
