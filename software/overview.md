---
layout: page
title: LOCKSS Software Overview
---

*This page is under construction.*

The LOCKSS system consists of these components:

*   Core components
    *   [LOCKSS Repository Service](https://github.com/lockss/laaws-repository-service): responsible for object storage
    *   [LOCKSS Configuration Service](https://github.com/lockss/laaws-configservice): responsible for centralizing configuration and state data for the other components of the system
    *   [LOCKSS Poller Service](https://github.com/lockss/laaws-poller): responsible for operating the peer-to-peer LOCKSS audit-and-repair protocol
*   Metadata components
    *   [LOCKSS Metadata Extraction Service](https://github.com/lockss/laaws-metadataextractor): responsible for scheduling the extraction of metadata from preserved content
    *   [LOCKSS Metadata Service](https:/github.com/lockss/laaws-metadataservice): responsible for answering metadata queries, including DOI and OpenURL queries

The LOCKSS system can interoperate with these components:

*   Web replay engines
    *   [Pywb](https://github.com/webrecorder/pywb): the state-of-the-art Web replay engine from [Webrecorder.io](https://webrecorder.io/)
    *   [OpenWayback](https://github.com/iipc/openwayback): the Web replay engine developed by the [IIPC](http://netpreserve.org/) community
*   Web archive search front-ends *(planned)*
    *   [Shine](https://github.com/ukwa/shine) *(planned)*
    *   [SolrWayback](https://github.com/netarchivesuite/solrwayback) *(planned)*
    *   [Warclight](https://github.com/archivesunleashed/warclight) *(planned)*
