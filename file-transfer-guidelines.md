---
layout: page
title: File Transfer Guidelines
---

To ingest content via file transfer technology for LOCKSS network preservation, please comply with the requirements below.

## Content delivery

### General requirements
* Uniquely named deliveries, including full text and supplemental materials.
* Clear, consistent file naming convention that correlates specific metadata to full text content.
* Full-text content in a standard readable form (e.g., PDF).
* Delivery of duplicative content only for corrections and updates.
* Delivery of final published content, no in-progress issues or pre-publication articles.
* Delivery may be in an archive or in unpacked directories but delivery must be in non-proprietary formats (such as tar and zip).

### Metadata requirements
* In order to identify the delivered content, a LOCKSS network requires metadata provided in a standard consistent text format, such as RIS or an XML schema. 
* Already supported formats include RIS, JATS, ONIX, PubMed, & CrossRef in addition to some popular publishing platform internal schemas.  
  * For JATS examples for journal article content, see: [http://jats.nlm.nih.gov/index.html](http://jats.nlm.nih.gov/index.html).
  * Sample files can be found at: [http://jats.nlm.nih.gov/publishing/tag-library/1.1d1/n-cq42.html](http://jats.nlm.nih.gov/publishing/tag-library/1.1d1/n-cq42.html).
  * For ONIX examples for book content, see:
  * For specific information about what is allowed in the schema, go to: [http://www.editeur.org/93/Release-3.0-Downloads/](http://www.editeur.org/93/Release-3.0-Downloads/).
  * Sample files can be found at: [http://www.editeur.org/files/ONIX%203/ONIX_Books_3.0_sample_2.zip](http://www.editeur.org/files/ONIX%203/ONIX_Books_3.0_sample_2.zip).
* Metadata to be supplied: DOI, publisher, publication date, ISSN or ISBN, and as appropriate: publication title, article/book title, series title, volume, issue.
* DOIs for journal articles and book titles are required.

### General optimizations
* Content as individual PDFs without redundant versions such as manuscript, epub, mobi.
* Notification to the delivery alias when a delivery has occurred.
* A listing of files delivered with updates clearly identified.
* Deliveries in tar or zip bundles should be completely self-contained. Multiple archives should not need to be expanded to map metadata to articles.
* Updates to previously delivered content would include just the modified items.
* Semi-annual list of individual items sent for preservation – e.g. all the ISSNs and DOIs.

## Server staging setup
* If the publisher has a staging server, please tell us: the location and password; the update schedule; the content removal schedule.
* If the publisher would like to send content to the LOCKSS network staging server, we will send you the location and password; please tell us your update schedule.

NOTE: do not routinely send "published before print" articles in your preservation feed.
