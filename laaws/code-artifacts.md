---
layout: page
permalink: /laaws/code-artifacts/
---
# Code Artifacts

The Maven code artifacts of the LOCKSS software are:

## POM Files

### Parent POMs

*   `org.lockss:lockss-parent-pom`
    *   Version: 1.7.0
    *   GitHub: https://github.com/lockss/lockss-parent-pom

### POM Bundles

* `org.lockss:lockss-core-bundle`
    *   Version: 1.1.1
    *   Note: Unless otherwise specified, version matches `lockss-core` version
    *   GitHub: https://github.com/lockss/lockss-core-bundle
*   `org.lockss:lockss-junit4-bundle`
    *   Version: 1.1.0
    *   GitHub: https://github.com/lockss/lockss-junit4-bundle
*   `org.lockss:lockss-junit5-bundle`
    *   Version: 1.1.0
    *   GitHub: https://github.com/lockss/lockss-junit5-bundle
*   `org.lockss:lockss-spring-bundle`
    *   Version: 1.7.0
    *   GitHub: https://github.com/lockss/lockss-spring-bundle

## Core

*   `org.lockss.laaws:lockss-core`
    *   Version: 1.1.1
    *   GitHub: https://github.com/lockss/lockss-core

## Repository

*   `org.lockss.laaws:laaws-repository-core`
    *   Version: 1.11.4
    *   GitHub: https://github.com/lockss/laaws-repository-core
*   `org.lockss.laaws:laaws-repository-service`
    *   Version: 1.7.0
    *   GitHub: https://github.com/lockss/laaws-repository-service
*   `org.lockss.laaws:laaws-repository-client`
    *   Version: 1.5.0
    *   GitHub: https://github.com/lockss/laaws-repository-client

## Attic

### Renamed

*   `org.lockss:lockss-core-parent-pom -> org.lockss:lockss-core-bundle`
*   `org.lockss:lockss-spring-parent-pom -> org.lockss:lockss-spring-bundle`

### Deprecated

*   `org.lockss:lockss-core-spring-parent-pom`
    *   Use `org.lockss:lockss-core-bundle` and `org.lockss:lockss-spring-bundle` in combination
