---
layout: page
title: LAAWS
---

The LAAWS project (short for "LOCKSS Architected As Web Services") is a
software re-architecture initiative aimed at unlocking the functionality of the
LOCKSS software into a suite of REST services.

## REST APIs

The API of each LAAWS REST service is described in a Swagger 2.0 specification,
which can be found in the component's Git repository in the file
`docs/swagger.yaml`. The specification can be used as input into another tool
to produce clients and server stubs in a variety of languages and frameworks.
The following HTML pages of API documentation were generated with the
[Swagger Codegen](https://swagger.io/tools/swagger-codegen/) tool:

*   [LOCKSS Repository Service REST API](apis/lockss-repository-service.html)
*   [LOCKSS Configuration Service REST API](apis/lockss-configuration-service.html)
*   [LOCKSS Metadata Extraction Service REST API](apis/lockss-metadata-extraction-service.html)
*   [LOCKSS Metadata Service REST API](apis/lockss-metadata-service.html)
*   [LOCKSS Poller Service REST API](apis/lockss-poller-service.html)

## See Also

*   [Code Artifacts](/developers/laaws/code-artifacts)
