---
layout: page
title: LOCKSS Plugin Developer Manual
---

*This page is under construction.*

**Welcome to the LOCKSS Plugin Developer Manual.**

## Table of Contents

1.  Introduction
    1.  [Plugin Concepts](plugin-concepts)
    1.  [Plugin Format](plugin-format)
1.  Identifying Elements
    1.  [Plugin Identifier](plugin-identifier)
    1.  [Plugin Name](plugin-name)
    1.  [Plugin Version](plugin-version)
    1.  [Plugin Configuration Parameters](plugin-parameters)
    1.  [AU Name](au-name)
    1.  [Required Daemon Version](required-daemon-version)
1.  Crawl Control
    1.  [Start URLs](start-urls)
    1.  [Crawl Seed](crawl-seed)
    1.  [Permission URLs](permission-urls)
    1.  [Per-Host Permission Path](per-host-permission-path)
    1.  [Permitted Host Pattern](permitted-host-pattern)
    1.  [Crawl Rules](crawl-rules)
    1.  [Crawl Window](crawl-window)
    1.  [Recrawl Interval](recrawl-interval)
    1.  [Fetch Pause Time](fetch-pause-time)
    1.  [Crawl Rate Limiter](crawl-rate-limiter)
    1.  [Crawl Pool](crawl-pool)
    1.  [Response Handler](response-handler)
    1.  [URL Normalizer](url-normalizer)
    1.  [Link Extractor](link-extractor)
    1.  [Content Filter](content-filter)
    1.  [URL Fetcher](url-fetcher)
    1.  [URL Consumer](url-consumer)
1.  Crawl Validation
    1.  [Redirect to Login URL Pattern](redirect-to-login-url-pattern)
    1.  [Login Page Checker](login-page-checker)
    1.  [Content Validator](content-validator)
    1.  [Substance Patterns](substance-patterns)
    1.  [Substance Predicate](substance-predicate)
1.  Poll Control
    1.  [Exclude URLs](exclude-urls)
    1.  [Poll Result Weight](poll-result-weight)
    1.  [Repair From Publisher When Too Close](repair-from-publisher-when-too-close)
    1.  [Repair From Peer If Missing](repair-from-peer-if-missing)
1.  Hash Filters
    1.  [Introduction](hash-filters)
    1.  [HTML Filters](html-filters)
    1.  [PDF Filters](pdf-filters)
1.  Metadata Extraction
    1.  [Article Iterator](article-iterator)
    1.  [Article Metadata Extractor](article-metadata-extractor)
    1.  [File Metadata Extractor](file-metadata-extractor)
1.  Web Replay
    1.  [Link Rewriter](link-rewriter)
    1.  [Rewrite HTML Meta Tags](rewrite-html-meta-tags)
1.  Plugin Inheritance
    1.  [Parent Plugin](parent-plugin)
    1.  [Parent Plugin Version](parent-plugin-version)
 <!-- TODO miscellaneous section -->
1.  Appendix: Related Concepts
    1.  [printf Format Strings](printf-format-strings)
    1.  [Regular Expressions](regular-expressions)
