F&S i.MX8ULP Yocto Pre Release 2024.12 (fsimx8ulp-Y2024.12-pre)
==============================================================

Please see the new revision of following file

  doc/FSiMX8ULP_FirstSteps_eng.pdf

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

This is a major pre release for all F&S boards and modules based on the
i.MX8ULP CPU, i.e. PicoCoreMX8ULP or OSM8ULP

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


This pre release is based on NXP lf-6.6.23-2.0.0 release.

Here are some highlights of this release.

1. New Linux Kernel 6.6.43

 The Linux kernel is now based on 6.6.43
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

u-boot-v2024.04-fs0.2-fsimx8ulp-Y2024.12-pre ()
-----------------------------------------------
Supported boards: PicoCoreMX93, OSM93, PicoCoreMX8ULP, OSM8ULP

- board:F+S: create NXP-Firmware dir
- Merge branch 'nboot_feature' into fsimx93
- board:F+S: small improvements after merge
- board:F+S:fs_fdt_common: search in __symbols__ to get node offs
- Makefile: rename target firmware.fs to flash.fs
- arch:arm:mach-imx:ele_ahab: fix typo
- make uboot-info.fs as default target
- board:F+S:fs_cntr_common: Expect DRAM-FW dynamically during loading
- cmd:fsimage: allow -b 0/1/2 args during fsimage save
- board:F+S:fs_cntr_common: bugfix ptr-arithmetic in hash-validation
- board:F&S:common: improve verbosity in bootflow
- cmd:fsimage: fix board-id overwrite for cntr images
- tools:imx8image: add UPOWER && M33 Core
- board:F+S:common: consider target fsimx8ulp
- board:F&S:ffsimx8ulp: add nboot support
- arch:asm:mach-imx:imx8ulp: determine LPUART clk during runtime
- arm:mach-imx:imx8ulp: configure MDA2-8 as DID1
- board:F&S:common:fs_cntr_common: Workaround loading board-cfg for 8ulp
- cmd:fsimage: validate U-Boot Image in save_uboot
- board:F+S:common:fs_bootrom: ensure alignment during the search for FSH
- board:F+S: add prepare_nboot target
- scripts:addfsheader: Trapping and exit on error
- cmd:fsimage: allow to save non flash.fs images in fastboot
- board:F+S:*:nboot: add git-version in nboot version
- board:F+S:fsimx8ulp:nboot add OSM8ULP-FERT1
- board:F+S:fsimx8ulp: increase FDT and SPL-Stack size
- board:F+S:fsimx8ulp: remove SPL_BOARD_INIT
- board:F+S:fsimx8ulp: add osm8ulp-fert2
- board:F+S:fsimx8ulp:nboot: improve OSM DRAM config
- board:F+S:fsimx8ulp: use fdt_fixup_memory_banks
- arch:arm:dts: add fs-osm-sf-mx8ulp dts
- board:F+S:fsimx8ulp:nboot: add have-eth feature for PCore
- board:F+S:fsimx8ulp: small improvements
- cmd:fsimage: bugfix use correct header
- board:F+S:fsimx*: set sec_boot=yes, when board is closed

linux-v6.6.48-fs0.2-fsimx8ulp-Y2024.12-pre ()
-----------------------------------------------
Supported boards: PicoCoreMX93, OSM93, PicoCoreMX8ULP, OSM8ULP

- drivers:rtc: remove rtc-pcf85263.c
- drivers:rtc:rtc-pcf85363: add clk-out and drive property
- arch:arm64:boot:dts:F+S: update rtc node for fsimx93
- arm64:boot:dts:F+S:picocoremx93: add gpio_adp for BT070L1060CS0I1AD-A
- arm64:boot:dts:F+S:picocoremx93: use SoM specific labels and alias IDs
- arm64:boot:dts:F+S:fs-osm-mx93: add pinctrl for USB_*_OC
- arm64:boot:dts:F+S: add fs-osm-sf-mx8ulp-adp-osm-bb
- arm64:boot:dts:F+S: rework picocoremx8ulp devicetrees
- arch:arm64:boot:dts:F+S: add imx8ulp.dtsi
- arm64:configs:fsimx8ulp: build IMX_SEC_ENCLAVE as internal
- gpu:drm:panel:newvision: add F&S version for nv3051d
- gpu:drm:panel:newvision-fus: add modes
- arm64:boot:dts:F+S: improve fsimx8ulp display dts
- gpu:drm:bridge:nwl-dsi: add drm_atomic_bridge_chain_pre_enable()
- dts:F+S:picocoremx8ulp: improve Display support


meta-fus-scarthgap-5.0.3-fs0.2-fsimx93-Y2024.12-pre ()
-----------------------------------------------
Supported boards: PicoCoreMX93, OSM93, PicoCoreMX8ULP, OSM8ULP

- meta-fus-bsp:recipes-bsp:u-boot: Generate .scmversion from annotated tag
- meta-fus-bsp:uboot: add nboot recipe
- Use github for F&S specific gits
- Improve fsimx93 bootloader building
- Update uboot-fus
- Update linux-fus
- Improve fus-image-std
- Update atf-fus
- meta-fus-bsp:recipes-bsp: add realtimed recipe
- meta-fus-bsp:conf:machine:fsimx8ulp: update machine conf
- meta-fus-bsp:conf:machine:fsimx93: update machine conf
- recipe-kernel: update linux rev
- recipes-bsp: update u-boot rev
- recipes-bsp: update nboot rev
- recipes-bsp: update atf rev


atf-lf_v2.10 ()
-----------------------------------------
Supported boards: PicoCoreMX93, OSM93, PicoCoreMX8ULP, OSM8ULP

- plat:imx:imx93: allow OCRAM access in NonSecure state
- plat:imx:imx93: support varius LPUART Devices for different Boards
- plat:imx:imx93: allow OCRAM access in NonSecure state

firmware-imx-8.24 ddr synopsys ()
-------------------------------------------
Supported boards: PicoCoreMX93, OSM93

(no changes)


firmware-ele-imx-1.2.0 ()
-------------------------------------------
Supported boards: PicoCoreMX8ULP, OSM8ULP

(no changes)


Examples
--------

(no changes)


Documentation
-------------

- FSiMX8ULP_FirstSteps_eng.pdf
- LinuxOnFSBoards_eng.pdf

Please download the hardware documentation directly from our website.
Then you always have the newest version.
