---
layout: page
title: Starter Network Configuration File
---

You can use the following file as a starter network configuration file. Using the placeholders from the [checklist](props-server#cecklist), this file is located at `${NETROOT}/lockss.xml`.

Please note that the `org.lockss.plugin.registries` (search for `plugin.registries`) configuration value needs to be replaced with the correct URL for your network's plugin registry; the example below contains placeholders from the [checklist](props-server#cecklist), which would correspond to `http://props.mybiglockssnet.org:8001/mybiglockssnet/plugins/`.

Please also note the `org.lockss.id.initialV3PeerList` (search for `id.initialV3PeerList`) configuration value, which is a list of **participant identifiers** of the LOCKSS preservation nodes in the network. A participant identifier contains the publicly routable IP address of the preservation node, and the polling and repair port of the preservation node (usually 9729, configured by each node). An example participant identifier is `TCP:[10.1.2.3]:9729`.
```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE lockss-config [
    <!ELEMENT lockss-config (if|property)+>
    <!ELEMENT property (property|list|value|if)*>
    <!ELEMENT list (value)+>
    <!ELEMENT value (#PCDATA)>
    <!ELEMENT test EMPTY>
    <!ELEMENT and (and|or|not|test)*>
    <!ELEMENT or (and|or|not|test)*>
    <!ELEMENT not (and|or|not|test)*>
    <!ELEMENT if (and|or|not|then|else|test|property)*>
    <!ELEMENT then (if|property)*>
    <!ELEMENT else (if|property)*>
    <!ATTLIST property name CDATA #REQUIRED>
    <!ATTLIST property value CDATA #IMPLIED>
    <!ATTLIST test hostname CDATA #IMPLIED>
    <!ATTLIST test group CDATA #IMPLIED>
    <!ATTLIST test serviceName CDATA #IMPLIED>
    <!ATTLIST test serviceAbbrev CDATA #IMPLIED>
    <!ATTLIST test daemonVersionMin CDATA #IMPLIED>
    <!ATTLIST test daemonVersionMax CDATA #IMPLIED>
    <!ATTLIST test daemonVersion CDATA #IMPLIED>
    <!ATTLIST test platformVersionMin CDATA #IMPLIED>
    <!ATTLIST test platformVersionMax CDATA #IMPLIED>
    <!ATTLIST test platformVersion CDATA #IMPLIED>
    <!ATTLIST test platformName CDATA #IMPLIED>
    <!ATTLIST if hostname CDATA #IMPLIED>
    <!ATTLIST if group CDATA #IMPLIED>
    <!ATTLIST if serviceName CDATA #IMPLIED>
    <!ATTLIST if serviceAbbrev CDATA #IMPLIED>
    <!ATTLIST if daemonVersionMin CDATA #IMPLIED>
    <!ATTLIST if daemonVersionMax CDATA #IMPLIED>
    <!ATTLIST if daemonVersion CDATA #IMPLIED>
    <!ATTLIST if platformVersionMin CDATA #IMPLIED>
    <!ATTLIST if platformVersionMax CDATA #IMPLIED>
    <!ATTLIST if platformVersion CDATA #IMPLIED>
    <!ATTLIST if platformName CDATA #IMPLIED>
    <!ATTLIST list append CDATA #IMPLIED>
    ]>
    
    <lockss-config>
    
      <property name="org.lockss">
    
        <!-- PLN Configuration -->
    
        <property name="titleDbs">
          <list>
            <value>titledb/titledb.xml</value>
          </list>
        </property>
    
        <property name="plugin.registries">
          <list>
            <value>http://${PROPSHOST}:${PROPSPORT}/${NETCODE}/plugins/</value>
          </list>
        </property>
    
        <property name="id.initialV3PeerList">
          <list>
            <!-- a list of participant identifiers in your LOCKSS network; example: -->
            <!-- lockss.auniversity.edu (A University) -->
            <value>TCP:[10.1.2.3]:9729</value>
            <!-- lockss1.buniversity.edu (B University) -->
            <value>TCP:[1.2.3.4]:9729</value>
            <!-- mylockssnet.cuniversity.edu (C University) -->
            <value>TCP:[192.168.2.3]:9729</value>
            <!-- lockss.duniversity.edu (D University) -->
            <value>TCP:[192.168.100.101]:9729</value>
          </list>
        </property>

        <!-- Typically desired: -->

        <!-- Allow export feature -->
        <property name="export.enabled" value="true" />
    
        <!-- No simultaneous crawls of AUs belonging to same plugin -->
        <property name="baseau.defaultFetchRateLimiterSource" value="plugin" />
    
        <!-- Enables display of (a single) referrer info in crawl status -->
        <property name="crawlStatus.recordReferrers" value="First" />
    
        <!-- Max number of simultaneous crawls.  Default 15 -->
        <property name="crawler.threadPool.max" value="3" />
    
       <property name="log">
          <property name="default.level" value="debug" />
          <property name="Scheduler.level" value="info" />
          <property name="CrawlerImpl.level" value="info" />
          <property name="BaseCrawler.level" value="info" />
        </property>
    

        <!-- Helps with debugging -->
        <property name="thread.hungThreadDump" value="true" />
    
        <property name="poll.v3">
          <property name="quorum" value="4" />
    
          <property name="deleteExtraFiles" value="false" />
    
          <!-- Required for a closed network (all peers listed in
               initialV3PeerList -->
          <property name="enableDiscovery" value="false" />
          <property name="minNominationSize" value="0" />
          <property name="maxNominationSize" value="0" />
    
          <property name="repairFromCachePercent" value="25" />
    
          <property name="enableSymmetricPolls" value="true" />
          <property name="allSymmetricPolls" value="true" />
    
        </property>
    
        <property name="jms.connect.failover" value="true" />
    
        <!-- These are now the default in the code, sot hese lines won't be necessary soon -->
        <property name="poll.expireRecent" value="2d" />
        <property name="crawler.maxRepairRate" value="1000/1d" />
        <property name="HtmlTagFilter.throwIfNoEndTag" value="false" />
    
      </property>
    
    </lockss-config>
```
The network configuration file can be used to configure numerous aspects of the network or even of individual nodes. This LOCKSS Network Admin Guide is under construction and will be expanded to document many of these tuning parameters.
