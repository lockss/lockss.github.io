---
layout: page
title: Article Iterator
---

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `plugin_article_iterator_factory`

## Value Type

Value type: string (`<string>`)

The string is the fully-qualified name of a Java class implementing the `org.lockss.plugin.ArticleIteratorFactory` interface.

## Example

Plugin XML file:

```xml
  <entry>
    <string>plugin_article_iterator_factory</string>
    <string>edu.example.plugin.publisherx.PublisherXArticleIteratorFactory</string>
  </entry>
```

Corresponding Java class:

```java
package edu.example.plugin.publisherx;

import org.lockss.plugin.ArticleIteratorFactory;

public class PublisherXArticleIteratorFactory implements ArticleIteratorFactory {
  // ...
}
```

## Description

The article iterator is part of the [metadata extraction](metadata-extraction) pipeline. Its function is enumerate the articles (where "article" is meant as "item" or "object") in the archival unit (AU). Each article is represented by an `ArticleFiles` instance.

The **`org.lockss.plugin.ArticleIteratorFactory`** interface is as follows:

```java
public interface ArticleIteratorFactory {

  public Iterator<ArticleFiles> createArticleIterator(ArchivalUnit au,
                                                      MetadataTarget target)
      throws PluginException;

}
```

Rather than traversing the AU's URLs manually through the `ArchivalUnit` interface and implementing typical inner workings of a Java `Iterator`, many article iterators make use of utility classes available in the LOCKSS software, such as `SubTreeArticleIterator` and `SubTreeArticleIteratorBuilder`.

### ArticleFiles

An **`org.lockss.plugin.ArticleFiles`** instance groups the main URLs of an article (item) together and labels them. It is a mapping from **roles** to URLs (which are internally represented as objects implementing `org.lockss.plugin.CachedUrl`). (Technically, it is a mapping from roles to arbitrary Java objects.)

![ArticleFiles mapping](images/articlefiles-mapping.png)

Roles are arbitrary strings, but many typical role strings are defined as constants in the `ArticleFiles` class, for example:

*   Full text URLs:

    *   `ArticleFiles.ROLE_FULL_TEXT_HTML`: a URL for the full text of a work, in HTML form

    *   `ArticleFiles.ROLE_FULL_TEXT_PDF`: a URL for the full text of a work, in PDF form

    *   `ArticleFiles.ROLE_FULL_TEXT_EPUB`: a URL for the full text of a work, in EPUB form

    *   `ArticleFiles.ROLE_FULL_TEXT_XML`: a URL for the full text of a work, in XML form

*   `ArticleFiles.ROLE_ABSTRACT`: a URL for a work's abstract

*   `ArticleFiles.ROLE_REFERENCES`: a URL for a work's list of works cited

*   `ArticleFiles.ROLE_FIGURES`: a URL for a landing page of the work's figures and illustrations

*   `ArticleFiles.ROLE_TABLES`: a URL for a landing page of the work's tables

*   `ArticleFiles.ROLE_SUPPLEMENTARY_MATERIALS`: a URL for a landing page of the work's supplementary materials

*   Citation URLs:

    *   `ArticleFiles.ROLE_CITATION`: a URL for a landing page or the work's citation files

    *   `ArticleFiles.ROLE_CITATION_BIBTEX`: a URL for a BibTeX citation file for the work

    *   `ArticleFiles.ROLE_CITATION_ENDNOTE`: a URL for an EndNote citation file for the work

    *   `ArticleFiles.ROLE_CITATION_RIS`: a URL for a RIS citation file for the work

*   `ArticleFiles.ARTICLE_METADATA`: a URL from which metadata for the work can be found

In addition to the mapping from roles to URL, one URL has a special status in the `ArticleFiles` instance as the designated, "best" full text URL for the work. It is referred to as the **full text URL** or **full text CU** (for `CachedUrl`) of the article, and is set via the `setFullTextCu(...)` method. In plugins written by the LOCKSS Program, for articles with multiple full text representations, typically HTML is favored above all, then PDF, then EPUB, and lastly XML (in subjective order of richness of rendering experience in a Web browser).

### SubTreeArticleIterator

The **`org.lockss.plugin.SubTreeArticleIterator`** class implements `Iterator<ArticleFiles>` and can be returned by an article iterator factory. It traverses an AU's URLs, restricting them in various ways according to a specification. These restrictions include considering only certain subdirectory trees (hence the name), applying regular expressions, selecting a media type, or applying a custom condition.

The **`SubTreeArticleIterator.Spec`** class contains the specification:

*   The specification identifies **root URLs**, limiting which AU URLs are enumerated to those under these root URLs only. This restriction applies to the directory structure, not the URL strings -- in effect, root URLs end with a slash. Root URLs can be specified directly with `setRoot(...)` or `setRoots(...)`, or via printf templates (which expand to URLs) expressed as single Java strings, with `setRootTemplate(...)` or `setRootTemplates(...)`. The printf templates are expressed as single Java strings, which can be tricky to read, for example: `"\"%s%s/%d/\", base_url, journal_id, year"` (with the convention that the base URL value ends with a slash). If the specification specifies no root URL, all URLs in the AU are enumerated.

*   The specification can optionally have an **include pattern** or an **exclude pattern**. With an include pattern, URLs below each root URL that match the include pattern are considered (but others are ignored). With an exclude pattern, URLs below each root URL that match the exclude pattern are ignored (but others are considered). No error will happen if both are specified, but the exclude pattern will be ignored in favor of the include pattern. These patterns (regular expressions) can be specified directly with `setIncludeSubTreePattern(...)` or `setExcludeSubTreePattern(...)`, or via printf templates (which expand to regular expressions) expressed as single Java strings with `setIncludeSubTreePatternTemplate(...)` or `setExcludeSubTreePatternTemplate(...)`.

*   The specification can optionally have a **general pattern**, which is a regular expression applied to any URL still under consideration. It can be specified directly with `setPattern(...)`, or via a printf template (which expands to a regular expression) expressed as a single Java string with `setPatternTemplate(...)`.

*   The specification can have an optional media type (for example `text/html`), and only URLs under consideration that have this media type will be enumerated. *There is currently no way to specify multiple media type, which can be problematic for media types with multiple common representations, like `text/xml` vs. `application/xml`. The class could be enhanced in the future to allow multiple media types.*

The logic for which URLs are enumerated is found in the `isArticleCu(...)` method, which can be customized in a subclass.

By default, for each successful URL, this iterator makes one `ArticleFiles` instance that has its designated full text URL set, and no roles set. This behavior can be customized in `visitArticleCu(...)` and `createArticleFiles(...)` in a subclass.

### SubTreeArticleIteratorBuilder

The **`org.lockss.plugin.SubTreeArticleIteratorBuilder`** class assists in the creation of a `SubTreeArticleIterator` instance under circumstances where the URLs of various aspects of an article (e.g. its abstract URL, its full text HTML URL, its full text PDF URL, etc.) can all be derived from one another through **mutually compatible regular expressions** and replacement strings.

An example of such mutual compatibility would be a journal where articles have full text HTML URLs that look like this: `http://www.example.com/vol12/iss3/art45` and full text PDF URLs that look like this: `http://www.example.com/pdf/article_12_3_45.pdf` (assuming these URLs represent volume 12, issue 3, page 45 for example). A regular expression for the full text HTML URLs (expressed as a Java string) could be `"/vol(\\d+)/iss(\\d+)/art(\\d+)$"`, and the replacement string `"/pdf/article_$1_$2_$3.pdf"` would yield the corresponding full text PDF URL; likewise a regular expressin for the full text PDF URL could be `"/pdf/article_(\\d+)_(\\d+)_(\\d+)\\.pdf$"`, and the replacement string `"/vol$1/iss$2/art$3"` would yield the corresponding full text HTML URL.

The `SubTreeArticleIteratorBuilder` class has convenient methods to:

*   Create a `SubTreeArticleIterator.Spec` specification. See `setSpec(...)`, or use `newSpec()` to manipulate an empty `Spec` from scratch.

*   Define **major aspects** with one or more regular expressions matching the aspect's URLs, one or more replacement strings yielding the aspect's URLs from matchers for URLs of other major aspects, and one or more roles for the aspect.

*   Define **minor aspects** with one or more replacement strings yielding the aspect's URLs from matchers for URLs of major aspects, and one or more roles for the aspect.

The key differences between major and minor aspects are:

*   URLs enumerated by the `SubTreeArticleIterator` are tried against the regular expressions of the major aspects only.

*   The earliest URL for a major aspect to match for a given article is also designated as the article's full text CU.

All aspects are defined with the variants of the `addAspect(...)` method and associated methods.

When an `ArticleFiles` is complete, methods like `setRoleFromOtherRoles(...)` and `setFullTextFromRoles(...)` can be used to designate additional roles or the full text CU from the value associated with an ordered list of possibilities from other roles.

The `getSubTreeArticleIterator()` method can finally be used to obtain a `SubTreeArticleIterator` behaving in the specified manner.
