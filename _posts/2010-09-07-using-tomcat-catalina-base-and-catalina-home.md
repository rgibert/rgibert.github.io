---
title: Using Tomcat’s CATALINA_BASE & CATALINA_HOME for multiple instances
categories: tomcat code java
---

Tomcat supports having multiple instances from a single installation by using the CATALINA_BASE & CATALINA_HOME directories. CATALINA_BASE is the installation root, while CATALINA_HOME is the instance root. Using these two variables and a few symbolic links it’s easy to support quick & easy changes between patch levels (and even major revisions) of Tomcat without having to re-install & re-configure application/deployment level changes.

Assuming we unpack the default Apache Tomcat 8 tarball (latest version at time of this is 8.0.24) at /usr/local/share/apache-tomcat-8.0.24 (we’ll reference this as ${TOM_BASE} from now on) we can set things up to support numerous Tomcat 8 instances from this single installation as follows.

For this case we’ll assume we’re installing 2 instances at ~/tomcat/instance0 and ~/tomcat/instance1.

First you need to create the directories for the instances and some required instance specific directories:

~~~
for DIR in ~/tomcat/instance0 ~/tomcat/instance1; do
    mkdir -p \
        ${DIR}/bin \
        ${DIR}/conf \
        ${DIR}/lib \
        ${DIR}/logs \
        ${DIR}/temp \
        ${DIR}/webapps \
        ${DIR}/work
done
~~~

Each instance needs it’s own copy of conf/server.xml:

~~~
cp ${TOM_BASE}/conf/server.xml ~/tomcat/instance0/conf/server.xml
cp ${TOM_BASE}/conf/server.xml ~/tomcat/instance1/conf/server.xml
~~~

The following files are also needed for each instance, but they can be symbolic links as they don’t need to vary between instances (you could also copy them instead of symbolic linking them if you want to support different settings like log levels):

~~~
for DIR in ~/tomcat/instance0 ~/tomcat/instance1; do
    for FILE in \
        bin/tomcat-juli.jar \
        bin/catalina.sh \
        bin/daemon.sh \
        bin/digest.sh \
        bin/setclasspath.sh \
        bin/shutdown.sh \
        bin/startup.sh \
        bin/tool-wrapper.sh \
        bin/version.sh \
        conf/catalina.properties \
        conf/logging.properties \
        conf/web.xml
    do
        ln -sf ${TOM_BASE}/${FILE} ~/tomcat/instance0/${FILE}
        ln -sf ${TOM_BASE}/${FILE} ~/tomcat/instance1/${FILE}
    done
done
~~~

For each instance to be able to run in parallel you’ll need to edit their respective conf/server.xml files to ensure that the ports from one instance don’t conflict with any other instances.

Finally you need to set the CATALINA_BASE & CATALINA_HOME environment variables for each instance for this setup to work properly. Tomcat will automatically source bin/setenv.sh on start up if it’s present, so we’ll use that to set these variables properly.

~/tomcat/instance0/bin/setenv.sh:
~~~
CATALINA_BASE=/usr/local/share/apache-tomcat-8.0.24
CATALINA_HOME=${HOME}/tomcat/instance0
~~~

~/tomcat/instance1/bin/setenv.sh:
~~~
CATALINA_BASE=/usr/local/share/apache-tomcat-8.0.24
CATALINA_HOME=${HOME}/tomcat/instance1
~~~

You’re now ready to run both instances in parallel by running their specific startup.sh:

~~~
~/tomcat/instance0/bin/startup.sh
~/tomcat/instance1/bin/startup.sh
~~~

When the time comes to upgrade Apache Tomcat to the next version you can now just unpack the tarball to a shared directory, update the instances’s bin/setenv.sh that you want to upgrade, and re-run the symbolic link loop above to re-link everything to the new shared install.

One note of importance, conf/server.xml should remain the same between patch levels but can be quite different between major versions (8.x.x to 9.x.x), so I suggest overwriting server.xml with the fresh one and re-applying your changes when doing major version changes of Apache Tomcat.

Scripted versions of the above setup are at the following download links.

- [Tomcat 6](https://github.com/rgibert/apache-tomcat/tree/tomcat6){:target="blank"}
- [Tomcat 7](https://github.com/rgibert/apache-tomcat/tree/tomcat7){:target="blank"}
- [Tomcat 8](https://github.com/rgibert/apache-tomcat/tree/tomcat8){:target="blank"}
