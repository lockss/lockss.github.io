---
layout: page
title: Setting Up a Props Server
---

As mentioned in the [introduction](../introduction), a **LOCKSS props server** is a Web server that hosts a LOCKSS network configuration file, a LOCKSS plugin registry and a LOCKSS title database file in one place.

## Host

If you do not have an existing Web server, or an existing host machine on which to install a Web server, set up a generic **Linux** host (bare-metal or virtual) that can house a modest Web server.

The LOCKSS Program at Stanford University Libraries operates props servers for various LOCKSS networks; our largest plugin registry (with hundreds of plugins, some with a 15-year history) is about 500MB, and the largest title database file is about 1GB. A network configuration file is a small text file, so it is fair to say that provisioning **a few gigabytes of disk space** for the props server in total is ample. The props server is low-traffic and requires **minimal CPU and memory**.

## Web Server

If you do not have an existing Web server on your Web server host, install one of your choice. We recommend the [Apache Web server](http://httpd.apache.org/); instructions below work with Apache but can be adapted to other environments.

## Checklist

The instructions below use the following placeholders:

*   `${NETNAME}`: The full name of the LOCKSS network. Example value: `My Big LOCKSS Network`
*   `${NETCODE}`: A short code representing the name of the LOCKSS network in directory and file names and URLs. Recommended: a single, lowercase word suitable for a host name. Example value: `mybiglockssnet`
*   `${PROPSHOST}`: The host name of the props server machine. Example value: `props.mybiglockssnet.org`
*   `${PROPSPORT}`: The listening port number for the props server's Web server. Recommended value: `8001`
*   `${STAFFGROUP}`: A user group on the props server host shared by the users who need to perform tasks on the files served by the Web server, such as releasing plugins or updating
title database files. Recommended value: `propsstaff`
*   `${WEBUSER}`: The system user on the props server host under which the Web server
runs. For example, on CentOS 7 for the Apache Web server, this is `apache`.
*   `${WEBGROUP}`: The system group on the props server host associated with `${WEBUSER}`.
For example, on CentOS 7 for the Apache Web server, this is `apache`.
*   `${WEBCONF}`: The directory where the Web server configuration files are located on the
props server host. For example, on CentOS 7 for the Apache Web server, this is `/etc/httpd`.
*    `${WEBROOT}`: The path of the Web server's overall root directory for files. This means that `${WEBROOT}/foo.gif` corresponds to (for instance) `http://www.example.com/foo.gif`. For example, on CentOS 7 for the Apache Web server, this is `/var/www/html`.
*    `${NETROOT}`: The path of the Web server's root directory for files devoted to the
props server. This is a path below `${WEBROOT}`. Recommended value: `${WEBROOT}/${NETCODE}`.
*   `${WEBMASTERADDR}`: A contact e-mail address for the webmaster or administrator of the props server host. Example value: `webmaster@mybiglockssnet.org`

## Staff Group

We recommend the creation of a props server staff group so all users who share responsibilities in updating the network configuration file, plugins, or title database files of the network can do so collaboratively.

Create the props server staff group with `groupadd`:

    sudo groupadd --system ${STAFFGROUP}

With the recommended values in the [checklist](#checklist), this is:

    sudo groupadd --system propsstaff

For each user `${USER}` that needs to be added to the `${STAFFGROUP}` group, as well as the
`${WEBUSER}` system user, issue the following `usermod` command:

    sudo usermod --groups ${STAFFGROUP} --append ${USER}

With the recommended values in the [checklist](#checklist), for a user named `jsmith`, this is:

    sudo usermod --groups propsstaff --append jsmith

Although in principle group changes take effect immediately, as evidenced by (for example) `groups jsmith`, in practice active sessions that pre-date the group change often do not see the update promptly, so we recommend logging out and initiating new sessions for such users.

## Directory Structure

The recommended directory and file structure is:

*   `${NETROOT}/` (the root of the props server)
    *   `lockss.xml` (the network configuration file)
    *   `plugins/` (the root of the plugin registry)
        *   `Plugin1.jar`
        *   `Plugin2.jar`
        *   ...
    *   `titledb/` (the root of the title database)
        * `titledb.xml` (the single title database XML file)

Create the directory structure with these commands:

    sudo mkdir ${NETROOT} ${NETROOT}/plugins ${NETROOT}/titledb
    sudo chown --recursive root:${STAFFGROUP} ${NETROOT}
    sudo chmod --recursive 2775 ${NETROOT}

With the recommended values in the [checklist](#checklist), this is:

    sudo mkdir /var/www/html/mybiglockssnet \
               /var/www/html/mybiglockssnet/plugins \
               /var/www/html/mybiglockssnet/titledb
    sudo chown --recursive root:propsstaff /var/www/html/mybiglockssnet
    sudo chmod --recursive 2775 /var/www/html/mybiglockssnet

## Configuration

Configure your Web server to serve `${NETROOT}` over port `${PROPSPORT}`, and restrict access to the IP addresses of the LOCKSS preservation nodes in the network, as well as any useful IP addresses of staff members or developers who might want to see or use the props server from their own machines.

### Apache Example

Please refer to <http://httpd.apache.org/docs/> for Apache configuration information. The instructions in this section are given as examples of what it looks like to set up Apache to serve the props server.

1.  Edit `${WEBCONF}/conf/httpd.conf` as root.

    1.  Make sure there is a Listen directive for `${PROPSPORT}`:

            Listen ${PROPSPORT}

        Using the recommended value in the [checklist](#checklist), this would be:

            Listen 8001

        Note: The Listen directive can also bind to specific IP addresses, including a syntax for IPv6 addresses. See <https://httpd.apache.org/docs/2.4/mod/mpm_common.html#listen> for details.

        Important: Please note that this is a global setting.

    1.  Set the server name to `${PROPSHOST}` and the administrator e-mail address to `${WEBMASTERADDR}` in the `ServerName` and `ServerAdmin` directives, respectively:

            ServerName ${PROPSHOST}
            ServerAdmin ${WEBMASTERADDR}

        Using the example values in the [checklist](#checklist), this is:

            ServerName props.mybiglockssnet.org
            ServerAdmin webmaster@mybiglockssnet.org

    1.  Verify that the file ends (or contains) an `IncludeOptional` (or perhaps `Include`) directive for files matching `conf.d/*.conf`, and add one if needed:

            IncludeOptional conf.d/*.conf

        This pattern is relative to the path known as `ServerRoot` in the configuration file. For example on CentOS, `ServerRoot` is `/etc/httpd`. Adjust as needed depending on the actual value of `ServerRoot`, so that the files in question are `${WEBCONF}/conf.d/*.conf`.

    1.  *(optional)* Check the file for other configuration parameters you might like to adjust.

1.  Create the file `${WEBCONF}/conf.d/${NETCODE}.conf` as root in a text editor.

    Tip: If you are sharing with an existing Web server, you will likely be creating a virtual host, which can be defined in this file.

    1.  Create a `<Directory>` block for your props server root directory `${NETROOT}`:

            <Directory "${NETROOT}">
                Options Includes FollowSymLinks MultiViews
                Order allow,deny
                Include ${WEBCONF}/access.d/${NETCODE}.acl
            </Directory>

        With the defaults and examples in the [checklist](#checklist), this corresponds to:

            <Directory "/var/www/html/mybiglockssnet">
                Options Includes FollowSymLinks MultiViews
                Order allow,deny
                Include /etc/httpd/access.d/mybiglockssnet.acl
            </Directory>

        The purpose of the `Include` directive is to refer to your network's access control list (list of authorized IP addresses). See the definition of `${WEBCONF}/access.d/${NETCODE}.acl` in the
next step.

    1.  Create a `<Directory>` block for your plugin registry `${NETROOT}/plugins`:

            <Directory "${NETROOT}/plugins">
                Options Indexes FollowSymLinks MultiViews
                IndexOptions IgnoreCase SuppressHTMLPreamble
                HeaderName HEADER.html
                ReadmeName FOOTER.html
                IndexIgnore .. FOOTER*
            </Directory>

        With the defaults and examples in the [checklist](#checklist), this is:

            <Directory "/var/www/html/mybiglockssnet/plugins">
                Options Indexes FollowSymLinks MultiViews
                IndexOptions IgnoreCase SuppressHTMLPreamble
                HeaderName HEADER.html
                ReadmeName FOOTER.html
                IndexIgnore .. FOOTER*
            </Directory>

1.  Create the directory `${WEBCONF}/access.d` if it does not exist:

        sudo mkdir -p ${WEBCONF}/access.d

    Using the defaults and examples in the [checklist](#checklist), this is:

        sudo mkdir /etc/httpd/access.d

1.  Create the file `${WEBCONF}/access.d/${NETCODE}.acl` as root in a text editor.

    Add one `Allow` directive per IP address of a LOCKSS preservation node in your network (and additional staff and develop IP addresses). We recommend adding comments (beginning with the character `#` and extending to the end of the line) to annotate the list of IP addresses with location names and host names, for reference. Example:

        Allow from 10.1.2.3        # lockss.auniversity.edu (A University)
        Allow from 1.2.3.4         # lockss1.buniversity.edu (B University)
        Allow from 192.168.2.3     # mybiglockssnet.cuniversity.edu (C University)
        Allow from 192.168.100.101 # lockss.duniversity.edu (D University)

    You may not know all necessary IP addresses at the inception of the network; add more over time.

    Note: The syntax of the `Allow` directive allows for IPv6 addresses, subnets (ranges) in IP/netmask or in CIDR notation, and more. See <https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html#allow>.

    Tip: In the event your LOCKSS network is open-ended rather than private, you would simply have this version of the Allow directive instead:

        Allow from all

1.  Place the following HTML fragment in `${NETROOT}/plugins/HEADER.html`:
```html
        <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
        <HTML>
          <HEAD>
            <TITLE>${NETNAME} Plugin Registry</TITLE>
          </HEAD>
          <BODY>
            <H1>${NETNAME} Plugin Registry</H1>
```
    Substitute the formal name of your network in the `<title>` and `<h1>` tags. With the example given in the [checklist](#checklist), this would be:
```html
        <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
        <HTML>
          <HEAD>
            <TITLE>My Big LOCKSS Network Plugin Registry</TITLE>
          </HEAD>
          <BODY>
            <H1>My Big LOCKSS Network Plugin Registry</H1>
```
1.  Place the following HTML fragment in `${NETROOT}/plugins/FOOTER.html`:
```html
            <P>
              LOCKSS system has permission to collect, preserve, and serve this Archival Unit
          </BODY>
        </HTML>
```
    The sentence `LOCKSS system has permission to collect, preserve, and serve this Archival Unit` must be verbatim, as it is the permission statement the LOCKSS crawler looks for to determine that it has permission to harvest the plugins contained in the plugin registry.

1.  *(optional)* If the firewall on your operating system only allows traffic to typical ports, it may not include
`${PROPSPORT}`. For example on CentOS using `firewall-cmd`, issue the following commands:

        sudo firewall-cmd --permanent --add-port=${PROPSPORT} /tcp
        sudo firewall-cmd --reload

    Using the recommended value in the [checklist](#checklist), this is:

        sudo firewall-cmd --permanent --add-port=8001 /tcp
        sudo firewall-cmd --reload

1.  Start the Apache Web server, for instance on CentOS:

        sudo systemctl start httpd
