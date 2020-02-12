---
layout: page
title: CLOCKSS File Transfer Guidelines
---


## Overview

This document provides guidelines to enable content providers to support file transfer preservation through CLOCKSS, including guidelines for data, metadata, and transmission, as well as descriptions of the evaluation, setup, and production processes. Ideally we can work with your existing practice, which will be reviewed during the evaluation phase.


## Specifications


#### Packaging


Deliveries should include:
 + both content and all related metadata
 + materials as discrete file data: 
    - [ ] in a single directory, or
    - [ ] in a directory tree, or
    - [ ] packaged in a non-proprietary package format (e.g., tar, zip). 
 + consistent metadata to content relationships:
    - [ ] one metadata file per content file (1:1) or 
    - [ ] one metadata file per multiple content files (1:M), with metadata file names that include a timestamp or other unique identifier.


#### Content



 - [ ] final content, no pre-publication content
 - [ ] non-proprietary formats only (e.g., PDF, HTML)
 - [ ] a maximum of one non-text format for each item, (e.g., PDF, EPUB, MOBI)


#### Metadata



 - [ ] text formats (e.g., XML, RIS)
 - [ ] standard metadata schemas preferred (e.g., JATS, ONIX, PubMed, Crossref)

*Scholarly content:* metadata must include the DOI, publication name, publication date, access URL, and ISSN or ISBN as appropriate. Additional metadata could include: item title, series title, volume, issue, author, and page range. 

*Content other than scholarly books & journals:* metadata must deliver enough information to uniquely identify the item, for example, the DOI or other identifier, provider, publication date, and access URL.


#### File Names

We can work with many varieties of file-naming conventions, as long as the full path with the filename is codifiable, unique, and remains consistent over time. Here are some examples of how this can be accomplished.

Metadata files map to content file(s) consistently. For example:



*  for a 1:1 relationship, options include: 
    *  using the same base filename for each file pair, or
    *  using the same base filename for each file pair, with codified differences.
*  for a 1:Many relationship, content filenames may:
    *  be contained in the XML file along with the related metadata,  \
e.g., <content_filename>fred_smith_2002.pdf</content_filename>
    *  be built up from metadata elements identified in the XML, for example, journal_id + volume + start_page, e.g., foo_17_101.pdf
    *  correspond to the doi of the article in question with underbars in place of "/", e.g. “10.1111/foo/xxx2018.1" would be "10.1111_foo_xxx2018.1.pdf"
    *  use a publisher specific identifier for the content, e.g., xxx2019.1.pdf

Note: For a 1:Many relationship, metadata filenames must contain a date stamp or other unique identifier (e.g., Atypon extracts).


#### Transmission

Transmissions can be scheduled at any time. 

We accept data:



 - [ ] pushed to our CLOCKSS FTP server (CLOCKSS SFTP coming soon); or 
 - [ ] which we can pull from FTP or SFTP servers. We have some ability to pull from an AWS bucket, rsync target, or other custom source.

Establish and implement standards for: 



 - [ ] uniquely-named deliveries; and 
 - [ ] a defined schedule: annually, monthly, or continually.

Note: if a standard part of your delivery process is email delivery notifications, we will provide an email alias.


## Evaluation

The first stage in preservation is to determine if the content format is standard or custom. Sample content must furnish enough context to process and preserve the materials with the associated metadata. At the end of this phase a determination of whether to continue is made between the publisher and CLOCKSS.

For an accurate evaluation, please deliver the following:


#### Information



 - [ ] a description of the file structure: flat directory? directory tree? zip or tar file? How many levels deep is the file structure?
 - [ ] a description of the relationship between the metadata files and the content files: Is there one metadata file for each content file (1:1) or is there one metadata file for multiple content files (1:M)? Are metadata and content files in the same directory or seperated?
 - [ ] the schema of valid XML files (if used): JATS 2, JATS 3, Crossref 2, Crossref 3, ONIX 2, ONIX 3, NLM, or custom schema?


#### Sample content



 - [ ] at least one example of each file type to be preserved with any relevant metadata.
 - [ ] for a 1:1 relationship a minimum of 4 files: 2 metadata and 2 content files. The naming convention of the files should demonstrate the relationship between the metadata file and the content file.
 - [ ] for a 1:M relationship a minimum of 3 files: 1 metadata and 2 content files. The metadata file should contain at least two sections, one for each content file, each with a reference to the relative content file. 


## Setup Phase

Once an agreement has been reached, we begin development of a plugin which can parse the content directory or package structure, filenames, and metadata. We test the plugin by crawling content delivered in the evaluation phase. 

File naming and directory structure may change as we request alterations or you update your standards. However, once the setup phase ends, it is vital to maintain file naming and directory structure conventions consistently.


## Production Phase

Once the setup is complete, permanent archiving begins. No data that remains in the deposit location after the setup phase will be permanently archived, unless requested otherwise. 

Start uploading content according to your schedule. We accept content any time day or night. New or updated files will be pulled into our ingest process once per day. Once material has been processed, we may remove it from the deposit location without notice.

When a file must be revised, upload the updated file using the same file name. We automatically detect replaced files and version the previous copies in our archive.

Once the production phase starts, follow the delivery standards agreed upon in the evaluation and setup phases, otherwise additional setup costs may be incurred.


