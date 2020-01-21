---
layout: page
title: HTML Filters
---

*This page is under construction.*

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

HTML is the media type most frequently in need of transformation and canonicalization, as part of [hash filters](hash-filters) but also crawl filters. To this end, the LOCKSS software contains a variety of utility classes that can be used as building blocks to construct effective HTML filters.

## `HtmlFilterInputStream`

The `org.lockss.filter.html.HtmlFilterInputStream` class is a way to parse an `InputStream` of HTML content and apply a transform of type `org.lockss.filter.html.HtmlNodeFilterTransform` to it, resulting in a new `InputStream`.

The `org.lockss.filter.html.HtmlNodeFilterTransform` class provides two kinds of transforms, that either filter out all HTML nodes that match a predicate (very common use pattern), or collect only HTML nodes that match a predicate (uncommon use pattern). The code of the library used to implement `org.lockss.filter.html.HtmlFilterInputStream`  and `org.lockss.filter.html.HtmlNodeFilterTransform` refers to these predicates as `org.htmlparser.NodeFilter`.

Whether an "exclude" transform or an "include" transform, most often the predicate is really the union of many smaller predicates, which can be grouped together by the `org.htmlparser.filters.OrFilter` class (and other similar boolean operators).

Although some complex cases call for the definition of a custom predicate, most typical situations can be handled by predicates predefined in the `org.lockss.filter.html.HtmlNodeFilters` utility class:

*   `org.lockss.filter.html.HtmlNodeFilters.tag(String tag)`: predicate that matches a tag with the given name. (Many LOCKSS plugins make direct use of the underlying `org.htmlparser.filters.TagNameFilter.TagNameFilter(String)` class, but using the utility method is recommended.)
*   `org.lockss.filter.html.HtmlNodeFilters.tagWithAttribute(String tag, String attr)`: predicate that matches a tag with the given name, that defines an attribute with the specified key (regardless of the value).
*   `org.lockss.filter.html.HtmlNodeFilters.tagWithAttribute(String tag, String attr, String val)`: predicate that matches a tag with the given name, that defines an attribute with the specified key and value. The variant `org.lockss.filter.html.HtmlNodeFilters.divWithAttribute(String attr, String val)` assumes a `<div>` tag.
*   `org.lockss.filter.html.HtmlNodeFilters.tagWithAttributeRegex(String tag, String attr, String regex)`: predicate that matches a tag with the given name, that defines an attribute with the specified key, whose value matches the given regular expression. The variant `org.lockss.filter.html.HtmlNodeFilters.tagWithAttributeRegex(String tag, String attr, String regex, boolean ignoreCase)` adds a flag for whether the regular expression is case-insensitive.
*   `org.lockss.filter.html.HtmlNodeFilters.comment()`: predicate that matches any HTML comment.
*   `org.lockss.filter.html.HtmlNodeFilters.commentWithString(String str)`: predicate that matches HTML comments containing the given string. The variant `org.lockss.filter.html.HtmlNodeFilters.commentWithString(String str, boolean ignoreCase)` adds a flag for whether the test is case-insensitive.
*   `org.lockss.filter.html.HtmlNodeFilters.commentWithRegex(String regex)`: predicate that matches HTML comments matching the given regular expression. The variant `org.lockss.filter.html.HtmlNodeFilters.commentWithRegex(String regex, boolean ignoreCase)` adds a flag for whether the regular expression is case-insensitive.

## `WhiteSpaceFilter`

The `org.lockss.filter.WhiteSpaceFilter` class is a `Reader` implementation that canonicalizes whitespace by collapsing consecutive whitespace characters to a single one. This is useful because many transformations may leave different numbers of consecutive whitespace characters (perhaps zero) depending on the whitespace surrounding the outermost tags of various removed nodes.

In many LOCKSS plugins, the typical way to use `WhiteSpaceFilter` is to turn an `InputStream` into a `Reader`, apply `WhiteSpaceReader`, and turn the result back into an `InputStream` for further processing:

```java
    InputStream i1 = ...; // an input stream
    String e1 = ...; // the encoding of the input stream
    Reader r1 = FilterUtil.getReader(i1, e1);
    Reader r2 = new WhiteSpaceFilter(r1);
    InputStream i2 = new ReaderInputStream(r2);
```
