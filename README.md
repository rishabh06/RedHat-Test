# ownCloud Quickstart Guide
This guide provides information on ownCloud server installation, setting up the server, and accessing your OwnCloud server through a OwnCloud client.
The guide includes the following topics:

- [Installation Guide](#INSTGUIDE)
- [Configuring ownCloud Server](#CONFGUIDE)
- Creating a User(#CRUSER)



# <a name="INSTGUIDE"></a>Installation Guide

You can install the OwnCloud server using the instructions given in the following topics

- [Manual Installation](#MANINST)
- [Installing With Docker](#DOCKINST)
- [Linux Package Manager](#LPMINST)


## <a name="MANINST"></a>Manual Installation
Before you begin check the prerequisites for the ownCloud server on [Manual Installation Prerequisites](https://doc.owncloud.com/server/admin_manual/installation/manual_installation/manual_installation_prerequisites.html) and [Supported Databases](https://doc.owncloud.com/server/admin_manual/installation/manual_installation/manual_installation_db.html)

To install ownCloud server perform the following steps:
1. Select the desired zip or tar.bz2 archive of the source package from [Server Packages](https://owncloud.com/download-server/#instructions-server), and download the file.
    ```shell
    $ wget https://download.owncloud.org/community/owncloud-complete-yyyymmdd.tar.bz2
    ```
    Replace "owncloud-complete-yyyymmdd.tar.bz2" in the above command with the selected package name.
2. Download the corresponding MD5 or SHA256 checksum file and verify the file's integrity.
    ```shell
    $ wget https://download.owncloud.org/community/owncloud-complete-yyyymmdd.tar.bz2.md5

    $ sudo md5sum -c owncloud-complete-yyyymmdd.tar.bz2.md5 < owncloud-complete-yyyymmdd.tar.bz2
    ```
    ```shell
    $ wget https://download.owncloud.org/community/owncloud-complete-yyyymmdd.tar.bz2.sha256

    $ sudo sha256sum -c owncloud-complete-yyyymmdd.tar.bz2.sha256 < owncloud-complete-yyyymmdd.tar.bz2
    ```
3. You can also verify the PGP signature:
    ```shell
    $ wget https://download.owncloud.org/community/owncloud-complete-yyyymmdd.tar.bz2.asc

    $ gpg --verify owncloud-complete-yyyymmdd.tar.bz2.asc owncloud-complete-yyyymmdd.tar.bz2
    ```
4. Install the ownCloud server using one of the following methods:
   
   -  **Script Guided Installation**: ownCloud has scripts that assist you to easily install or upgrade ownCloud or manage ownership and permissions. 
      Using the Script Guided Installation, you can handle many useful installation and update options automatically. See [Scripts for Script Guided Installation](https://doc.owncloud.com/server/admin_manual/installation/manual_installation/script_guided_install.html)

   -  **Command Line Guided Installation**: You can use this method if you want to do the basic setup without any changes or physical installation options.                Consider using the Script Guided Installation if you plan improving your setup from step one.
      To install ownCloud using command line, unpack the archive, and copy the `ownCloud` directory that contains all the unpacked file to the Apache document root
      ```shell
      $ tar -xjf owncloud-complete-yyyymmdd.tar.bz2
   
      $ cp -r owncloud /var/www
      ```
     In the above example /var/www is considered as the apache document root.
     Post physical installation, set the correct ownership and permissions upfront. It is recommened to use the scripts from the Script Guided Installation for setting correct        ownership and permissions.
    
   
5. Finalize the installation by creating the administrator and database users and setting their passwords. Create these users by using one of the following methods:
   -  **Graphical Installation Wizard**: See [Installation Wizard](https://doc.owncloud.com/server/admin_manual/installation/installation_wizard.html) for details.
   -  **Command Line**: Run the following command with your desired parameters
      ```shell
      sudo -u www-data php occ maintenance:install \
      --database "mysql" \
      --database-name "owncloud" \
      --database-user "root"\
      --database-pass "password" \
      --admin-user "admin" \
      --admin-pass "password"
      ```
      For details on `occ`, see [Using the OCC Command](https://doc.owncloud.com/server/admin_manual/configuration/server/occ_command.html


## <a name="DOCKINST"></a>Installing with Docker
See [Installing With Docker](https://doc.owncloud.com/server/admin_manual/installation/docker/) for details.

## <a name="LPMINST"></a>Installing with Linux Package Manager

See [Linux Package Manager](https://doc.owncloud.com/server/admin_manual/installation/linux_packetmanager_install.html) for details.


# <a name="CONFGUIDE"></a>Configuring ownCloud Server
After installing ownCloud successfully, ownCloud recommends that you perform the following post installation tasks. These configurations help in improving the overall ownCloud performance and accesibility.

- [Background Jobs](#BJOBS)
- [Caching](#CACHING)
- [Trusted Domains](#TRUDOM)

## <a name="BJOBS"></a>Background Jobs
ownCloud requires some jobs to run periodically to mantain its overall performance. These are CRON jobs that can be configured to run automatically without any user interaction. See [Background Jobs](https://doc.owncloud.com/server/admin_manual/configuration/server/background_jobs_configuration.html) for details.

## <a name="CACHING"></a>Configure Caching
It is recommended to install and enable caching (PHP opcode Cache and/or Data Cache), which significantly improves performance. See [Memory Caching](https://doc.owncloud.com/server/admin_manual/configuration/server/caching_configuration.html) for details.

## <a name="TRUDOM"></a>Trusted Domains
All URLs used to access your ownCloud server must be white-listed in your config.php file, under the trusted_domains setting. Users are allowed to log into ownCloud only when they point their browsers to a URL that is listed in the trusted_domains setting.

This setting is important when changing or moving to a new domain name. You may use IP addresses and domain names. Adding the server's IP address in the configuration file enables your users to connect to the ownCloud server using the servers's IP address and port 8080.

A typical configuration may look like this:
```shell
'trusted_domains' => [
   0 => 'localhost',
   1 => 'server1.example.com',
   2 => '192.168.1.50',
],
```
The loopback address, 127.0.0.1, is automatically white-listed, so as long as you have access to the physical server you can always log in. In the event that a load-balancer is in place, there will be no issues as long as it sends the correct X-Forwarded-Host header.


For further information on improving the quality of your ownCloud installation, see the [Configuration Notes and Tips](https://doc.owncloud.com/server/admin_manual/installation/configuration_notes_and_tips.html.)


# <a name="CRUSER"></a>Creating a User
Administrators can add new uses to ownCLoud using the User management page of your ownCloud Web UI.
To create a user account:

1. Enter a Login Name and initial Password for the new user.
2. Optionally, assign Groups memberships
3. Click the Create button


![users-create](https://user-images.githubusercontent.com/22167451/113716462-40586700-9708-11eb-82ed-b76786ae3c5d.png)


Login names may contain letters (a-z, A-Z), numbers (0-9), dashes (-), underscores (_), periods (.) and at signs (@). After creating the user, you may fill in their Full Name if it is different than the login name, or leave it for the user to complete.

If you have checked Send email to new user in the control panel on the lower left sidebar, you may also enter the new user’s email address, and ownCloud will automatically send them a notification with their new login information. You may edit this email using the email template editor on your Admin page (see Email Configuration).
