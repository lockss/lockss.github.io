---
layout: page
title: Network Ports
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

This page describes the default network ports used by the LOCKSS system.

Unless otherwise noted, all ports are **TCP**.

All ports in the 24600-24699 range should be considered reserved. The LCAP (LOCKSS polling and repair) port retains its historical value of 9729.

*   8080: Pywb or OpenWayback replay engine
*   9729: LCAP (LOCKSS polling and repair)
*   24600: *reserved* (currently LOCKSS Configuration Service UI)
*   24602: PostgreSQL
*   24603: Solr
*   24606: ActiveMQ
*   24610: LOCKSS Repository Service - REST port
*   24619: *reserved* (HDFS FS port)
*   24620: LOCKSS Configuration Service - Rest port
*   24621: LOCKSS Configuration Service - UI port
*   24630: LOCKSS Poller Service - REST port
*   24631: LOCKSS Poller Service - UI port
*   24640: LOCKSS Metadata Extraction Service - REST port
*   24641: LOCKSS Metadata Extraction Service - UI port
*   24650: LOCKSS Metadata Service - REST port
*   24651: LOCKSS Metadata Service - UI port
*   24670: LOCKSS Proxy
*   24671: *reserved*
*   24672: LOCKSS Audit Proxy
*   24673: *reserved*
*   24674: ICP server **(UDP)**
*   24680: LOCKSS Content Server (ServeContent)
*   24681: *reserved* Pywb replay engine
*   24682: *reserved* OpenWayback replay engine
