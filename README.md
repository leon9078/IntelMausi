# IntelMausi

[![Build Status](https://github.com/acidanthera/IntelMausi/actions/workflows/main.yml/badge.svg?branch=master)](https://github.com/acidanthera/IntelMausi/actions) [![Scan Status](https://scan.coverity.com/projects/18406/badge.svg?flat=1)](https://scan.coverity.com/projects/18406)

Intel onboard LAN driver for macOS. Courtesy of [Laura Müller](https://github.com/Mieze),
refer to [original repository](https://github.com/Mieze/IntelMausiEthernet) for more details.
This copy includes alterations that are of concern in [Acidanthera](https://github.com/acidanthera)
as well as kernel debugging support initially provided by [aerror2](https://github.com/aerror2) in
[IntelMausiEthernetWithKernelDebugger](https://github.com/aerror2/IntelMausiEthernetWithKernelDebugger)
repository. Do use the original version when uncertain. No support or troubleshooting provided.

In macOS, Wake on LAN from sleep is controlled by the system setting "Wake for network access" or pmset "womp". The same is applied by default for WoL from shutdown.
To force-enable WoL use `mausi-wol-override=1` boot-arg.
To force-disable WoL use `mausi-wol-override=0` boot-arg.

---

A few days before Christmas I started my latest project, a new driver for recent Intel onboard LAN controllers. My intention was not to replace hnak's AppleIntelE1000e.kext completely but to deliver best performance and stability on recent hardware. That's why I dropped support for a number of older NICs. Currently the driver supports:
 
- 5 Series
  - 82578LM
  - 82578LC
  - 82578DM
  - 82578DC
- 6 and 7 Series
  - 82579LM
  - 82579V
- 8 and 9 Series
  - I217LM
  - I217V
  - I218LM
  - I218V
  - I218LM2
  - I218V2
  - I218LM3
- 100 Series
  - I219V
  - I219LM
  - I219V2
  - I219LM2
  - I219LM3
- 200 Series
  - I219LM
  - I219V
- 300 Series
  - I219LM
  - I219V

Key Features of the Driver
- Support for multisegment packets relieving the network stack of unnecessary copy operations when assembling packets for transmission.
- No-copy receive and transmit. Only small packets are copied on reception because creating a copy is more efficient than allocating a new buffer.
- TCP, UDP and IPv4 checksum offload (receive and transmit).
- Support for TCP/IPv6 and UDP/IPv6 checksum offload.
- Makes use of the chip's TCP Segmentation Offload (TSO) feature with IPv4 and IPv6 in order to reduce CPU load while sending large amounts of data (disabled due to hardware bugs).
- Fully optimized for Mavericks or newer (64-bit architecture).
- Support for Energy Efficient Ethernet (EEE).
- VLAN support is implemented but untested as I have no need for it.
- The driver is published under GPLv2.

Support

Please refer to the driver's thread on insanelymac.com

https://www.insanelymac.com/forum/topic/304235-intelmausiethernetkext-for-intel-onboard-lan/

in case you have further questions, need support or want to submit a problem report. As of now, support requests here on Github will be ignored!
