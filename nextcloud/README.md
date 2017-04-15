## [Nextcloud](https://nextcloud.com) Rock-On definitions for [Rockstor](https://rockstor.com)

## About

This custom Rock-On simplyfies installation of Nextcloud software on to the Rockstor server.

It consists of two separate Docker images:

Custom Nextcloud Docker using php-fpm and Nginx reverse proxy with SSL and Let's Encrypt support.

MariaDB database backend for storing the metadata. A default database, user and password is created at the installation time and the same info is used for automatically configuring the Nextcloud container.

## Installation

Install [Rockstor](http://rockstor.com/download.html), create an user account and storage pool etc.

Change the Rockstor GUI port from 443 to 1443 to free the default SSL port for Nextcloud.

On the Rockstor GUI go to System -> Services, click the wrench icon next to Rockstor service and enter the new port (1443 for example).

Create shares for Nextcloud: nextcloud-config, nextcloud-db, nextcloud-apps, nextcloud-data also a share for rock-ons.

On the Rockstor GUI go to Rock-Ons menu and activate the Rock-Ons service.
Select the rock-ons share where the docker images will be kept.

Log in to your Rockstor server shell and create the directory for custom Rock-Ons.
```
mkdir /opt/rockstor/rockons-metastore
```

Download the Nextcloud definition:
```
curl https://raw.githubusercontent.com/martmaiste/rockstor/master/nextcloud/nextcloud.json -o /opt/rockstor/rockons-metastore/nextcloud.json
```

Go to Rock-Ons menu and click the Update button. Find the Nextcloud Rock-On and click Install.

Select the correct shares and make sure that SSL port is 443.

Optionally you may want to open two shell windows and observe the installation process.
In one shell window type:
```
tail -f /opt/rockstor/var/log/rockstor.log
```
And in second window:
```
journalctl -f
```

The installation may take few minutes, be patient.
