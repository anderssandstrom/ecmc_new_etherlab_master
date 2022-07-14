# Test

systemctl get-default
graphical.target


## Data set 1:

cpu load: 10.6%

cat new_master_lat_0* | python ~/sources/ecmccomgui/pyDataManip/plotCaMonitor.py 
Added PV: MASTER0:MCU-ThdLatMax
Statistics: 
[<caPVArrayLib.caPVArray object at 0x7fc537632310>]
MASTER0:MCU-ThdLatMax[150526] 1788.0..239242.0, mean: 2079.917077448414, std: 1193.9911670245974


## Data set 2:

CPU load 10.6%

Hard to get IOC running had to restart several times?!!?

cat new_master_lat_2* | python ~/sources/ecmccomgui/pyDataManip/plotCaMonitor.py 
Added PV: MASTER0:MCU-ThdLatMax
Statistics: 
[<caPVArrayLib.caPVArray object at 0x7f49e30aa9d0>]
MASTER0:MCU-ThdLatMax[150363] 1621.0..3980030.0, mean: 1855.1615024972898, std: 10351.407038839658
