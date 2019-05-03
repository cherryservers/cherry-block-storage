# cherry-elastic-storage

----
## Quick overview
This script helps in attaching or detaching Cherry elastic storage volume to desired server. Use ir at your own risk and always have a backup!

# Supported distributions
* CentOS 6, 7
* Ubuntu 14, 16, 18
* Debian 8, 9

# Features
* Attach elastic storage block device
* Detach elastic storage block device

## Installation

```
git clone git@github.com:cherryservers/cherry-elastic-storage.git
cp ./cherry-elastic-storage /usr/local/bin/
chmod +x /usr/local/bin/cherry-elastic-storage
```

## Usage

** Attach a volume **
1. Create a volume under the Storage tab in CherryServers.com portal.
2. Click on a volume configuration button ant click on Attach menu.
3. Select desired server to attach a volume.
4. Execute cherry-elastic-storage from the server you with volume to be attached.
5. Partition block device.
6. Make file system on block device.
7. Mount the block device on desired mount point on your system.

Example:

```
vlan_id="ZZZZ"
vlan_ip="xxx.xxx.xxx.xxx" # your VLAN private IP, assigned to your server
portal_ip="yyy.yyy.yyy.yyy" # portal IP address
initiator="qn.2019-03.com.cherryservers:initiator-XXXXXXX-YYYYYYY" # initiator name provided for your server

cherry-block-storage -v $vlan_id -z $vlan_ip -d $portal_ip -i $initiator -e
```

** Detach a volume **

1. Unmount a block device from mount point.
2. Execute cherry-elastic-storage from the server you with volume to be detached.
3. Detach a volume from CherryServers client portal

Example:

```
vlan_ip="xxx.xxx.xxx.xxx" # your VLAN private IP, assigned to your server
portal_ip="yyy.yyy.yyy.yyy" # portal IP address

rsync -a -e ssh cherry-block-storage root@$ip:/root/ && ssh root@$ip ./cherry-block-storage -z $vlan_ip -d $portal_ip -q
```