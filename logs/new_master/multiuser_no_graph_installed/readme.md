# Tests

# Data set 1:  new_master_lat_0*
cpuload approx 10.3%

cat new_master_lat_0*.log | python ~/sources/ecmccomgui/pyDataManip/plotCaMonitor.py 
Added PV: MASTER0:MCU-ThdLatMax
Statistics: 
[<caPVArrayLib.caPVArray object at 0x7f89cb497a10>]
MASTER0:MCU-ThdLatMax[152531] 1405.0..13323.0, mean: 1599.1751906169893, std: 286.9307221594335

# Data set 2:  new_master_lat_2*
cpuload	approx 10.3%

cat new_master_lat_2* | python ~/sources/ecmccomgui/pyDataManip/plotCaMonitor.py 
Added PV: MASTER0:MCU-ThdLatMax
Statistics: 
[<caPVArrayLib.caPVArray object at 0x7fdd6214b710>]
MASTER0:MCU-ThdLatMax[150380] 1570.0..13342.0, mean: 1861.00745444873, std: 216.05368835958538

