# Installation

## Data directory

The IPT stores configuration, resources, users and logs in its data directory.  This can be set during installation, or the first time the IPT is run.

A typical location on Linux is `/var/lib/ipt` (installed from packages) or `/srv/ipt` (running in Tomcat).  On Windows, `C:\ipt-data` is appropriate.  The IPT must have write permission to the chosen location, see the [FAQ entry](faq.adoc#file-permissions) if you have problems.

<dl><dt><strong>🔥 CAUTION</strong></dt><dd>

Do not select a data directory that is vulnerable to inadvertent changes or removal. Do not use `/tmp`, for example, on systems where this folder may be emptied on a system restart.

**The data directory should be backed up regularly in keeping with an appropriate disaster recovery plan.**

Loss of the contents of the data directory will result in the loss of resource, user, and other configuration information and customizations to the IPT installation.
</dd></dl>

**📌 NOTE**\
If you have a data directory from a previously running IPT of the same version and want to use that previous configuration (including users and resources), you can enter the absolute path of that data directory below, or during the first step of the IPT setup.

## Installation method

There are several ways to install the IPT.

* Users of **Red Hat**, **CentOS**, **Debian**, **Ubuntu** or similar may install directly from [Linux packages](#installation-from-linux-packages).  This is the simplest method for the typical installation of a single IPT on a single server, and is also the easiest method to keep updated.
* Other **Linux** users, all **MS Windows** users, and those who wish to run multiple IPTs on the same server should instead look at the section on [Installation within a servlet container](#installation-within-a-servlet-container).
* **Docker** images are also available, see [Installation using Docker](#installation-using-docker).

## Installation from Linux packages

### RPM (Red Hat, CentOS etc)

To install the IPT onto Red Hat 8–9, CentOS 8–9 or similar, first add the GBIF package repository and install the IPT package:

```shell
yum install yum-utils
yum-config-manager --add-repo https://packages.gbif.org/gbif.repo
yum install ipt
```

Optionally, edit `/etc/sysconfig/ipt` to change the default data directory and port.  Finally:

```shell
systemctl enable ipt
systemctl start ipt
```

The IPT starts up on port 8080 (unless this was changed above).  Initial logs are visible with `journalctl -u ipt`, but are then logged in the data directory.  Make sure to **back up the IPT data directory**, which is `/var/lib/ipt` by default.

Successful installation of the IPT packages will make the IPT accessible through a web browser at a URL determined by the server’s name and port (e.g., http://server.example.org:8080). If the installation was successful, the initial IPT setup page will appear in a web browser using the IPT’s URL.

Then continue to [Opening the IPT to the Internet](#opening-the-ipt-to-the-internet).

### APT (Debian, Ubuntu etc)

Please refer to ["Debian packaging"](https://github.com/gbif/ipt/pull/1470) on GitHub.  This is a contribution from GBIF Spain, and not yet supported by the IPT developers.

Then continue to [Opening the IPT to the Internet](#opening-the-ipt-to-the-internet).

## Installation within a servlet container

Installing the IPT within a servlet container consists of deploying the IPT `.war` file in a servlet container such as Tomcat.

This section explains how to install different types of servlet containers on your server, and how to deploy the IPT within them.

It isn’t necessary to use an reverse proxy, but in case you do, the following section explains how to configure an Apache HTTPD virtual host declaration for the IPT.

The most common servlet containers used to deploy the IPT are Tomcat, Jetty and Wildfly.  The servlet container must support Servlet Specification 4.0 or later.

### Tomcat

The IPT has been tested and works well with recent releases of Tomcat 9.  Tomcat 10 and later versions are currently not supported.  The minimum supported version is Tomcat 8, but this is likely to change as it is no longer supported by Apache or leading Linux distributions. The Apache Tomcat documentation can be found on https://tomcat.apache.org/.

1. Install Tomcat — see our guide for [installing Tomcat on Linux](tomcat-installation-linux.adoc) or refer to the [Tomcat documentation](https://tomcat.apache.org/).
2. Configure the IPT data directory within Tomcat

   **💡 TIP**\
   This step is optional, but is recommended to improve security and simplify the upgrade procedure.

   Locate the Tomcat configuration directory (usually `/etc/tomcat` or `/etc/tomcat9` on Linux, `C:\Program Files\Apache Software Foundation\Tomcat X.Y\conf` on Windows), and create a file `Catalina/localhost/ipt.xml` (described in the [Tomcat documentation "Defining a context"](https://tomcat.apache.org/tomcat-9.0-doc/config/context.html#Defining_a_context)).   For example, on a typical CentOS Linux installation, the file would be `/etc/tomcat/Catalina/localhost/ipt.xml`. The file should be readable by the Tomcat process.

   Define the `IPT_DATA_DIR` parameter within the file — copy and paste the text here, since the case of the letters is important:

   ```xml
   <Context>
     <Parameter name="IPT_DATA_DIR" value="/srv/ipt"/>
   </Context>
   ```

   Ensure the Tomcat server either has permission to create this directory, or create it and then grant read and write permission. See [this FAQ entry](faq.adoc#i-get-the-following-error-the-data-directory-directory-is-not-writable-what-should-i-do) if you have errors about write permissions on the data directory.

   <dl><dt><strong>📌 NOTE</strong></dt><dd>

   If this step is not done, the IPT will prompt for a data directory when it is first run.  The location will be stored in a file called `datadir.location` the IPT’s base installation directory, e.g. `/var/lib/tomcat/webapps/ipt/WEB-INF/datadir.location`.

   If the data directory location needs to be changed, remove/edit this file and restart Tomcat.
   </dd></dl>
3. Deploy the IPT

   Download the latest WAR release of the IPT from the [releases page](releases.adoc) and rename it to `ipt.war` (or similar, matching `ipt.xml` from step 2 if used). Copy the `ipt.war` file to the Tomcat webapps folder, and then start Tomcat if it is not already running.

Successful deployment of the IPT within a servlet container will make the IPT accessible through a web browser at a URL determined by the servlet’s name and port, followed by /ipt (e.g., http://server.example.org:8080/ipt). If the installation was successful, the initial IPT setup page will appear in a web browser using the IPT’s URL.

Then continue to [Opening the IPT to the Internet](#opening-the-ipt-to-the-internet).

If the installation doesn’t start please check the `catalina.out` logfile, and refer to the [FAQ](faq.adoc) for help.

The following screencast also explains how to install the IPT using Tomcat, assuming Tomcat has already been installed.

video::116142276[vimeo,width=100%]

<dl><dt><strong>💡 TIP</strong></dt><dd>

Multiple IPTs can be installed on the same server with a small variation to this process.  Rather than (or in addition to) using `ipt.xml` and `ipt.war`, use different names and change the files accordingly: on [cloud.gbif.org](https://cloud.gbif.org/) we have `africa.xml` and `africa.war`, `bid.xml` and `bid.war` etc.

Different IPT versions may be installed side-by-side, though we always recommend always using the latest version.

_Ensure each IPT is configured to use its own data directory!_
</dd></dl>

### Jetty

_As a very rough guide, on CentOS 7, to run a single instance of the IPT:_

```shell
yum install jetty-runner
java -jar /usr/share/java/jetty/jetty-runner.jar --port 8080 ipt.war
```

Then continue to [Opening the IPT to the Internet](#opening-the-ipt-to-the-internet).

## Installation using Docker

GBIF maintain a Docker image, published to the [Docker Hub](https://hub.docker.com/r/gbif/ipt/).  The image builds upon the Docker community Tomcat 9 / OpenJDK 17 image.  Tomcat is exposed on port 8080 and the IPT runs as the ROOT application.

To run a new Docker container, startup Tomcat and expose the Tomcat port run like this:

```shell
docker run --detach --volume /full/path/to/data-directory:/srv/ipt --publish 8080:8080 gbif/ipt
```

You can then access the setup screen of the IPT on port 8080.

If you need to override the data directory, this can be done with `-e IPT_DATA_DIR=/path/within/container`.

If you need to find the IP address of your "default" Docker machine use `docker-machine ip default`.

Run a specific version from [those available](https://hub.docker.com/r/gbif/ipt/tags) by using `gbif/ipt:version` rather than `gbif/ipt`.

## Opening the IPT to the Internet

You will probably need to work with your system or network administrator for the IPT to be available on the Internet.

You will need a DNS name for the server (<q>ipt.example.org</q>) and the firewall to allow access.

Many people use Apache HTTPD as a reverse proxy, often to provide HTTPS access or to allow sharing other websites on the same server.

The configuration used by `ipt.gbif.org` is shown here as an example.  It uses Apache HTTPD, with the `mod_proxy` module installed. The paths [`/media`](https://ipt.gbif.org/media/) and [`/icons`](https://ipt.gbif.org/icons/) are excluded from being passed to the IPT, to allow hosting static image files (such as occurrence images) on the same server.  Requests to http://ipt.gbif.org/ are redirected to the secure https://ipt.gbif.org/.

```apache
```

Nginx can also be used as a reverse proxy. An example configuration is below.

```nginx
```

### TLS certificate configuration

For production deployments of the IPT we recommend using a TLS certificate, so information such as logins are secured when accessing the IPT.  The procedure to set this up sometimes depends on your institution’s policies, but the free [LetsEncrypt](https://letsencrypt.org/) service is a good choice.  They [provide instructions](https://certbot.eff.org/instructions) for adding a certificate to Apache, Nginx and many other webservers running on Linux or Windows.

For a new deployment, it is best to set up the webserver with TLS first, then install and set up the IPT.  Adding a certificate to a configured IPT requires changing the public URL.  See the note on [updating the public URL](administration.adoc#public-url) in the administration section.

Verify your setup is correct using [What’s My Chain Cert?](https://whatsmychaincert.com/).  The requirements for GBIF’s servers to retrieve published data are stricter than those for normal web browsers, so ensure you receive a "has the correct chain" message from this test. (See also [this FAQ entry](faq.adoc#why-is-gbif-unable-to-access-my-ipt-over-https).)
