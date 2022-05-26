---
layout: page
title: Enable OJS Platform for Preservation in LOCKSS or CLOCKSS
---

Once an agreement is reached regarding preservation, settings within the OJS Administrative 
interface make it possible for collection and preservation through the 
Global LOCKSS Network (GLN) or the CLOCKSS Network. For more information contact us at: <a href="https://www.lockss.org/contact">https://www.lockss.org/contact</a>

## OJS 2.X

OJS 2.X is retired and is not recommended for ongoing use. Please upgrade to OJS 3.X. For more information see <a href="https://pkp.sfu.ca/ojs/ojs_download/">https://pkp.sfu.ca/ojs/ojs_download/</a>.

### Configuring OJS 2.X content for GLN/CLOCKSS preservation:

1. Go to the Journal Management screen for each journal and click "Journal Setup".
2. Select the second item, "Policies".
3. Scroll down to section 2.6, "Journal Archiving".
4. Check the box "Enable LOCKSS..." to turn on the LOCKSS feature.
5. In text box beneath, type in the following sentence exactly as written: CLOCKSS system has permission to 
ingest, preserve, and serve this Archival Unit
6. Save your changes.
7. Verify changes by going to front page of your journal(s) in your browser:
8. Edit the URL in your browser URL bar (if applicable, delete the word 'index' from the very end of the 
URL) so that it ends with /gateway/lockss. (If you are redirected back to the front page, the configuration changes 
were not saved properly. Otherwise, you will see a LOCKSS-related page with the LOCKSS logo.)
9. Verify CLOCKSS by going to About and to Editorial Policies. Search for the CLOCKSS permission statement, 
which should appear towards the bottom of the page.


## OJS 3.X

We recommend using a recent stable version of OJS 3.X, OJS 3.1.3 at minimum. For more information 
see <a href="https://pkp.sfu.ca/ojs/ojs_download/">https://pkp.sfu.ca/ojs/ojs_download/</a>.

### Known Issues

#### OJS 3.1.2.1 

This version of OJS has a bug in the permission statement for the GLN. Please upgrade to a more recent version, 
OJS 3.1.3 or higher. If that is not an option, it may be possible to manually correct the permission statement.

#### OJS 3.1.1.X and before

These versions of OJS 3.X are not enabled for preservation in either CLOCKSS or the GLN. 
Please upgrade to a more recent version, OJS 3.1.3 or higher, or apply a patch before enabling 
CLOCKSS &/or LOCKSS preservation. A possible patch can be found at: <a href="https://github.com/pkp/ojs/pull/2215/commits/22f1d220">https://github.com/pkp/ojs/pull/2215/commits/22f1d220</a>.

### Configuring OJS 3.X content for GLN/CLOCKSS preservation:

1. View the <a href="https://docs.pkp.sfu.ca/learning-ojs/en/settings-distribution">Distribution Settings</a> section of the administrative interface.
2. On the <a href="https://docs.pkp.sfu.ca/learning-ojs/en/settings-distribution#archiving">Archiving tab</a>, check the boxes to "Enable LOCKSS" &/or "Enable 
CLOCKSS" as desired.
3. To review the manifest page, click on "Publisher Manifest" next to the check boxes. 
The resulting page should show a listing of your journal issues.
