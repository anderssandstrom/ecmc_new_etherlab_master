# Conclusion

1. Do NOT run in graphical.target
2. Seems similar latecny performance of old and new master
3. (Seems new etherlab master results in slightly lower latency. BUT need to run test, old master and without graphics to confirm)
4. IMPORTANT!!! When using new master the ecmc IOC was not always starting OK.. needs more tests.. hmmm
5. New and old master have comparable latency performance in multi-user.target with graphics installed.

Best configuration based on the few tests:
1. New etherlab master, multi-user.target (no graphics installed)
2. New etherlab master, multi-user.target (graphics installed)
3. Old etherlab master, multi-user.target (graphics installed)
4. Old etherlab master, graphical.target
5. New etherlab master, graphical.target

# Old etherlab master

## multi-user.target (graphics installed)
Unfortenately no test was performed without graphics installed with "old" master

## multi-user.target (graphics installed)
```
MASTER0:MCU-ThdLatMax[167750] 1208.0..18971.0, mean: 1384.0919284649776, std: 371.56111662578945
MASTER0:MCU-ThdLatMax[120575] 1210.0..18475.0, mean: 1380.4042297325316, std: 365.322075616804
```

## graphical.target
```
MASTER0:MCU-ThdLatMax[57264] 1317.0..24442.0, mean: 6306.419478206203, std: 2200.4395850054384
```

# New etherlab master

## multi-user.target (no graphics installed)
```
MASTER0:MCU-ThdLatMax[152531] 1405.0..13323.0, mean: 1599.1751906169893, std: 286.9307221594335
MASTER0:MCU-ThdLatMax[150380] 1570.0..13342.0, mean: 1861.00745444873, std: 216.05368835958538
```

## multi-user.target (graphics installed)
```
MASTER0:MCU-ThdLatMax[151124] 1744.0..19865.0, mean: 1954.122707180858, std: 352.4035662991947
MASTER0:MCU-ThdLatMax[150289] 1642.0..16536.0, mean: 1825.4496203980332, std: 304.60628163376776
```

## graphical.target
```
MASTER0:MCU-ThdLatMax[150526] 1788.0..239242.0, mean: 2079.917077448414, std: 1193.9911670245974
MASTER0:MCU-ThdLatMax[150363] 1621.0..3980030.0, mean: 1855.1615024972898, std: 10351.407038839658
```
