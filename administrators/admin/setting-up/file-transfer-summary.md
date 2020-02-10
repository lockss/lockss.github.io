
# File Transfer Summary


## Overview

File transfer preservation is a method by which publishers control what documents and formats are preserved by delivering them to CLOCKSS through file transfer methodologies. This document provides a summary of the specifications and process. Ideally we can work with your existing practice, which will be reviewed during the evaluation phase of development.


## Specifications

Transmissions can be scheduled at any time. We accept data pushed to our CLOCKSS FTP server; or which we can pull from FTP or SFTP servers. We have some ability to pull from an AWS bucket, rsync target, or other custom source.

Metadata must deliver enough information to uniquely identify the items. We can work with many varieties of file-naming conventions, as long as the full path with the filename is codifiable, unique, and remains consistent over time. 



*   Deliveries should include:
    *   both content and related metadata; 
    *   consistent metadata to content relationships;
    *   non-proprietary formats only (e.g., PDF, HTML); 
    *   metadata in text formats (e.g., XML, RIS); and 
    *   standard metadata schemas preferred (e.g., JATS, ONIX, PubMed, Crossref).


## Evaluation Phase

The first stage in preservation is to determine if the content format is standard or custom. Sample content must furnish enough context to process and preserve the materials with the associated metadata. At the end of this phase a determination of whether to continue is made between the publisher and CLOCKSS.


## Setup Phase

Once an agreement has been reached, we begin development of a plugin which can parse the content directory or package structure, filenames, and metadata. We test the plugin by crawling content delivered in the evaluation phase. 


## Production Phase

Once the setup is complete, permanent archiving begins. Start uploading content according to your schedule. We accept content any time day or night. New or updated files will be pulled into our ingest process once per day. We automatically detect replaced files and version the previous copies in our archive.


