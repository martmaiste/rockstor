# Nextcloud Rock-On definitions for [Rockstor](https://rockstor.com)

## About

This custom Rock-On simplyfies installation of Nextcloud software on to the Rockstor server.

It consists of two separate Docker images:

  - Custom [personal public cloud server Docker container](https://hub.docker.com/r/martmaiste/nextcloud/) using [Nextcloud](https://nextcloud.com) cloud server, [PHP-FPM](https://php-fpm.org/) FastCGI Process Manager and [Nginx](https://nginx.org/en/) reverse proxy with SSL and [Let's Encrypt](https://letsencrypt.org/) certificate authority support.

  - [MariaDB](https://hub.docker.com/_/mariadb/) database backend for storing the metadata. A default database, user and password is created at the installation time and the same info is used for automatically configuring the Nextcloud container.

## Installation procedure

### Installing the Rock-On

1. Install [Rockstor](http://rockstor.com/download.html), create an user account and storage pool etc.

1. Change the Rockstor GUI port from 443 to 1443 to free the default SSL port for Nextcloud:

   - On the Rockstor GUI go to _System -> Services_, click the wrench icon next to Rockstor service and enter the new port (1443 for example).

1. Create required shares:

   - nextcloud-config
   - nextcloud-db
   - nextcloud-apps
   - nextcloud-data
   - also a share for rock-ons

1. On the Rockstor GUI go to Rock-Ons menu and activate the Rock-Ons service.
1. Select the rock-ons share where the docker images will be kept.
1. Log in as root to your Rockstor server shell and:
   - Create the directory for custom Rock-Ons:
   ``` console
   # mkdir /opt/rockstor/rockons-metastore
   ```
   - Download the latest Nextcloud Rock-On definition:
   ``` console
   # curl https://raw.githubusercontent.com/martmaiste/rockstor/master/nextcloud/nextcloud.json -o /opt/rockstor/rockons-metastore/nextcloud.json
   ```
1. Go back to Rock-Ons menu and click the Update button.
1. Find the Nextcloud Rock-On and click Install.
1. From the Nextcloud Rock-On dialog, select the correct shares and make sure that HTTP port is 80 and HTTPS port is 443 (otherwise the Let's Encrypt challenge will not pass).
1. Optionally, you may want to open two shell windows as root and observe the installation process:
   - In one shell window type:
   ``` console
   # sudo tail -f /opt/rockstor/var/log/rockstor.log
   ```
   - And in second window:
   ``` console
   # journalctl -f
   ```
   
> The installation may take few minutes, please be patient!

### CA certificate setup

1. On the server shell as root, enter the Nextcloud's Docker container shell with:
   ``` console
   # docker exec -ti nextcloud bash
   ```
1. Next, config Let's Encrypt:
   - Start the setup:
   ``` console
   # DOMAIN=your.domain.com EMAIL=your@domain.com letsencrypt-setup
   # exit
   ```
   Where the `DOMAIN` variable keeps your public server name and `EMAIL` variable keeps your e-mail address.
   
## CA certificate renew
Let's Encrypt system will send e-mail notices when certificate expires. To manually renew it, open one shell as root and type:
   ``` console
   # docker exec -ti nextcloud letsencrypt-renew
   # exit
   ```
   
That's all!  :)
