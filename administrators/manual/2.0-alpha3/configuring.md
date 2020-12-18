---
layout: page
title: Configuring the LOCKSS System
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

After [installing the LOCKSS system](installing), configure the system with the configure script:

    scripts/configure-lockss

(If you have experience with classic LOCKSS daemon version 1.x, this is the equivalent of `hostconfig`.)

When run the first time, some of the questions asked by the script will have a suggested or default value, displayed in square brackets; hit Enter to accept the suggested value, or type the correct value and hit Enter.  Any subsequent runs will use the previous values as the default value; review and hit Enter to leave unchanged. Password prompts will not display the previous value but can still be left unchanged with Enter.

The questions are:

1.  `Fully qualified hostname (FQDN) of this machine:` Enter the machine's hostname (e.g. `locksstest.myuniversity.edu`).
1.  `IP address of this machine:` The publicly routable IP address of the machine, or if it is not publicly routable but will be accessible via network address translation (NAT), its IP address on the internal network.
1.  `Is this machine behind NAT?:` Enter `Y` if the machine is not publicly routable but will be accessible via network address translation (NAT), or `N` otherwise.
    1.  `External IP address for NAT:` If you answered `Y` to the previous question, enter the publicly routable IP address of the NAT router.
1.  `Initial subnet for admin UI access:` Enter a semicolon-separated list of subnets in CIDR or mask notation that should initially have access to the Web user interfaces of the system. The access list can be modified later via the UI.
1.  `LOCKSS subnet for container access:` This is calculated from the MicroK8s node and should not need to be modified in a standard installation.
1.  `LCAP V3 protocol port:` Enter the port on the publicly routable IP address that will be used to receive LCAP (LOCKSS polling and repair) traffic. Historically, most LOCKSS nodes use 9729.
1.  `PROXY port:` Port for the LOCKSS content proxy.  Accept the default - it can be changed later if necessary.
1.  `Mail relay for this machine:` Hostname of this machine's outgoing mail server.
1.  `Does mail relay <mailhost> need user & password`: Enter `Y` if the outgoing mail server requires password authentication, `N` otherwise.
    1. `User for <mailhost>:` If you answered `Y` to the outgoing mail server password authentication question, enter the username for the mail server.
    1. `Password for <mailuser>@<mailhost>:` Enter the password for the given username.
    1. `Password for <mailuser>@<mailhost> (again):` Re-enter the mail server password (if the two passwords do not match, the password will be asked again).
1.  `E-mail address for administrator:` Enter the e-mail address of the person or team who will administer the LOCKSS system on this machine.
1.  `Configuration URL:` Enter the URL of the LOCKSS network configuration file. If you are not running your own LOCKSS network, use `http://props.lockss.org:8001/demo/lockss.xml`, the configuration file for a demo network set up for LOCKSS 2.0 pre-release testing.
1.  `Configuration proxy (host:port):` If a proxy server is required to reach the configuration server, enter its host:port here, otherwise leave this blank.
1.  `Preservation group(s):` Enter a semicolon-separated list of preservation network identifiers. If you are not joining an existing network or running your own, enter `demo`, the network identifier for the demo network set up for LOCKSS 2.0 pre-release testing.
1.  `Content data storage directory:` Enter the full path of a directory to use as the root of the main storage area of the LOCKSS system. This is where preserved content will be stored, along with several databases; it is the analog of `/cache0` in the classic LOCKSS system.
1.  `Use additional directories for content storage?:` If you want to use more than one filesystem to store preserved content answer `Y`.
    1.  `Enter path to additional content storage directory <n> (q to quit):` If you entered `Y` to `Use additional directories` you will be prompted repeatedly for those paths; enter them one at a time, then enter `q` when done.
1.  `Service logs directory:` Defaults to the content data storage directory; enter a different path if you want to put the logs elsewhere. *In the classic LOCKSS system this was `/var/log/lockss`, but now there will be a set of subdirectories, one for each component service.*
1.  `Temporary storage directory:` Defaults to the content data storage directory. If that directory is remote (e.g., NFS), performance can be improved by supplying a local disk directory here. Don't use a RAM-based tmpfs; in some circumstances a substantial amount of temporary space (tens of GB) may be needed.
1.  `User name for web UI administration:` Enter a username for the primary administrative user in the LOCKSS system's Web user interfaces.
1.  `Password for web UI administration user <uiuser>:` Enter a password for the primary administrative user.
1.  `Password for web UI administration user <uiuser> (again):` Re-enter the password for the primary administrative user (if the two passwords do not match, the password will be asked again).
1.  `Use LOCKSS Metadata Query Service?:` Enter `Y` if you want the metadata query service to be run, otherwise `N`.
1.  `Use LOCKSS Metadata Extractor Service?:` Enter `Y` if you want the metadata extraction service to be run, otherwise `N`.
1.  `Use LOCKSS PostgreSQL DB Service?`:
    *   Enter `Y` to use the embedded PostgreSQL database. This is recommended in most cases.
        1.  `Password for PostgreSQL database:` Enter a password for the embedded PostgreSQL database.
        1.  `Password for PostgreSQL database (again):` Re-enter the password for the PostgreSQL database (if the two passwords do not match, the password will be asked again).
    *   Enter `N` if you wish to use your own PostgreSQL database. You will be queried for the details of your PostgreSQL service.
        1.  `Fully qualified hostname (FQDN) of PostgreSQL host:` Enter the hostname of your PostgreSQL database (e.g. `mypgsql.myuniversity.edu`).
        1.  `Port used by PostgreSQL host:` Enter the port where your running PostgreSQL database can be reached.
        1.  `Login name for PostgreSQL service:` Enter the user name for your PostgreSQL database. The default is `LOCKSS`.
        1.  `Schema for PostgreSQL service:` Enter the schema name to be used by the LOCKSS system. The default is `LOCKSS`.
        1.  `Database name prefix for PostgreSQL service:` Prefix to use for any LOCKSS databases. The default is `Lockss` (note the uppercase/lowercase).
        1.  `Password for PostgreSQL database:` Enter the password for your PostgreSQL database.
        1.  `Password for PostgreSQL database (again):` Re-enter the password for your PostgreSQL database (if the two passwords do not match, the password will be asked again).
1.  `Use LOCKSS Solr Service?:`
    *   Enter `Y` to use the embedded Solr server. This is recommended in most cases.
    *   Enter `N` to use your own Solr server.
        1.  `Fully qualified hostname (FQDN) of Solr host:` Enter the hostname of your Solr database server (e.g. `mysolr.myuniversity.edu`).
        1.  `Port used by Solr host:` Enter the port where your running Solr database server can be reached.
        1.  `Solr core repo name:` Enter name of the Solr core for the LOCKSS repository. The default is `lockss-repo`.
1.  `Use LOCKSS PyWb Service?:` Enter `Y` to use PyWb for content replay; enter `N` and you will be offered the option to use OpenWayback instead.
1.  `Use LOCKSS OpenWayback Service?:` Enter `Y` to use OpenWayback for content replay (only if you did not opt for PyWb). 
    1.  `Okay to turn off authentication for read-only requests for LOCKSS Repository Service?:` OpenWayback currently does not supply user credentials when reading content from the LOCKSS repository, so the repository must be configured to respond to unauthenticated read requests. Enter `Y` to accept this, otherwise OpenWayback will not be enabled.
1.  `OK to store this configuration:` Enter `Y` if the configuration values are to your liking, otherwise `N` to make edits.

If you enter `Y`, some checks will be run, necessary directories will be
created, and you will be prompted to run `scripts/start-lockss` to start the
configured system.

----
