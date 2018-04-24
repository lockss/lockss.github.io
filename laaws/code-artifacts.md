---
layout: page
permalink: /laaws/code-artifacts/
---
# Code Artifacts

The Maven code artifacts of the LOCKSS software are:

## Core

*   `org.lockss.laaws:lockss-core`
    *   Stable version: 1.1.1
    *   Development version: 1.2.0-SNAPSHOT
    *   GitHub: <https://github.com/lockss/lockss-core>

## Repository

*   `org.lockss.laaws:laaws-repository-core`
    *   Stable version: 1.11.4
    *   Development version: 1.12.0-SNAPSHOT
    *   GitHub: https://github.com/lockss/laaws-repository-core
*   `org.lockss.laaws:laaws-repository-service`
    *   Stable version: 1.7.0
    *   Development version: 1.8.0-SNAPSHOT
    *   GitHub: https://github.com/lockss/laaws-repository-service
*   `org.lockss.laaws:laaws-repository-client`
    *   Stable version: 1.5.0
    *   Development version: 1.6.0-SNAPSHOT
    *   GitHub: https://github.com/lockss/laaws-repository-client

## Metadata

*   `org.lockss.laaws:laaws-metadata-extraction-service`
    *   Stable version: 1.0.0
    *   Development version: 1.1.0-SNAPSHOT
    *   GitHub: https://github.com/lockss/laaws-metadataextractor
*   `org.lockss.laaws:laaws-metadata-service`
    *   Development version: 1.0.0-SNAPSHOT
    *   GitHub: https://github.com/lockss/laaws-metadataservice
*   `org.lockss.laaws:laaws-metadataextractor-common`
    *   Stable version: 1.2.0
    *   Development version: 1.3.0-SNAPSHOT
    *   GitHub: https://github.com/lockss/laaws-metadataextractor-common

## Infrastructural

*   `org.lockss:lockss-configuration-service`
    *   Stable version: 1.0.0
    *   Development version: 1.1.0-SNAPSHOT
    *   GitHub: https://github.com/lockss/laaws-configservice

## Ancillary

### Parent POMs

*   `org.lockss:lockss-parent-pom`
    *   Stable version: 1.8.0
    *   Development version: 1.9.0-SNAPSHOT
    *   GitHub: https://github.com/lockss/lockss-parent-pom

### POM Bundles

* `org.lockss:lockss-core-bundle`
    *   Maven dependency type: `<type>pom</type>`
    *   Stable version: 1.1.1
    *   Development version: 1.2.0-SNAPSHOT
    *   Note: Unless otherwise specified, version matches `lockss-core` version
    *   GitHub: https://github.com/lockss/lockss-core-bundle
*   `org.lockss:lockss-junit4-bundle`
    *   Maven dependency type: `<type>pom</type>`
    *   Maven dependency scope: `<scope>test</scope>`
    *   Stable version: 1.1.0
    *   Development version: 1.2.0-SNAPSHOT
    *   GitHub: https://github.com/lockss/lockss-junit4-bundle
*   `org.lockss:lockss-junit5-bundle`
    *   Maven dependency type: `<type>pom</type>`
    *   Maven dependency scope: `<scope>test</scope>`
    *   Stable version: 1.1.0
    *   Development version: 1.2.0-SNAPSHOT
    *   GitHub: https://github.com/lockss/lockss-junit5-bundle

# Code Bundles

*   `org.lockss:lockss-util`
    *   Stable version: 1.6.0
    *   Development version: 1.7.0-SNAPSHOT
    *   GitHub: https://github.com/lockss/lockss-util
*   `org.lockss:lockss-spring-bundle`
    *   Stable version: 1.7.0
    *   Development version: 1.8.0-SNAPSHOT
    *   GitHub: https://github.com/lockss/lockss-spring-bundle

## Attic

### Renamed

*   `org.lockss:lockss-core-parent-pom -> org.lockss:lockss-core-bundle`
*   `org.lockss:lockss-spring-parent-pom -> org.lockss:lockss-spring-bundle`

### Deprecated

*   `org.lockss:lockss-core-spring-parent-pom`
    *   Inherit from `lockss-parent-pom` and depend on `lockss-spring-bundle` instead
