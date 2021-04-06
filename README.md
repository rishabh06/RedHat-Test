# OwnCloud Quickstart Guide
This guide provides information on ownCloud server installation, setting up the server, and accessing your OwnCloud server through a OwnCloud client.
The guide includes the following topics:

- [Installation Guide](https://github.com/rishabh06/RedHat-Test/wiki/Installation-Guide)



# Installation Guide

You can install the OwnCloud server using the instructions given in the following topics

- [Manual Installation](#MANINST)
- [Installing With Docker](#DOCKINST)
- [Linux Package Manager](#LPMINST)


## <a name="MANINST"></a>Manual Installation
`Before you begin check the prerequisites for the ownCloud server on` [Manual Installation Prerequisites] (https://doc.owncloud.com/server/admin_manual/installation/manual_installation/manual_installation_prerequisites.html) and [Supported Databases](https://doc.owncloud.com/server/admin_manual/installation/manual_installation/manual_installation_db.html)

To install the ownCloud server perform the following steps:
1. Select the desired zip or tar.bz2 archive of the source package from [Server Packages](https://owncloud.com/download-server/#instructions-server), and download the file.
  ```shell
  wget https://download.owncloud.org/community/owncloud-complete-yyyymmdd.tar.bz2
  ```
  Replace "owncloud-complete-yyyymmdd.tar.bz2" in the above command with the selected package name.
2. Download the corresponding MD5 or SHA256 checksum file and verify the file integrity.
  ```shell
  wget https://download.owncloud.org/community/owncloud-complete-yyyymmdd.tar.bz2.md5

  sudo md5sum -c owncloud-complete-yyyymmdd.tar.bz2.md5 < owncloud-complete-yyyymmdd.tar.bz2
  ```
  ```shell
  wget https://download.owncloud.org/community/owncloud-complete-yyyymmdd.tar.bz2.sha256

  sudo sha256sum -c owncloud-complete-yyyymmdd.tar.bz2.sha256 < owncloud-complete-yyyymmdd.tar.bz2
  ```
3. You can also verify the PGP signature:
  ```shell
  wget https://download.owncloud.org/community/owncloud-complete-yyyymmdd.tar.bz2.asc

  gpg --verify owncloud-complete-yyyymmdd.tar.bz2.asc owncloud-complete-yyyymmdd.tar.bz2
  ```
4. Install the ownCloud server using one of the following methods:
   
 -  Script Guided Installation: ownCloud has scripts that assist you to easily install or upgrade ownCloud or manage ownership and permissions. 
Using the Script Guided Installation, you can handle many useful installation and update options automatically. See [Scripts for Script Guided Installation](https://doc.owncloud.com/server/admin_manual/installation/manual_installation/script_guided_install.html)

-  Command Line Guided Installation: You can use this method if you want to do the basic setup without any changes or physical installation options. Consider using the Script Guided Installation if you plan improving your setup from step one.
   To install ownCloud using command line, unpack the archive and copy the `ownCloud` directory that contains all the unpacked file to the Apache document root
   ```shell
   tar -xjf owncloud-complete-yyyymmdd.tar.bz2
   
   cp -r owncloud /var/www
   ```
   In the above example /var/www is considered as the apache document root.
   Post physical installation, set the correct ownership and permissions upfront. To do so, it is suggested use the scripts from the Script Guided Installation.
   
5. Finalize the installation using one of the following methods:
   - 


## <a name="DOCKINST"></a>Installing with Docker
See [Installing With Docker](https://doc.owncloud.com/server/admin_manual/installation/docker/) for details.

## <a name="LPMINST"></a>Installing with Linux Package Manager

See [Linux Package Manager](https://doc.owncloud.com/server/admin_manual/installation/linux_packetmanager_install.html) for details.
