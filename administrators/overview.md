---
layout: page
title: LOCKSS Software Overview
---

*This information does not apply to the classic LOCKSS daemon (version 1.x).*

The LOCKSS system consists of these components:

*   Core components

    *   [LOCKSS Configuration Service](https://github.com/lockss/laaws-configservice): responsible for centralizing configuration and state data for the other components of the system

    *   [LOCKSS Repository Service](https://github.com/lockss/laaws-repository-service): responsible for object storage

    *   [LOCKSS Poller Service](https://github.com/lockss/laaws-poller): responsible for operating the peer-to-peer LOCKSS audit-and-repair protocol

*   Metadata components

    *   [LOCKSS Metadata Extraction Service](https://github.com/lockss/laaws-metadataextractor): responsible for scheduling the extraction of metadata from preserved content

    *   [LOCKSS Metadata Service](https:/github.com/lockss/laaws-metadataservice): responsible for answering metadata queries, including DOI and OpenURL queries

The LOCKSS system can interoperate with these components:

*   Web replay engines

    *   [Pywb](https://github.com/webrecorder/pywb): the state-of-the-art Web replay engine from [Webrecorder.io](https://webrecorder.io/)

    *   [OpenWayback](https://github.com/iipc/openwayback): the Web replay engine developed by the [IIPC](http://netpreserve.org/) community
