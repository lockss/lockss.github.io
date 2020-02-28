---
layout: page
title: LOCKSS Plugin XML Format
---

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

Conceptually, a LOCKSS plugin is a mapping from keys to values. In practice, this mapping is expressed in an XML file.

The top-level element is `<map>`, which contains any number of map entries delineated by `<entry>`.

An entry is a key-value pair.

The key is always a string (`<string>`).

The values can be strings, integers (`<int>`), long integers (`<long>`), lists (`<list>` containing its own values), and maps (`<map>` containing its own `<entry>` pairs).

```xml
<map>

  <!-- string value -->
  <entry>
    <string>key one</string>
    <string>value one</string>
  </entry>

  <!-- integer value -->
  <entry>
    <string>key two</string>
    <int>222</int>
  </entry>

  <!-- long integer value (e.g. number of milliseconds) -->
  <entry>
    <string>key three</string>
    <long>333333</long>
  </entry>

  <!-- list value (e.g. list of strings) -->
  <entry>
    <string>key four</string>
    <list>
      <string>list item one</string>
      <string>list item two</string>
      <string>list item three</string>
    </list>
  </entry>

  <!-- map value (e.g. mapping from string to string) -->
  <entry>
    <string>key five</string>
    <map>
      <entry>
        <string>subkey1</string>
        <string>subvalue1</string>
      </entry>
      <entry>
        <string>subkey2</string>
        <string>subvalue2</string>
      </entry>
      <entry>
        <string>subkey3</string>
        <string>subvalue3</string>
      </entry>
    </map>
  </entry>

</map>
```

The order of the key-value pairs does not matter but the effect of specifying the same key in more than one map entry is undefined.

## Diving Deeper

*Optional technical details for the curious.*

Technically, the file format is not XML but XML-like. Under the covers, it is really a Java map serialized with [XStream](https://x-stream.github.io/).
