# ecmc_new_etherlab_master
Test etherlab master with patches:
https://github.com/paulscherrerinstitute/ethercat

Commit: b3084de2050d46e671af2fca70855443421d022d

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

## Installation process

Copy https://github.com/paulscherrerinstitute/ethercat into etherlabmaster-code dir of https://github.com/icshwi/etherlabmaster

```
git clone https://github.com/icshwi/etherlabmaster
$cd etherlabmaster
$make init

  210  2022-05-19 13:42:40 ls
  211  2022-05-19 13:42:54 mv etherlabmaster-code/ etherlabmaster-code_hg/
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


# Needed to copy /etc/ethercat.conf from other system to this and change mac then

$sudo systemctl stop ethercat
$sudo systemctl start ethercat

make install in etherlabmaster:
----------------------------------------------------------------------
Libraries have been installed in:
   /opt/etherlab/lib

```

## Ensure correct version

```
$ modinfo ec_master
filename:       /lib/modules/3.10.0-1062.12.1.rt56.1042.el7.x86_64/extra/ec_master.ko.xz
version:        1.5.2 unknown
license:        GPL
description:    EtherCAT master driver module
author:         Florian Pose <fp@igh-essen.com>
retpoline:      Y
rhelversion:    7.7
srcversion:     F0FBDB65F41AE81D20BE1FD
depends:        
vermagic:       3.10.0-1062.12.1.rt56.1042.el7.x86_64 SMP preempt mod_unload modversions 
parm:           main_devices:MAC addresses of main devices (array of charp)
parm:           backup_devices:MAC addresses of backup devices (array of charp)
parm:           debug_level:Debug level (uint)
parm:           pcap_size:Pcap buffer size (ulong)

# New master was installed 19/5 so seems ok:
$ ls -la /lib/modules/3.10.0-1062.12.1.rt56.1042.el7.x86_64/extra/ec_master.ko.xz
-rw-r--r--. 1 root root 107700 May 19 13:47 /lib/modules/3.10.0-1062.12.1.rt56.1042.el7.x86_64/extra/ec_master.ko.xz


$ modinfo ec_generic
filename:       /lib/modules/3.10.0-1062.12.1.rt56.1042.el7.x86_64/extra/ec_generic.ko.xz
version:        1.5.2 unknown
license:        GPL
description:    EtherCAT master generic Ethernet device module
author:         Florian Pose <fp@igh-essen.com>
retpoline:      Y
rhelversion:    7.7
srcversion:     1AE486D6201500C92B67C63
depends:        ec_master
vermagic:       3.10.0-1062.12.1.rt56.1042.el7.x86_64 SMP preempt mod_unload modversions 

# New master was installed 19/5 so seems ok:
$ ls -la  /lib/modules/3.10.0-1062.12.1.rt56.1042.el7.x86_64/extra/ec_generic.ko.xz
-rw-r--r--. 1 root root 3184 May 19 13:47 /lib/modules/3.10.0-1062.12.1.rt56.1042.el7.x86_64/extra/ec_generic.ko.xz
```

Not sure why version is "unkown"?!!?



## OTHER SYSTEM OLD MASTER FOR COMPARISON

```
$ ethercat version
IgH EtherCAT master 1.5.2 334c34cfd2e5+

$ modinfo ec_master
filename:       /lib/modules/3.10.0-1062.12.1.rt56.1042.el7.x86_64/extra/ec_master.ko.xz
version:        1.5.2 unknown
license:        GPL
description:    EtherCAT master driver module
author:         Florian Pose <fp@igh-essen.com>
retpoline:      Y
rhelversion:    7.7
srcversion:     28E1AC457BCCF9056582029
depends:        
vermagic:       3.10.0-1062.12.1.rt56.1042.el7.x86_64 SMP preempt mod_unload modversions 
parm:           main_devices:MAC addresses of main devices (array of charp)
parm:           backup_devices:MAC addresses of backup devices (array of charp)
parm:           debug_level:Debug level (uint)

$ modinfo ec_generic
filename:       /lib/modules/3.10.0-1062.12.1.rt56.1042.el7.x86_64/extra/ec_generic.ko.xz
version:        1.5.2 unknown
license:        GPL
description:    EtherCAT master generic Ethernet device module
author:         Florian Pose <fp@igh-essen.com>
retpoline:      Y
rhelversion:    7.7
srcversion:     1AE486D6201500C92B67C63
depends:        ec_master
vermagic:       3.10.0-1062.12.1.rt56.1042.el7.x86_64 SMP preempt mod_unload modversions 
```

