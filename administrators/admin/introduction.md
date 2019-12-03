---
layout: page
title: LOCKSS Network Introduction
---

## LOCKSS Network

The **[LOCKSS](https://www.lockss.org/) system** is a general-purpose distributed digital preservation solution, meaning software designed for the long-term preservation of data in a peer-to-peer fashion. The LOCKSS software is developed by the LOCKSS Program under the auspices of Stanford University Libraries. For more information about the LOCKSS Program, visit <http://www.lockss.org/>.

A **LOCKSS preservation network**, or **LOCKSS network** for short, is a group of nodes running the LOCKSS system, working together to preserve content using the LOCKSS audit and repair protocol.

## Closed and Open-Ended

Most typically, a LOCKSS network is a **closed LOCKSS network**, meaning the nodes in the network all know each other and only work among themselves; this model was historically referred to as a **private LOCKSS network** (or **PLN**) or **community LOCKSS network** (or **CLN**).

When a LOCKSS network has open-ended participation, it is referred to as an **open-ended LOCKSS network**.

The only meaningful difference between LOCKSS networks that are closed or open-ended is one of intent and governance. Most preservation initiatives are among a group of related institutions with common preservation goals, that do not need nor want to provide a way for arbitrary external participants to "plug into" their LOCKSS network, and as a result most LOCKSS networks are de facto private.

Even though concepts in the LOCKSS system apply the same to closed or open-ended LOCKSS networks, the dominance of closed LOCKSS networks causes the literature to refer to LOCKSS networks often as private LOCKSS networks or PLNs, even when that aspect is not directly relevant.

## Components

A LOCKSS network consists of the following components:

*   A **LOCKSS network configuration file**. The LOCKSS network configuration file is read from a Web server by the nodes in a LOCKSS network, and contains configuration information about the network.

    This file is most often standalone, but can point to additional network configuration files if desired. It also points to one or more LOCKSS plugin registries and one or more title database files (see below).

*   One or more **LOCKSS plugin registries**. A LOCKSS plugin registry is a collection of LOCKSS plugins, which are signed JAR files that provide the LOCKSS system with specialized software to process and preserve specific preservation targets.

    Most LOCKSS networks only require a single plugin registry, but some applications might have LOCKSS plugins served from different origins, or split into participant tiers, or other scenarios that could call for several registries.

*   One or more **LOCKSS title database files**. A LOCKSS title database file describes lists of archival units (AUs) that can be preserved in the network, including information linking AUs to plugins and parameters needed by the plugins, and essential identifying or bibliographic data.

    The name *title database* is historic and implies an interactive database of some kind, but it is only a descriptive file -- there is no database system at this level.

*   A number of **LOCKSS preservation nodes** running the LOCKSS software, configured to use the network configuration file.

    See the [LOCKSS 2.0 System Manual](../manual) or the [Classic LOCKSS Manual](../classic-lockss) for installation and administration guides.

## Props Server

The network configuration file, plugin files and title database files are merely files on Web servers. The Web server that serves a network's configuration file is the configuration server; that which serves a plugin registry, a plugin registry server; and that which serves title database files,
a title database file server.

In most cases, all these Web servers are one and the same, referred to as a **LOCKSS props server**.
