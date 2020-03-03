---
layout: page
title: File Metadata Extractor
---

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `<mediatype>_metadata_extractor_factory_map` (for example `text/html_metadata_extractor_factory_map`)

## Value Type

Value type: map (`<map>`) from string (`<string>`) keys to string values

The keys are (*FIXME*)

The values are the fully-qualified name of a Java class implementing the `org.lockss.extractor.FileMetadataExtractorFactory` interface.

## Example

Plugin XML file:

```xml
  <entry>
    <string>text/html_metadata_extractor_factory_map</string>
    <map>
      <entry>
        <string>*</string>
        <string>edu.example.plugin.publisherx.PublisherXHtmlMetadataExtractorFactory</string>
      </entry>
    </map>
  </entry>
```

Corresponding Java class:

```java
package edu.example.plugin.publisherx;

import org.lockss.extractor.FileMetadataExtractorFactory;

public class PublisherXHtmlMetadataExtractorFactory
    implements FileMetadataExtractorFactory {
  // ...
}
```

If the media type is represented under multiple guises in the plugin's AUs, for example XML represented as both `text/xml` and `application/xml`, you will need multiple entries in the plugin.

## Description

File metadata extractors are part of the [metadata extraction](metadata-extraction) pipeline. Their function is to parse the contents of a particular URL based on its media type and file format, and emit any number of `ArticleMetadata` metadata records, and they are invoked as part of the execution of an [article metadata extractor](article-metadata-extractor).

The **`org.lockss.extractor.FileMetadataExtractorFactory`**, **`org.lockss.extractor.FileMetadataExtractor`** and **`org.lockss.extractor.FileMetadataExtractor.Emitter`** interfaces are as follows:

```java
public interface FileMetadataExtractorFactory {

  public FileMetadataExtractor createFileMetadataExtractor(MetadataTarget target,
                                                           String contentType)
      throws PluginException;

}

public interface FileMetadataExtractor {

  public interface Emitter {

    public void emitMetadata(CachedUrl cu,
                             ArticleMetadata metadata);

  }

  public void extract(MetadataTarget target,
                      CachedUrl cu,
                      Emitter emitter)
    throws IOException, PluginException;

}
```

### SimpleFileMetadataExtractor

The **`org.lockss.extractor.SimpleFileMetadataExtractor`** utility class is used as a base class for the common case where a file metadata extractor produces a single metadata record (or `null`), rather than an arbitrary number of metadata records. It defines one abstract method:

```java
  public abstract ArticleMetadata extract(MetadataTarget target,
                                          CachedUrl cu)
      throws IOException, PluginException;
```

and its `extract(MetadataTarget target, CachedUrl cu, Emitter emitter)` simply calls `extract(MetadataTarget target, CachedUrl cu)` and emits the returned `ArticleMetadata` if it is not `null`.

Utility classes based on `SimpleFileMetadataExtractor` include `JsoupTagExtractor`, `RisMetadataExtractor`.

### JsoupTagExtractor

The **`org.lockss.extractor.JsoupTagExtractor`** utility class can be used to build HTML or XML file metadata extractors that use the [jsoup](https://jsoup.org/) parser.

By default, it maps the value of the `name` attribute of **HTML `<meta>` tags** to the value of their `content` attribute in the `ArticleMetadata` object's raw multi-map.

However if the media type is `text/xml`, `application/xml` or `application/xhtml+xml`, or if the extractor is created with **selector strings**, for each selector string, and for each element matched by the selector string, it maps the selector string to the selector value in the raw multi-map. The selector strings are those understood by the `select(...)` method of jsoup's `Document` class.

Subclasses provide the recipe multi-map (cook map) to process raw data into metadata.

*The `org.lockss.extractor.JsoupXmlTagExtractor` class exists but its functionality has been absorbed into `org.lockss.extractor.JsoupTagExtractor`, which is capable of handling HTML without selector strings as well as HTML and XML with selector strings. It may be removed in a future version of the LOCKSS system and should not be used for new plugin implementations -- use `JsoupTagExtractor` instead.*

*The `org.lockss.extractor.SimpleHtmlMetaTagMetadataExtractor` class also exists and scrapes HTML `<meta>` tags using a regular expression-based approach. It is at risk of being deprecated in a future version of the LOCKSS system, and is not recommended for new plugin implementations -- use `JsoupTagExtractor` instead.*

### RisMetadataExtractor

The **`org.lockss.extractor.RisMetadataExtractor`** utility class parses **RIS metadata files** (media type `application/x-research-info-systems`).

By default, it maps RIS tags to their values in the `ArticleMetadata` object's raw multi-map, and its recipe map (cook map) maps the following raw keys (RIS tags) to the following `MetadataField` instances:

*   `T1` to the article title (`MetadataField.FIELD_ARTICLE_TITLE`)
*   `AU` to an author (`MetadataField.FIELD_AUTHOR`)
*   `JF` tp the journal title (`MetadataField.FIELD_PUBLICATION_TITLE`)
*   `DO` to the DOI (`MetadataField.FIELD_DOI`)
*   `PB` to the publisher name (`MetadataField.FIELD_PUBLISHER`)
*   `VL` to the journal volume (`MetadataField.FIELD_VOLUME`)
*   `IS` to the journal issue (`MetadataField.FIELD_ISSUE`)
*   `SP` to the start page (`MetadataField.FIELD_START_PAGE`)
*   `EP` to the end page (`MetadataField.FIELD_END_PAGE`)
*   `DA` to the publication date (`MetadataField.FIELD_DATE`)
*   `SN` to the ISSN (`MetadataField.FIELD_ISSN`) for a journal (`TY` tag equal to `JOUR`) or ISBN (`MetadataField.FIELD_ISBN`) for a book (`TY` tag equal to `BOOK`, `CHAP`, `EBOOK`, `ECHAP`, `EDBOOK`)

but the behavior is customizable.

### SourceXmlMetadataExtractor

Because the LOCKSS Program processes large amounts of bulk content on behalf of the CLOCKSS Archive, which is often in the form of bundles of content with multi-article metadata in XML (for example JATS format), there are utility classes in the `org.lockss.plugin.clockss` package of the *plugins* tree of the [`lockss-daemon`](https://github.com/lockss/lockss-daemon) project to generalize this kind of data processing.

Plugins can only reference classes found in the plugin JAR itself, in [`lockss-core`](https://github.com/lockss/lockss-core) and in its dependencies (if using the re-architected LOCKSS system), or in the *main* tree of `lockss-daemon` and in its dependencies (if using the classic LOCKSS system), so these classes in the *plugins* tree of `lockss-daemon` are not directly accessible to arbitrary plugins (without some manipulation, like injecting additional classes in plugin JARs). However there is growing interest in re-using these utility classes in the broader LOCKSS community, so some of these classes will be "promoted" to `lockss-core` so they can be used by third-party plugins in a future version of the LOCKSS system.

The `org.lockss.plugin.clockss.SourceXmlMetadataExtractorFactory`, `org.lockss.plugin.clockss.SourceXmlMetadataExtractorFactory.SourceXmlMetadataExtractor` and `org.lockss.plugin.clockss.SourceXmlSchemaHelper` classes define a framework for processing XML metadata in some format, and mapping from XPath expressions to text values in the `ArticleMetadata` object's raw multi-map. The format-specific logic is confined in the `SourceXmlSchemaHelper` object.

The `SourceXmlSchemaHelper` class consists of a *global map* and an *article map*. Both map XPath strings to the corresponding values. The article map, aided by the `getArticleNode()` method which gives an XPath for the top-level node of each article in the XML file, is used to designate XPaths for each emitted article from the file. The optional global map is used to designate XPaths that apply to all emitted articles from the file, and can be used for XML formats that hoist some data above the level of each article (for instance publication-level or issue-level data).

This framework also offers some features to perform deduplication or recombination, verify some URLs or file paths, and `SourceXmlSchemaHelper`'s `getCookMap()` method provides the recipe multi-map to produce metadata from the raw multi-map.

*There is also an effort underway to define an equivalent framework for similarly structured metadata in JSON, using the [Jayway JsonPath](https://github.com/json-path/JsonPath) library.*
