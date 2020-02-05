---
layout: page
title: Configuring the LOCKSS System
---

*This information applies to version 2.0-alpha2 of the LOCKSS system.*

After [installing the LOCKSS system](installing) and [downloading the LOCKSS Installer](installing/lockss-installer), configure the system with the configure script:

    scripts/configure-lockss

(If you have experience with a classic LOCKSS daemon version 1.x, this is the equivalent of `hostconfig`.)

When run the first time the questions asked by the script often come with a suggested value, displayed in square brackets; hit Enter to accept the suggested value, or type the correct value and hit Enter.  Any subsequent runs will use the previous values ad the suggested value, review and hit Enter to leave unchanged.

 Questions include:

1.  `Fully qualified hostname (FQDN) of this machine`: enter the machine's hostname (e.g. `locksstest.myuniversity.edu`)
1.  `IP address of this machine`: the publicly routable IP address of the machine, or if it is not publicly routable but will be accessible via network address translation (NAT), its IP address on the internal network
1.  `Is this machine behind NAT?` Enter `Y` if the machine is not publicly routable but will be accessible via network address translation (NAT), or `N` otherwise
    1.  `External IP address for NAT`: if you answered `Y` in the previous question, enter the publicly routable IP address of the machine.
1.  `Initial subnet for admin UI access`: enter a semicolon-separated list of subnets in CIDR notation that should have access to the Web user interfaces of the system
1.  `LCAP V3 protocol port`: enter the port on the publicly routable IP address that will be used to receive LCAP (LOCKSS polling and repair) traffic. Historically, most LOCKSS nodes use 9729.
1.  `PROXY port`: not yet re-enabled in 2.0-alpha; ignore
1.  `Mail relay for this machine`: hostname for this machine's outgoing mail server
1.  `Does mail relay <mailhost> need user & password`: enter `Y` if the machine's outgoing mail server requires password authentication, `N` otherwise
    1. `User for <mailhost>`: if you answered `Y` to the outgoing mail server password authentication question, enter the username for the mail server
    1. `Password for <mailuser>@<mailhost>`: enter the mail server password for the given username
    1. `Again`: re-enter the mail server password for the given username (if the two passwords do not match, the password will be asked again)
1.  `E-mail address for administrator`: enter the e-mail address of the person or team who will administer the LOCKSS system on this machine
1.  `Configuration URL`: enter the URL of the LOCKSS network configuration file. If you are not running your own, use `http://props.lockss.org:8001/demo/lockss.xml`, the configuration file for a demo network set up for LOCKSS 2.0 pre-release testing.
1.  `Configuration proxy (host:port)`: enter a host:port combination for the proxy server needed to reach the network configuration file (or simply hit Enter if none is needed)
1.  `Preservation group(s)`: enter a semicolon-separated list of preservation network identifiers. If you are not joining an existing network or running your own, enter `demo`, the network identifier for the demo network set up for LOCKSS 2.0 pre-release testing.
1.  `Content data storage directory`: enter the path of a directory that is the root of the main storage area of the LOCKSS system. *If you are used to the classic LOCKSS daemon (1.x), this would be the equivalent of `/cache0`.*
1.  `Service logs directory`: enter the path of a directory that is the root of the storage area for LOCKSS-related log files (historically `/var/log/lockss`)
1.  `Temporary storage directory`: not actively used in LOCKSS 2.0-alpha ignore
1.  `User name for web UI administration`: enter the username for an administrative user in the LOCKSS system's Web user interfaces
1.  `Password for web UI administration user <uiuser>`: enter the password for the given administrative user in the LOCKSS system's Web user interfaces[<sup>1</sup>](#n1)
1.  `Password for web UI administration (again)`: re-enter the password for the given administrative user in the LOCKSS system's Web user interfaces (if the two passwords do not match, the password will be asked again)
    
The next set of questions will gather information about which of the LOCKSS services you will be using and how to access any service you have already configured for use:

1.  `Use LOCKSS Metadata Query Service?`: Enter `Y` to use the included metadata service or `N` and no metadata service will be run.
1.  `Use LOCKSS Metadata Extractor Service?`: Enter `Y` to use the metadata extraction service or `N` and no metadata extraction service will be run.
1.  `Use LOCKSS PostgreSQL DB Service?`:
    *   Enter `Y` to use the included PostgreSQL database.
        1.  `Password for database:` Enter the password for the PostgreSQL database included in LOCKSS 2.0-alpha2.[<sup>1</sup>](#n1)
        1.  `Password for database (again):` Re-enter the password for the PostgreSQL database (if the two passwords do not match, the password will be asked again)
    *   Enter `N` if you wish to use your own PostgreSQL database. You will be queried for the details of your PostgreSQL service.
        1.  `Fully qualified hostname (FQDN) of PostgreSQL host:` Enter the hostname (e.g. `mysql.myuniversity.edu`)
        1.  `Port used by PostgreSQL host:` Enter the port your running postgres sql can be reached at.
        1.  `Login name for PostgreSQL database: [LOCKSS]` Enter name used to login to the postgres service, the default is LOCKSS.
        1.  `Schema for PostgreSQL service: [LOCKSS]` Enter the schema to be used by LOCKSS, the default is LOCKSS.
        1.  `Database name prefix for PostgreSQL database: [Lockss]` Prefix to use for any LOCKSS databases.
        1.  `Password for database:` enter the password for your PostgreSQL database.[<sup>1</sup>](#n1)
        1.  `Password for database (again):` re-enter the password for your PostgreSQL database (if the two passwords do not match, the password will be asked again)
1.  `Use LOCKSS Solr Service?:`
    *   Answer `Y` if you wish to use the included Solr install.
    *   Answer `N` if you wish to use your own Solr service.
        1.  `Fully qualified hostname (FQDN) of Solr host:` Enter the hostname (e.g. `mysql.myuniversity.edu`)
        1.  `Port used by Solr host:` Enter the port your running postgres sql can be reached at.
        1.  `Solr core repo name: [lockss-repo]` Enter name for the Solr core repo, the default is `lockss-repo`.
1.  `Use LOCKSS PyWb Service?:`Answer `Y` to use PyWb, answer `N` and you will be offered the option to use OpenWayback.
1.  **OK to store this configuration**: confirm with `Y` that the summarized configuration data is correct and that you are ready to write it to a file

You will prompted to run `scripts/start-lockss` to start the configured system.



#### Footnotes

<a id="n1">[1]</a>: Passwords are not stored unencrypted by LOCKSS.  You should store them in a safe place as you will need them each time you run scripts/configure-lockss. If you need to change your passwords, rerun scripts/configure-lockss.
