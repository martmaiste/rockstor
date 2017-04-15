## [Nextcloud](https://nextcloud.com) Rock-Ons definitions for Rockstor

## Installation

Install [Nextcloud](https://nextcloud.com/)

Change the Rockstor GUI port from 443 to 1443 to free the default SSL port for Nextcloud.
On the Rockstor GUI go to System -> Services, click the wrench icon next to Rockstor service and enter the new port (1443 for example).

Create shares for nextcloud: nextcloud-config, nextcloud-db, nextcloud-apps, nextcloud-data also a share for rock-ons.

Log in to your Rockstor server shell and create the directory for custom Rock-Ons.
Then download the Nextcloud definition:
```
mkdir /opt/rockstor/rockons-metastore
curl https://raw.githubusercontent.com/martmaiste/rockstor/master/nextcloud/nextcloud.json -o /opt/rockstor/rockons-metastore/nextcloud.json
```

On the Rockstor GUI go to Rock-Ons menu and activate the Rock-Ons service. Select the rock-ons share where the docker images will be kept.

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
