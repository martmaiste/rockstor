## [MiniDLNA](https://github.com/azatoth/minidlna) Rock-On definitions for [Rockstor](https://rockstor.com)

## Installation

Log in to your Rockstor server shell and create the directory for custom Rock-Ons.
```
mkdir /opt/rockstor/rockons-metastore
```

Download the MiniDLNA definition:
```
curl https://raw.githubusercontent.com/martmaiste/rockstor/master/nextcloud/minidlna.json -o /opt/rockstor/rockons-metastore/minidlna.json
```

Go to Rock-Ons menu and click the Update button. Find the Nextcloud Rock-On and click Install.

Select the share where the media files are located.

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


## Credits

[source](https://forum.rockstor.com/t/trouble-with-my-own-rockons/2134)
