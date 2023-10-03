# oracle-java8-installer
Oracle Java 8 packages for Ubuntu (8u381) - The Oracle JDK License has changed for releases starting April 16, 2019.
Please note that Java 8 reached its end of public updates and Oracle will not release any more updates after January 2019. For details please see https://www.oracle.com/technetwork/java/java-se-support-roadmap.html

Introduction
------------

Oracle Java 8 packages for Ubuntu.

Supported Ubuntu version
-------------------------

So far packages were tested on following Ubuntu version:

- bionic amd64
- focal amd64

Usage
-----

To build the packages:

- sudo apt install -y build-essential debhelper java-common
- git clone https://github.com/keshwarsingh/oracle-java8-installer.
- cd oracle-java8-installer
- download jdk-8u381-linux-x64.tar.gz and jce_policy-8.zip
- Link JDK: https://www.oracle.com/java/technologies/downloads/
- Link JCE: https://www.oracle.com/java/technologies/javase-jce8-downloads.html
- dpkg-buildpackage -uc -us
- install any missing packages that dpkg-buildpackage complains about
- sudo apt-get install ./oracle-xxx.deb ./oracle-xxx.deb ./oracle-xxx.deb
