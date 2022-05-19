# ecmc_new_etherlab_master
Test etherlab master with patches

## Start conditions

CS-Entry install (rt patch and etherlab):
https://csentry.esss.lu.se/network/hosts/view/mcag-dev-asm-04


```
$ethercat version
IgH EtherCAT master 1.5.2 334c34cfd2e5+

# and this is this version
changeset:   2303:334c34cfd2e5
branch:      stable-1.5
tag:         tip
user:        Florian Pose <fp@igh.de>
date:        Thu Sep 03 12:53:53 2020 +0200
summary:     Improved debugging and behavior on sick SII contents.

```

## Instalaltion process
Copy https://github.com/paulscherrerinstitute/ethercat into etherlabmaster-code dir of https://github.com/icshwi/etherlabmaster

```
git clone https://github.com/icshwi/etherlabmaster
$cd etherlabmaster
$make init

  210  2022-05-19 13:42:40 ls
  211  2022-05-19 13:42:54 mv etherlabmaster-code/ etherlabmaster-code_bcak/
  212  2022-05-19 13:43:21 cp -r ../ethercat etherlabmaster-code
  213  2022-05-19 13:43:23 ls
  214  2022-05-19 13:43:30 make build
  215  2022-05-19 13:45:27 make showopts
  216  2022-05-19 13:46:11 make install
  217  2022-05-19 13:46:47 make dkms_add
  218  2022-05-19 13:47:04 make dkms_build
  219  2022-05-19 13:47:40 make dkms_install
  220  2022-05-19 13:48:48 ip a
  221  2022-05-19 13:49:11 echo "ETHERCAT_MASTER0=eno1" > ethercatmaster.local
  222  2022-05-19 13:49:40 make setup
  223  2022-05-19 13:49:55 etehrcat version
  224  2022-05-19 13:49:59 ethercat version
  225  2022-05-19 13:50:13 history

```


## After installation

```
$ethercat version
IgH EtherCAT master 1.5.2 unknown


# Needed to copy /etc/ethercat.conf from other system to this and chaneg mac then
$sudo systemctl stop ethercat
$sudo systemctl start ethercat
```

make install in etherlabmaster:
----------------------------------------------------------------------
Libraries have been installed in:
   /opt/etherlab/lib


