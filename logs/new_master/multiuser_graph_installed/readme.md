# Test

Multiuser.target with graphics installed (never been running in graphical.target)

## Data set 1: new_master_lat_0*

CPU load 10.6%
cat new_master_lat_0* | python ~/sources/ecmccomgui/pyDataManip/plotCaMonitor.py 
Added PV: MASTER0:MCU-ThdLatMax
Statistics: 
[<caPVArrayLib.caPVArray object at 0x7fa260d1c710>]
MASTER0:MCU-ThdLatMax[151124] 1744.0..19865.0, mean: 1954.122707180858, std: 352.4035662991947

## Data set 2: new_master_lat_2*
CPU load 10.6%

cat new_master_lat_2* | python ~/sources/ecmccomgui/pyDataManip/plotCaMonitor.py 
Added PV: MASTER0:MCU-ThdLatMax

Statistics: 
[<caPVArrayLib.caPVArray object at 0x7fd003c7b0d0>]
MASTER0:MCU-ThdLatMax[150289] 1642.0..16536.0, mean: 1825.4496203980332, std: 304.60628163376776

