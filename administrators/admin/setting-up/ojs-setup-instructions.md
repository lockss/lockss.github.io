---
layout: page
title: Enable OJS Platform for Preservation in LOCKSS or CLOCKSS
---

Once an agreement is reached with LOCKSS reguarding preservation, settings within the OJS Administrative 
interface make it possible for collection and preservation through the 
LOCKSS Global Network or the CLOCKSS Network.

For more information contact us at: <a href="https://www.lockss.org/contact">https://www.lockss.org/contact</a>

### OJS 2.X.X

Configuring OJS v2.X.X content for CLOCKSS/LOCKSS preservation:

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


### OJS 3.X.X

Configuring OJS v3.X.X content for LOCKSS/CLOCKSS preservation:

If your version of OJS v3.X.X is before 3.1.2 you will need to either:

* upgrade to 3.1.2 or higher; or
* apply a patch before you can successfully enable CLOCKSS &/or LOCKSS preservation.

The information we have is that the most recent commit of the fix can be found at 
https://github.com/pkp/ojs/pull/2215/commits/22f1d220. The 3.1.2 GitHub milestone and its progress is at 
https://github.com/pkp/pkp-lib/milestone/32.

To enable preservation:
1. View the Website Setting section. For reference see: 
https://docs.pkp.sfu.ca/learning-ojs/en/settings-distribution#archiving
2. On the Archiving tab, check the boxes to "Enable LOCKSS" &/or "Enable 
CLOCKSS" as desired.
2. To review the manifest page, click on "Publisher Manifest" next to the check boxes. 
The resulting page should show a listing of your journal issues.
