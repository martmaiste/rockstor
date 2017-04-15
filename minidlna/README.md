## [MiniDLNA](https://github.com/azatoth/minidlna) Rock-On definitions for [Rockstor](https://rockstor.com)

## Installation

Create a share for minidlna config and for media files if it does not exist yet.

Log in to your Rockstor server shell and create the directory for custom Rock-Ons.
```
mkdir /opt/rockstor/rockons-metastore
```

Download the MiniDLNA definition:
```
curl https://raw.githubusercontent.com/martmaiste/rockstor/master/minidlna/minidlna.json -o /opt/rockstor/rockons-metastore/minidlna.json
```

Go to Rock-Ons menu and click the Update button. Find the MiniDLNA Rock-On and click Install.

Select the config and media share.

Enter the UID and GID (1000 and 1000 for default user).

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
