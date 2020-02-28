---
layout: page
title: Crawl Rules
---

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Key

Key: `au_crawlrules`

## Value Type

Value type: list (`<list>`) of strings (`<string>`)

The strings are a integer **crawl rule code** separated by a comma from a **`printf` format string**, accepting expressions made of plugin configuration parameter keys and a small language of functions modifying them (e.g. `url_host(...)` applied to a plugin configuration parameter of type URL, resulting in the host portion of the URL). The `printf` format string expands to a **regular expression**.

## Example

```xml
  <entry>
    <string>au_crawlrules</string>
    <list>
      <string>4, "^%s", base_url</string>
      <string>1, "^%s.*\.(css|js|gif|jpg|png)$", base_url</string>
      <string>2, "^%s%s/vol%s/iss[^/]+/art[^/]+/citedby", base_url, journal_id, volume_name</string>
      <string>1, "^%s%s/vol%s/", base_url, journal_id, volume_name</string>
      <string>1, "^%spdf/.*\.pdf$", base_url</string>
    </list>
  </entry>
```

## Description

Sequential rules determining if a URL discovered during the crawl of an AU should in turn be fetched as part of the AU or not.

Given a URL, the crawler tries each crawl rule in the order of the list until one of them results in an outcome for the URL. If none of the crawl rules result in an outcome for the URL, the default outcome is to **exclude** the URL from the AU.

### Crawl Rule Codes

The crawl rule codes are:

*   `1` ("include"): if the URL matches the regular expression, include the URL in the AU.
*   `2` ("exclude") : if the URL matches the regular expression, exclude the URL from the AU.
*   `3` ("include no match"): if the URL does not match the regular expression, include the URL in the AU.
*   `4` ("exclude no match"): if the URL does not match the regular expression,  exclude the URL from the AU.
*   `5` ("include match else exclude"): if the URL matches the regular expression, include the URL in the AU, otherwise exclude the URL from the AU.
*   `6` ("exclude match else include"): if the URL matches the regular expression exclude the URL from the AU, otherwise include the URL in the AU.
