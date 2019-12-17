---
layout: page
title: Regular Expressions
---

*This page is under construction.*

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Definition

A **regular expression** is a character string that specifies a **text search pattern**. The search pattern can then be applied to an input string. If a portion of the input string **matches** the search pattern, the matching portions or designated subparts of it can be extracted.

A **regular expression engine** is a software library capable of applying search patterns specified in an implementation-dependent regular expression language to arbitrary input strings.

The LOCKSS software uses the [Java regular expression engine](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html), but because Java did not always have built-in regular expression support, in some contexts the LOCKSS software uses the [Apache ORO](https://jakarta.apache.org/oro/) regular expression engine. Typical use of regular expressions in LOCKSS plugins should not result in noticeable differences between the two engines' capabilities.

*This page is under construction.*

## References

*   [Regular expression](https://en.wikipedia.org/wiki/Regular_expression) on Wikipedia
