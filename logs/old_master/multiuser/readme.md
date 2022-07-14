# About

Test performed with graphics installed but in multi-user-target (text mode)



# Stats data set 1: old_master_lat_0*

cat old_master_lat_0* | python ~/sources/ecmccomgui/pyDataManip/plotCaMonitor.py 
Added PV: MASTER0:MCU-ThdLatMax
Statistics: 
[<caPVArrayLib.caPVArray object at 0x7fd106f77750>]
MASTER0:MCU-ThdLatMax[167750] 1208.0..18971.0, mean: 1384.0919284649776, std: 371.56111662578945

# Stats data set 2: old_master_lat_2*

cpu load approx 8.5%

cat old_master_lat_2* | python ~/sources/ecmccomgui/pyDataManip/plotCaMonitor.py 
Added PV: MASTER0:MCU-ThdLatMax
Statistics: 
[<caPVArrayLib.caPVArray object at 0x7f3800c52a10>]
MASTER0:MCU-ThdLatMax[120575] 1210.0..18475.0, mean: 1380.4042297325316, std: 365.322075616804


