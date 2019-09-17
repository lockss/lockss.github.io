##Security Practices for LOCKSS

###SOURCE CONTENT:

Encrypting the content at the source is the best way to protect information.  Even if someone gets access to encrypted content, it is useless to them without the means to decrypt it.  For PII information it’s a standard practice.

The problem with putting encrypted data in an archive is that the encryption key(s) and the tool(s) to decrypt the content must be available when one wants to view the archived content.  If the source content is encrypted, some serious thought should be given to how the content would be decrypted in a distant future by people/organizations who may not have been associated when the content was first encrypted.



###CONTENT PRESENTATION FOR CRAWLING:

There are two ways to secure the presentation of content (presumably from a website)

1) Secure the web server with an SSL certificate.  This will allow the content to be encrypted when it is accessed over the network segments - a bad actor who is capturing packets would capture encrypted data that they would not easily be able to decrypt.

2) Use ACLs - an ACL will list the IP address(es) who are allowed to access content.  Since it’s likely that the web server will server multiple types of content to multiple consumers, it would be wise to segregate the content in such a way that allows individual ACLs to be specified for various types of content.  A “webserver-wide” ACL would likely be too broad unless all of the content presented on the webserver is intended for the same consumer.

Over time, requirements change, and it’s possible that an ACL set up for some content becomes out of date or otherwise incorrect.  For this reason, it would be a best practice to audit ACLs at a regular interval to make sure it is as narrowly focused as possible.

3) Use of firewalls - firewalls greatly enhance the security of an ACL by blocking traffic from unauthorized networks from ever accessing the webserver hosting content in the first place.  There are two types of firewalls - an external firewall typically maintained by an institution and an internal firewall supplied by the webserver’s operating system.



###CONTENT STORAGE ON A LOCKSS BOX:

1) LOCKSS Application User (password) - by default, a single application user with full admin rights is defined in /etc/lockss/config.dat by someone who has root privilege on the LOCKSS box.  Early LOCKSS implementations stored passwords in a SHA1 hash, more recent LOCKSS implementations will store the password in a much stronger SHA256 hash.  If a SHA1 hash is currently in use, consider updating that to a SHA256 has by re-running /etc/lockss/hostconfig.

2) LOCKSS Application Users (permission) - by default, a single application user with full admin rights is defined in /etc/lockss/config.dat by someone who has root privilege on the LOCKSS box.  Adding the setting "org.lockss.accounts.enabled=true” to Expert Config and restarting the LOCKSS daemon provides the capability to have multiple users with settable permissions.  For securing content, it could be a policy to provide MetaArchive users with only privilege to select AUs to be collected and preserved.  Someone with this level of permission would not be able to access stored content on their LOCKSS box or modify the LOCKSS Box configuration in such a way to grant access to content.

3) LOCKSS Content Services - there are a number of LOCKSS box content servers - Content Server, Content Proxy, and Audit Proxy.  If these services are enabled on dedicated ports, they provide unauthenticated access to stored content.  While the unauthenticated access is governed by an ACL, it’s possible that access to archived content could unintentionally be exposed through these settings.  Strategies to ensure this unauthenticated access is not enabled includes limiting who has Admin access to the box, implementing local firewall rules to block ports, and adding code to the daily MetaArchive cron script to report out on configured LOCKSS content services.

4) Secure Admin URL with SSL Certificate - by default, the username and password supplied to the LOCKSS GUI during login is unencrypted and can be exposed by a packet capture tool.  Securing the Admin URL with an SSL certificate will cause the LOCKSS GUI username and password to be encrypted before being sent out on the network.

5) Root Password Policy - most institutions will have a sensible root password policy that dictates how often the root password is changed and also dictates that the root password is immediately changed when a someone who knows the current password leaves the institution.  A policy like this should be applied to the LOCKSS box as well to ensure that only authorized persons at the institution can gain root access.
