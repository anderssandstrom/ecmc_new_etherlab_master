# Latency logs

## Test setup

Both systems was tested with a setup with 54 ethercat slaves and 30 virtual axes with an EC_RATE of 1kHz

This startup file was used:
https://github.com/anderssandstrom/ecmc_multi_master_test/blob/master/master0/st.cmd

IMPORTANT: TESTS where run on different hw.

## New master
Running on an old nuc (the big version):
```
[anderssandstrom@mcag-dev-asm-04-usb ~]$ lshw
WARNING: you should run this program as super-user.
mcag-dev-asm-04-usb.cslab.esss.lu.se
    description: Computer
    width: 64 bits
    capabilities: smp vsyscall32
  *-core
       description: Motherboard
       physical id: 0
     *-memory
          description: System memory
          physical id: 0
          size: 16GiB
     *-cpu
          product: Intel(R) Core(TM) i3-4010U CPU @ 1.70GHz
          vendor: Intel Corp.
          vendor_id: GenuineIntel
          physical id: 1
          bus info: cpu@0
          version: 6.69.1
          width: 64 bits
          capabilities: fpu fpu_exception wp vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp x86-64 constant_tsc arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc aperfmperf eagerfpu pni pclmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt aes xsave avx f16c rdrand lahf_lm abm epb invpcid_single tpr_shadow vnmi flexpriority ept vpid fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms invpcid xsaveopt dtherm arat pln pts
          configuration: microcode=0
     *-pci
          description: Host bridge
          product: Haswell-ULT DRAM Controller
          vendor: Intel Corporation
          physical id: 100
          bus info: pci@0000:00:00.0
          version: 09
          width: 32 bits
          clock: 33MHz
          configuration: driver=hsw_uncore
          resources: irq:0
        *-display UNCLAIMED
             description: VGA compatible controller
             product: Haswell-ULT Integrated Graphics Controller
             vendor: Intel Corporation
             physical id: 2
             bus info: pci@0000:00:02.0
             version: 09
             width: 64 bits
             clock: 33MHz
             capabilities: vga_controller bus_master cap_list
             configuration: latency=0
             resources: memory:f7800000-f7bfffff memory:e0000000-efffffff ioport:f000(size=64)
        *-multimedia
             description: Audio device
             product: Haswell-ULT HD Audio Controller
             vendor: Intel Corporation
             physical id: 3
             bus info: pci@0000:00:03.0
             version: 09
             width: 64 bits
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: driver=snd_hda_intel latency=0
             resources: irq:16 memory:f7c30000-f7c33fff
        *-usb:0
             description: USB controller
             product: 8 Series USB xHCI HC
             vendor: Intel Corporation
             physical id: 14
             bus info: pci@0000:00:14.0
             version: 04
             width: 64 bits
             clock: 33MHz
             capabilities: xhci bus_master cap_list
             configuration: driver=xhci_hcd latency=0
             resources: irq:40 memory:f7c20000-f7c2ffff
        *-communication
             description: Communication controller
             product: 8 Series HECI #0
             vendor: Intel Corporation
             physical id: 16
             bus info: pci@0000:00:16.0
             version: 04
             width: 64 bits
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: driver=mei_me latency=0
             resources: irq:43 memory:f7c3a000-f7c3a01f
        *-network
             description: Ethernet interface
             product: Ethernet Connection I218-V
             vendor: Intel Corporation
             physical id: 19
             bus info: pci@0000:00:19.0
             logical name: eno1
             version: 04
             serial: c0:3f:d5:6a:74:92
             size: 100Mbit/s
             capacity: 1Gbit/s
             width: 32 bits
             clock: 33MHz
             capabilities: bus_master cap_list ethernet physical tp 10bt 10bt-fd 100bt 100bt-fd 1000bt-fd autonegotiation
             configuration: autonegotiation=on broadcast=yes driver=e1000e driverversion=3.2.6-k duplex=full firmware=0.6-4 latency=0 link=yes multicast=yes port=twisted pair speed=100Mbit/s
             resources: irq:42 memory:f7c00000-f7c1ffff memory:f7c38000-f7c38fff ioport:f080(size=32)
        *-usb:1
             description: USB controller
             product: 8 Series USB EHCI #1
             vendor: Intel Corporation
             physical id: 1d
             bus info: pci@0000:00:1d.0
             version: 04
             width: 32 bits
             clock: 33MHz
             capabilities: ehci bus_master cap_list
             configuration: driver=ehci-pci latency=0
             resources: irq:23 memory:f7c37000-f7c373ff
        *-isa
             description: ISA bridge
             product: 8 Series LPC Controller
             vendor: Intel Corporation
             physical id: 1f
             bus info: pci@0000:00:1f.0
             version: 04
             width: 32 bits
             clock: 33MHz
             capabilities: isa bus_master cap_list
             configuration: driver=lpc_ich latency=0
             resources: irq:0
        *-sata
             description: SATA controller
             product: 8 Series SATA Controller 1 [AHCI mode]
             vendor: Intel Corporation
             physical id: 1f.2
             bus info: pci@0000:00:1f.2
             version: 04
             width: 32 bits
             clock: 66MHz
             capabilities: sata ahci_1.0 bus_master cap_list
             configuration: driver=ahci latency=0
             resources: irq:41 ioport:f0d0(size=8) ioport:f0c0(size=4) ioport:f0b0(size=8) ioport:f0a0(size=4) ioport:f060(size=32) memory:f7c36000-f7c367ff
        *-serial
             description: SMBus
             product: 8 Series SMBus Controller
             vendor: Intel Corporation
             physical id: 1f.3
             bus info: pci@0000:00:1f.3
             version: 04
             width: 64 bits
             clock: 33MHz
             configuration: driver=i801_smbus latency=0
             resources: irq:18 memory:f7c35000-f7c350ff ioport:f040(size=32)
     *-pnp00:00
          product: PnP device PNP0c01
          physical id: 2
          capabilities: pnp
          configuration: driver=system
     *-pnp00:01
          product: PnP device PNP0c02
          physical id: 3
          capabilities: pnp
          configuration: driver=system
     *-pnp00:02
          product: PnP device PNP0b00
          physical id: 4
          capabilities: pnp
          configuration: driver=rtc_cmos
     *-pnp00:03
          product: PnP device INT3f0d
          vendor: Interphase Corporation
          physical id: 5
          capabilities: pnp
          configuration: driver=system
     *-pnp00:04
          product: PnP device PNP0c02
          physical id: 6
          capabilities: pnp
          configuration: driver=system
     *-pnp00:05
          product: PnP device PNP0c02
          physical id: 7
          capabilities: pnp
          configuration: driver=system
     *-pnp00:06
          product: PnP device PNP0c02
          physical id: 8
          capabilities: pnp
          configuration: driver=system
     *-pnp00:07
          product: PnP device PNP0c02
          physical id: 9
          capabilities: pnp
          configuration: driver=system
  *-network
       description: Ethernet interface
       physical id: 1
       bus info: usb@2:3
       logical name: enp0s20u3
       serial: ac:29:3a:da:89:2e
       size: 100Mbit/s
       capacity: 100Mbit/s
       capabilities: ethernet physical tp mii 10bt 10bt-fd 100bt 100bt-fd autonegotiation
       configuration: autonegotiation=on broadcast=yes driver=asix driverversion=22-Dec-2011 duplex=full firmware=ASIX AX88772 USB 2.0 Ethernet ip=172.30.41.20 link=yes multicast=yes port=MII speed=100Mbit/s
WARNING: output may be incomplete or inaccurate, you should run this program as super-user.
```

## Old master
Running on an newer black nuc (the big version):

```
 lshw
WARNING: you should run this program as super-user.
mcag-dev-asm-02.cslab.esss.lu.se
    description: Computer
    width: 64 bits
    capabilities: smp vsyscall32
  *-core
       description: Motherboard
       physical id: 0
     *-memory
          description: System memory
          physical id: 0
          size: 16GiB
     *-cpu
          product: Intel(R) Core(TM) i7-8650U CPU @ 1.90GHz
          vendor: Intel Corp.
          vendor_id: GenuineIntel
          physical id: 1
          bus info: cpu@0
          version: 6.142.10
          size: 1900MHz
          capacity: 2101MHz
          width: 64 bits
          capabilities: fpu fpu_exception wp vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp x86-64 constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc aperfmperf eagerfpu pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch epb invpcid_single intel_pt ssbd ibrs ibpb stibp tpr_shadow vnmi flexpriority ept vpid fsgsbase tsc_adjust bmi1 hle avx2 smep bmi2 erms invpcid rtm mpx rdseed adx smap clflushopt xsaveopt xsavec xgetbv1 dtherm ida arat pln pts hwp hwp_notify hwp_act_window hwp_epp spec_ctrl intel_stibp flush_l1d cpufreq
          configuration: microcode=0
     *-pci
          description: Host bridge
          product: Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers
          vendor: Intel Corporation
          physical id: 100
          bus info: pci@0000:00:00.0
          version: 08
          width: 32 bits
          clock: 33MHz
          configuration: driver=skl_uncore
          resources: irq:0
        *-display UNCLAIMED
             description: VGA compatible controller
             product: UHD Graphics 620
             vendor: Intel Corporation
             physical id: 2
             bus info: pci@0000:00:02.0
             version: 07
             width: 64 bits
             clock: 33MHz
             capabilities: vga_controller bus_master cap_list
             configuration: latency=0
             resources: memory:de000000-deffffff memory:c0000000-cfffffff ioport:f000(size=64)
        *-generic:0 UNCLAIMED
             description: System peripheral
             product: Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th/8th Gen Core Processor Gaussian Mixture Model
             vendor: Intel Corporation
             physical id: 8
             bus info: pci@0000:00:08.0
             version: 00
             width: 64 bits
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: latency=0
             resources: memory:df252000-df252fff
        *-usb
             description: USB controller
             product: Sunrise Point-LP USB 3.0 xHCI Controller
             vendor: Intel Corporation
             physical id: 14
             bus info: pci@0000:00:14.0
             version: 21
             width: 64 bits
             clock: 33MHz
             capabilities: xhci bus_master cap_list
             configuration: driver=xhci_hcd latency=0
             resources: irq:122 memory:df230000-df23ffff
        *-generic:1 UNCLAIMED
             description: Signal processing controller
             product: Sunrise Point-LP Thermal subsystem
             vendor: Intel Corporation
             physical id: 14.2
             bus info: pci@0000:00:14.2
             version: 21
             width: 64 bits
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: latency=0
             resources: memory:df251000-df251fff
        *-generic:2
             description: Signal processing controller
             product: Sunrise Point-LP Serial IO I2C Controller #0
             vendor: Intel Corporation
             physical id: 15
             bus info: pci@0000:00:15.0
             version: 21
             width: 64 bits
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: driver=intel-lpss latency=0
             resources: irq:16 memory:df250000-df250fff
        *-generic:3
             description: Signal processing controller
             product: Sunrise Point-LP Serial IO I2C Controller #1
             vendor: Intel Corporation
             physical id: 15.1
             bus info: pci@0000:00:15.1
             version: 21
             width: 64 bits
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: driver=intel-lpss latency=0
             resources: irq:17 memory:df24f000-df24ffff
        *-communication:0
             description: Communication controller
             product: Sunrise Point-LP CSME HECI #1
             vendor: Intel Corporation
             physical id: 16
             bus info: pci@0000:00:16.0
             version: 21
             width: 64 bits
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: driver=mei_me latency=0
             resources: irq:282 memory:df24e000-df24efff
        *-communication:1
             description: Serial controller
             product: Sunrise Point-LP Active Management Technology - SOL
             vendor: Intel Corporation
             physical id: 16.3
             bus info: pci@0000:00:16.3
             version: 21
             width: 32 bits
             clock: 66MHz
             capabilities: 16550 bus_master cap_list
             configuration: driver=serial latency=0
             resources: irq:19 ioport:f0a0(size=8) memory:df24d000-df24dfff
        *-sata
             description: SATA controller
             product: Sunrise Point-LP SATA Controller [AHCI mode]
             vendor: Intel Corporation
             physical id: 17
             bus info: pci@0000:00:17.0
             version: 21
             width: 32 bits
             clock: 66MHz
             capabilities: sata ahci_1.0 bus_master cap_list
             configuration: driver=ahci latency=0
             resources: irq:124 memory:df248000-df249fff memory:df24c000-df24c0ff ioport:f090(size=8) ioport:f080(size=4) ioport:f060(size=32) memory:df24b000-df24b7ff
        *-pci:0
             description: PCI bridge
             product: Sunrise Point-LP PCI Express Root Port #3
             vendor: Intel Corporation
             physical id: 1c
             bus info: pci@0000:00:1c.0
             version: f1
             width: 32 bits
             clock: 33MHz
             capabilities: pci normal_decode bus_master cap_list
             configuration: driver=pcieport
             resources: irq:120 memory:df100000-df1fffff
           *-network UNCLAIMED
                description: Network controller
                product: Wireless 8265 / 8275
                vendor: Intel Corporation
                physical id: 0
                bus info: pci@0000:01:00.0
                version: 78
                width: 64 bits
                clock: 33MHz
                capabilities: cap_list
                configuration: latency=0
                resources: memory:df100000-df101fff
        *-pci:1
             description: PCI bridge
             product: Sunrise Point-LP PCI Express Root Port #9
             vendor: Intel Corporation
             physical id: 1d
             bus info: pci@0000:00:1d.0
             version: f1
             width: 32 bits
             clock: 33MHz
             capabilities: pci normal_decode bus_master cap_list
             configuration: driver=pcieport
             resources: irq:121 memory:df000000-df0fffff
           *-nvme
                description: Non-Volatile memory controller
                product: NVMe SSD Controller SM981/PM981/PM983
                vendor: Samsung Electronics Co Ltd
                physical id: 0
                bus info: pci@0000:02:00.0
                version: 00
                width: 64 bits
                clock: 33MHz
                capabilities: nvme nvm_express bus_master cap_list
                configuration: driver=nvme latency=0
                resources: irq:16 memory:df000000-df003fff
        *-isa
             description: ISA bridge
             product: Sunrise Point LPC Controller/eSPI Controller
             vendor: Intel Corporation
             physical id: 1f
             bus info: pci@0000:00:1f.0
             version: 21
             width: 32 bits
             clock: 33MHz
             capabilities: isa bus_master
             configuration: latency=0
        *-memory UNCLAIMED
             description: Memory controller
             product: Sunrise Point-LP PMC
             vendor: Intel Corporation
             physical id: 1f.2
             bus info: pci@0000:00:1f.2
             version: 21
             width: 32 bits
             clock: 33MHz (30.3ns)
             capabilities: bus_master
             configuration: latency=0
             resources: memory:df244000-df247fff
        *-multimedia
             description: Audio device
             product: Sunrise Point-LP HD Audio
             vendor: Intel Corporation
             physical id: 1f.3
             bus info: pci@0000:00:1f.3
             version: 21
             width: 64 bits
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: driver=snd_hda_intel latency=32
             resources: irq:283 memory:df240000-df243fff memory:df220000-df22ffff
        *-serial
             description: SMBus
             product: Sunrise Point-LP SMBus
             vendor: Intel Corporation
             physical id: 1f.4
             bus info: pci@0000:00:1f.4
             version: 21
             width: 64 bits
             clock: 33MHz
             configuration: driver=i801_smbus latency=0
             resources: irq:16 memory:df24a000-df24a0ff ioport:f040(size=32)
        *-network
             description: Ethernet interface
             product: Ethernet Connection I219-LM
             vendor: Intel Corporation
             physical id: 1f.6
             bus info: pci@0000:00:1f.6
             logical name: eno1
             version: 21
             serial: 54:b2:03:10:b7:9c
             capacity: 1Gbit/s
             width: 32 bits
             clock: 33MHz
             capabilities: bus_master cap_list ethernet physical tp 10bt 10bt-fd 100bt 100bt-fd 1000bt-fd autonegotiation
             configuration: autonegotiation=on broadcast=yes driver=e1000e driverversion=3.2.6-k firmware=0.2-4 latency=0 link=no multicast=yes port=twisted pair
             resources: irq:125 memory:df200000-df21ffff
     *-pnp00:00
          product: PnP device PNP0c02
          physical id: 2
          capabilities: pnp
          configuration: driver=system
     *-pnp00:01
          product: PnP device PNP0501
          physical id: 3
          capabilities: pnp
          configuration: driver=serial
     *-pnp00:02
          product: PnP device PNP0c02
          physical id: 4
          capabilities: pnp
          configuration: driver=system
     *-pnp00:03
          product: PnP device PNP0b00
          physical id: 5
          capabilities: pnp
          configuration: driver=rtc_cmos
     *-pnp00:04
          product: PnP device INT3f0d
          vendor: Interphase Corporation
          physical id: 6
          capabilities: pnp
          configuration: driver=system
     *-pnp00:05
          product: PnP device PNP0c02
          physical id: 7
          capabilities: pnp
          configuration: driver=system
     *-pnp00:06
          product: PnP device PNP0c02
          physical id: 8
          capabilities: pnp
          configuration: driver=system
     *-pnp00:07
          product: PnP device PNP0c02
          physical id: 9
          capabilities: pnp
          configuration: driver=system
     *-pnp00:08
          product: PnP device PNP0c02
          physical id: a
          capabilities: pnp
          configuration: driver=system
  *-network
       description: Ethernet interface
       physical id: 1
       bus info: usb@1:5
       logical name: enp0s20f0u5
       serial: a0:ce:c8:1d:3f:7a
       size: 100Mbit/s
       capacity: 100Mbit/s
       capabilities: ethernet physical tp mii 10bt 10bt-fd 100bt 100bt-fd autonegotiation
       configuration: autonegotiation=on broadcast=yes driver=r8152 driverversion=v1.09.9 duplex=full ip=172.30.41.15 link=yes multicast=yes port=MII speed=100Mbit/s
WARNING: output may be incomplete or inaccurate, you should run this program as super-user.

```