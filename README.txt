F&S i.MX93 Yocto Pre Release 2024.03 (fsimx93-Y2024.03-pre)
==============================================================

Please see the file

  doc/FSiMX93_FirstSteps_eng.pdf

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

This is a major pre release for all F&S boards and modules based on the
i.MX93 CPU, i.e. PicoCoreMX93

More boards may be added to this family in the future.
All these boards can work with software that is created from this release
package.

Please note that Yocto releases use a 'Y' for the version number. The
version counting is independent form other releases.


The release consists of the following files and directories:

Readme-yocto-f+s.txt    Release notes (this text)
setup-yocto             Script to download and install the Yocto release
binaries/               Precompiled images (full names)
sdcard/                 Precompiled images (names as expected by
                        install script)
doc/                    Hardware and software manuals, schematics


!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!                               Attention                                     !
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
This pre release is based on NXP lf-6.1.55-2.2.0 release. In the pre release 
F&S nboot is not supported yet.
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!                               Attention                                     !
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!


Here are some highlights of this release.

1. New Linux Kernel 6.1.55

 The Linux kernel is now based on 6.1.55
 - Fixes and performance optimizations for EXT4.
 - Significant performance optimizations for BTRFS.
 - Many graphics improvements.
 - Support for statx to report direct I/O alignment details.
 - Various Security improvments (Linux Security).
 - Various scheduler improvements.
 - Initial Rust infrastructure.
 ...
 Many other improvments.

  (https://www.phoronix.com/review/linux-61-features)

 Of course, there are also many changes for other CPU types (like x86)
 and other graphics cores (like AMD, Nvidia, Intel) but these are not
 of interest here.

2. New bootloader U-Boot 2023.04

 The U-Boot is now based on 2023.04.
 Based on NXP version

3. New Yocto version 4.2 Mickledore 

 Updating Yocto to Version 4.2.4 Mickledore.

4. Improved Image versioning

TODO:

5. New Release concept over github

 We now provide our Linux gits over github at https://github.com/FSEmbedded.
 All release and pre-release states will be pushed here.
 For now, we will not push each single commit to github. 

 Also the release sources are not added to the release tar anymore, but will
 be downloaded from github during the setup process.
 
 The versions of the different gits of a release can be looked up in the 
 fs-release-manifest.xml file in the release tar directory.

6. New Azurewave wlan driver

 Additional to the mainline SD-BT-8997 driver we now provide the NXP
 version. This driver supports additional security features, optimized.
 STA and AP modes and improved roaming.

 To activate the nxp mlan driver uncomment the respective lines in:
 recipes-kernel/kernel-modules/files/mxm-wifiex.conf
 Also comment out the line for the mainline mwifiex driver.

 Please note that bluetooth is currently not supported with the
 nxp-mlan driver. For Bluetooth please use the mainline driver.


=========================================================================

The following list shows the most noticeable changes in this release in
more detail since our last release for this platform. Please note that the
source code is also used for other platforms. This is why you will
also find references to other CPU types and F&S boards here in the
change log.

u-boot-v2023.04-fs0.1-fsimx93-Y2024.03-pre ()
-----------------------------------------------
Supported boards: PicoCoreMX93

- arm:dts:imx93: Add a per clock for lpuart2
- arm:mach-imx:imx9: Initialize lpuart2 root clock
- Add board support for fsimx93
- common: Impvore usb_storage for usb devices
- Correct copyright message
- Improve picocoremx93 device tree



linux-v6.1.55-fs0.1-fsimx93-Y2024.03-pre ()
-----------------------------------------------
Supported boards: PicoCoreMX93

- arch:arm64:dts:freescale: Improve imx93.dtsi
- clock: Improve binding clock definitions for imx93
- arch:arm64:dts:f+s: Add device tree support for picocoremx93
- char: Add bdinfo driver
- rtc: Add rtc pcf85263 driver
- leds: Add leds-pca963x-fus driver
- spi: Improve spidev driver
- input:touch:focaltech: Improve focaltech touch driver
- Add support to use fsversion
- gpu:drm:bridge: Add F+S version of sn65dsi84-dsi2lvds driver
- arch:arm64:configs: Add default configuration for fsimx93
- arch:arm64:dts:f+s:picocoremx93: enable epxp node
- arch:arm64:dts:f+s: add picocoremx93-adp-lvds2lvds2-EE1010B1T-1CP
- drivers:input:touchscreen:goodix: configure interrupt direction
- dts:F+S:picocoremx93: complete BT070L1060CS0I1AD-A for ADP-LVDS2LVDS1


meta-fus-mickledore-4.2.4-fs0.1-fsimx93-Y2024.04-pre ()
-----------------------------------------------
Supported boards: PicoCoreMX93

- Rework meta-fus structure
  Use meta-bsp and meta-sdk, add initial support for fsimx93
- conf:machine:fsimx93: enable 2d acceleration
- Improve linux-fus recipe for fsimx93


atf-lf_v2.8 ()
-----------------------------------------
Supported boards: PicoCoreMX93

- Use NXP version lf-6.1.55-2.2.0



firmware-imx-8.22 ddr synopsys ()
-------------------------------------------

(no changes)



Examples
--------

(no changes)



Documentation
-------------

- Initial version 1.0 of FSiMX93_FirstSteps_eng.pdf
- Update to version 0.20 of LinuxOnFSBoards_eng.pdf

Please download the hardware documentation directly from our website.
Then you always have the newest version.

