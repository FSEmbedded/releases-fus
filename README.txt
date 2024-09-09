F&S i.MX93 Yocto Pre Release 2024.09 (fsimx93-Y2024.09-pre)
==============================================================

Please see the file

  doc/FSiMX93_FirstSteps_eng.pdf

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

This is a major pre release for all F&S boards and modules based on the
i.MX93 CPU, i.e. PicoCoreMX93 or OSM93

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
This pre release is based on NXP lf-6.6.23-2.0.0 release. In the pre release
F&S nboot is not supported yet.
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!                               Attention                                     !
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!


Here are some highlights of this release.

1. New Linux Kernel 6.6.23

 The Linux kernel is now based on 6.6.23
 - EEVDF replaces the existing CFS code scheduler.
 - ReiserFS Officially Declared "Obsolete"
 - KSMBD Declared Stable
 - CephFS Completes Multi-Year Effort Adding FSCRYPT Support.
 - EXT4 Lands A Nice Performance Improvement
 - Tmpfs Gains New Features
 - NFS Enables NFSv4.2 READ_PLUS Option By Default
 - Brings Fixes, Partially Recovers From Scrub Performance Regression
 - Adding Randomized Kmalloc Caches (Linux Security)
 - Various Security improvments (Linux Security)
 - Various kernel graphics improvements
 ...
 Many other improvments.

  (https://www.phoronix.com/review/linux-66-features)

 Of course, there are also many changes for other CPU types (like x86)
 and other graphics cores (like AMD, Nvidia, Intel) but these are not
 of interest here.

2. New bootloader U-Boot 2024.04

 The U-Boot is now based on 2024.04.
 Based on NXP version

3. New Yocto version 5.0 Scarthgap

 Updating Yocto to Version 5.0.3 Scarthgap.

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

u-boot-v2024.04-fs0.1-fsimx93-Y2024.09-pre ()
-----------------------------------------------
Supported boards: PicoCoreMX93, OSM93

- NXP version of u-boot-2024.04 (lf-6.6.23-2.0.0)
- Merge branch 'rel_imx' into fsimx93
- configs:fsimx93: update defconfig to 2024.04
- board:fsimx93: update fsimx93 to 2024.04
- board:fsimx93: adjust lpddr4 timings for osm.
- arch:arm:dts: Improve fs-osm-sf-mx93-adp-osm-bb-u-boot.dtsi
- board:f+s:fsimx93: Improve RAM timings
- arm:dts:imx93: Add a per clock for lpuart3 to lpuart8
- arm:mach-imx:imx9: Initialize lpuart[3-8] root clocks
- arch:arm:mach-imx:imx9:native: Rename board_fix_fdt() to arch_fix_fdt()
- board:f+s:common: Improve fs_fdt_common functionality
- board:f+s:common: Enable fs_eth_common function for iMX9 architecture
- board:f+s:common: Add fs common functionality for fsimx93
- arch:arm: Add F+S common configuartion
- board:f+s:fsimx93: Remove unused function for android
- board:f+s:fsimx93: Improve functionality for fsimx93
- configs: Improve fsimx93 board configuartion
  use F+S common functions
- configs: Improve fsimx93_defconfig
  add fixup, CONFIG_SYS_MAXARGS
- arch:arm:dts: Improve picocoremx93 device tree
- arch:arm:dts: Improve device trees for picocoremx93
- board:f+s:fsimx93: Improve fsimx93.c
- configs: Split fsimx93_deconfig in two configurations
- Improve build process for fsimx93
- In imx8m/soc.c, rename board_fix_fdt() to arch_fix_fdt()
- arch:arm:dts: Improve picocoremx93.dtsi
  improve SPI_B configuration
- board:f+s:fsimx93:Improve support for fsimx93


linux-v6.6.48-fs0.1-fsimx93-Y2024.09-pre ()
-----------------------------------------------
Supported boards: PicoCoreMX93, OSM93

- NXP Version lf-6.6.23-2.0.0
- Merge branch 'linux-imx-6.6.x' into fsimx93
- Original linux-6.6.48
- Merge branch 'linux-6.6.x' into linux-imx-patch-6.6.x
- Merge branch 'linux-imx-patch-6.6.x' into fus-6.6.x
- arch:arm64:boot:dts:f+s: Improve support for picocoremx93
- arch:arm64:boot:dts:f+s: Improve the indentation in Makefile
- arch:arm64:boot:dts:f+s: Remove support for display j070wvtc0211
- arch:arm64:boot:dts:f+s: Improve BT070L1060CS0I1AD-A display support
- arch:arm64:boot:dts:f+s: Add support for ee0350et-2cp display
- arch:arm64:boot:dts:f+s: Improve support for EE1010B1T-1CP display
- arch:arm64:configs: Improve fsimx93_defconfig
- arch:arm64:boot:dts:F+S: Adjust device tree for the BT070L1060CS0I1AD-A
  for osm93 with adapter board


meta-fus-scarthgap-5.0.3-fs0.1-fsimx93-Y2024.09-pre ()
-----------------------------------------------
Supported boards: PicoCoreMX93, OSM93

- Update layer to scarthgap
- Fix image_types_fus
- Fix osm device tree names
- Restructure meta-fus layers
- Improve fsimx93.conf
  change SERIAL_CONSOLES to "115200,ttyLP6"
- Improve handling of NXP wifi mxm-wifiex driver
- Improve alsa-state to deploy asound configuration
- Remove 0001-lib-build_OID_ patch
- Improve packagegroup-qt6-fsimx.bb
- Extend fus-image-std.bb to remove getty tty1
- Move wic directory to meta-fus-bsp
- meta-fus-bsp:conf:machine: Improve KERNEL_DEVICETREE in fsimx93.conf
  Remove device trees for j070wvtc0211 display
- meta-fsu-bsp:conf:machine: Improve KERNEL_DEVICETREE in fsimx93.conf
  Add support for ee0350et-2cp MIPI display.
- meta-fus-bsp:conf:machine: Improve fsimx93.conf
  Rework bootloader configuration
- meta-fus-bsp:imx-mkimage: Rework imx-boot_1.0.bbappend
  add support to use multiple default configurations
- meta-bus-bsp:alsa: Add imx-alsa-plugins_%.bbapend
  Handling QA issue warning
- meta-fus-sdk:dymaic-layer:qt6: Add qtbase_%.bbapend
- meta-fus-bsp:u-boot: Improve 0001-Set-file-system-RW.patch
- meta-fus-sdk:dymaic-layer:qt6: Add qtlanguageserver_%.bbapend
- meta-fus-sdk:dymaic-layer:qt6: Add qtwayland_%.bbapend
- meta-fus-bsp:machine: Improve fsimx93.conf
  Disable ptest support for qtbase, qtdeclarative, qtlanguageserver
  and qtwayland packages
- meta-fus-sdk:classes: Improve image_types_fus.bbclass
  Add IMAGE_NAME_SUFFIX
  Set IMAGE_NAME_SUFFIX = "-qt" in fus-image-qt6.bb

atf-lf_v2.10 ()
-----------------------------------------
Supported boards: PicoCoreMX93, OSM93

- Use NXP version lf-6.6.23-2.0.0


firmware-imx-8.24 ddr synopsys ()
-------------------------------------------

(no changes)


firmware-ele-imx-0.1.2 ()
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
