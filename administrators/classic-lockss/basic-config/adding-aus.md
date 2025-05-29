---
layout: page
title: Adding AUs
---

Your LOCKSS Box will collect and preserve open access content and materials to which your institution subscribes.

### Understanding AUs

Content is organized in units called AUs (Archival Units).  An AU is the smallest indivisible collection of content that a LOCKSS cache preserves. For electronic journals, an AU usually corresponds to a single volume of a single journal. For other types of content an AU may be an entire site, or any convenient, but well-defined, subset of the site.

### Accessing the LOCKSS UI

Content is added to your LOCKSS Box using the LOCKSS Admin UI (User Interface).  The LOCKSS Admin UI is accessed from your Internet browser.  The person who sets up your LOCKSS Box will provide you with a username (normally “lockss”), a password, and a URL to connect to enter in your browser (something like“http://<yourLOCKSSbox>:8081/”)

### Adding Content

1. Log in to your LOCKSS Admin UI with your Internet browser
1. Select **Journal Configuration** (for managing content)
1. Select **Add Titles** (to add  content)
1. You will see a list of collections available to you. Each collection will be followed by a number indicating the number of AUs within that collection which can be added.  Select the collections you wish to add AUs from,and then press the **Select Titles** button.
1. If your LOCKSS box has multiple disks, you will see a list of Available Disks and one these disk will be marked with a check. Under normal circumstances, you should select ALL of your disks so that the AUs you select are evenly distributed. If you LOCKSS box has a single disk, you will not see a list of Available Disks and you can proceed to the next step.
1. Select the individual titles you wish to collect in your LOCKSS machine. You may also press the **Select All** button to select all the titles on this screen.
1. Press the **Add Selected** AUs button to add content. It may take several moments for you choices to be confirmed, especially if you are adding a lot of content.

The LOCKSS daemon will shortly begin to collect the content and store it within your LOCKSS machine. You can check the progress of this by following the instructions outlined in the next section. Once the retrieval of content has completed, you can confirm that content has been correctly retrieved by viewing your content.

### Additional Notes

A list of [publishers and titles](https://reports.lockss.org/keepers/) is available. Most content is available to Alliance members only. Detailed here is the content publishers have committed for preservation, the titles already made available for preservation and titles that are in process. To see what content is currently available for preservation, login to your LOCKSS Box interface and visit the Add Titles menu. Alternatively, use the Title List feature available in the navigation menu.

Occasionally, a title may temporarily be unavailable for retrieval: if a publisher changes the structure of their site,the plugin used by LOCKSS to retrieve the appropriate content may need to be updated. Fresh retrieval of this content will not be possible until the redevelopment work required to make this plugin conform to the new site has been completed.

Before your LOCKSS box can collect content for preservation, a publisher must give permission via a LOCKSS permission statement. Your LOCKSS Box can only collect and preserve content when it can access the publisher’s LOCKSS permission statement, which is hosted on their server. Publishers control access to the permission statement via IP authentication. You will be able to collect and preserve only open access titles and titles to which you subscribe.

If you administer your LOCKSS Box by “adding all available content” you will receive many ‘No permission from publisher’ crawl results but no harm will be done. Establishing the lack of permission will inevitably take time that could be better used in collecting the content to which you do have access. Once you can identify the titles failing to collect, you may find it helpful to clean up your interface by removing them.

IMPORTANT NOTE: Some publishing platforms require librarians to register their Global LOCKSS Network LOCKSS box IP address. A list of [impacted publishers and contacts is here](https://lockss.github.io/administrators/classic-lockss/atypon-publishers-gln).


