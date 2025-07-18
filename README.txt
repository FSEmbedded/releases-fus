F&S i.MX93 Yocto Pre Release 2025.02.1 (fsimx93-Y2025.02-pre)
==============================================================

Please see the new revision of following file

  doc/FSiMX93_FirstSteps_eng.pdf

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

This is a major pre release for all F&S boards and modules based on the
i.MX93 CPU, i.e. PicoCoreMX93 or OSM-SF-MX93

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


This pre release is based on NXP lf-6.6.52-2.2.0 release.

Here are some highlights of this release.

1. New Linux Kernel 6.6.69

 The Linux kernel is now based on 6.6.69
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

3. New Yocto version 5.0 Scarthgap

 Updating Yocto to Version 5.0.4 Scarthgap.

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

u-boot-v2024.04-fs0.3-fsim93-Y2025.02-pre ()
-----------------------------------------------
Supported boards: PicoCoreMX93, OSM93, PicoCoreMX8ULP, OSM8ULP

- tools:imx8image: add CMD_HASH for SHA_HASH token 
- board:fsimx93: add uboot-info.fs target 
- board:fsimx93:nboot: add dram-infos.fs target 
- board:fsimx93:nboot: add board-info.fs target 
- board:fsimx93:nboot: add boot-info.fs target 
- scripts:addfsheader.sh: add imx container support 
- scripts: add extra data flag in addfsheader.sh and fsimage.sh 
- board:fsimx93: define new OCRAM layout 
- board:fsimx93: add MULTI_DTB_FIT support 
- env:nvedit: save redundant env copy 
- board:F+S:fs_cntr_common: provide nboot-info and signature validation 
- board:F+S:fs_image_common: add IMX_CONTAINER support 
- cmd:fsimage: add support for IMX_CONTAINER and new F&S-Image Layout 
- doc:F+S: add Porting-Guide for new NBOOT-Layout 
- board:F+S:fsimx93:nboot: add new BOARD-CFGs 
- board:F+S:fsimx93: implement PCore rev1.1 support 
- board:F+S:fsimx93: add PCore-FERT5 DRAM-Timing 
- Merge branch 'nboot_feature' into fsimx93 
- board:F+S: small improvements after merge 
- board:F+S:fsimx93: Add new DRAM-Timing for OSM-Modules 
- board:F+S:common: consider target fsimx8ulp 
- board:F&S:ffsimx8ulp: add nboot support 
- arm:mach-imx:imx8ulp: configure MDA2-8 as DID1 
- cmd:fsimage: validate U-Boot Image in save_uboot 
- cmd:fsimage: allow to save non flash.fs images in fastboot 
- board:F+S:fsimx8ulp:nboot add OSM8ULP-FERT1 
- board:F+S:fsimx8ulp: add osm8ulp-fert2 
- arch:arm:dts: add fs-osm-sf-mx8ulp dts 
- arch:arm:dts:picocoremx93: new label and alias definition 
- board:F+S:fsimx*: set sec_boot=yes, when board is closed  (tag: v2024.04-fs0.2-pre, tag: fsimx8ulp-Y2024.12-pre)
- Activate optee in fsimx93_defconfig 
- Add support for booting Tianocore UEFI Image, used by Windows IoT 
- WinIoT: Add fs_deviceinfo driver 
- WinIot: Add fsimx93_winiot_defconfig 
- board:F+S:fsimx93:nboot: add OSM93-FERT2 
- board:F+S:fsimx93:nboot: add PCore93-FERT6 
- board:F+S:fsimx8ulp:nboot: add PCoreMX8ULP-FERT6 
- board:F+S:fsimxX:nboot: small BOARD-CFG inprovements 
- board:F+S:fsimxX: define BOARD-Revision as env board_rev 
- dts:fs-osm-sf-mx93.dtsi: update dts for REV1.10 and ADP-OSM-BB REV1.20 
- board:F+S:fsimx8ulp: dump nboot version to 2025.02  (tag: nboot-fsimx8ulp-2025.02)
- board:F+S:fsimxX: skip autoboot during USBx_BOOT 
- board:F+S:fsimx93: add EfusMX93 
- board:F+S:fsimx93: dump NBOOT to 2025.02  (tag: v2024.04-fs0.3-pre, tag: fsimx93-Y2025.02-pre)

linux-v6.6.69-fs0.6-fsimx93-Y2025.02-pre ()
-----------------------------------------------
Supported boards: PicoCoreMX93, OSM93, PicoCoreMX8ULP, OSM8ULP

- Add support of OSM8MM 
- Use bitbanging for SPI_A on adp-osm-bb 
- Handle backlight control better for osm8mm 
- Update version of PCoreBBDSI for fsimx8mm 
- Fix basler support for fsimx8mm 
- Fix pwm frequency for pca963x  (tag: fsimx8mm-2024.10)
- fsimx6: Fix ipu_pixel_clk parent recognition 
- arch:arm64:config: Improve fsimx8mp_defconfig  (origin/master, origin/HEAD)
- fslc-6.6.54-2.1.0  (origin/linux-fslc-6.6.x-2.1.x-imx)
- Merge branch 'linux-fslc-6.6.x-2.1.x-imx' into fsimx93 
- linux-fslc-6.6.x-2.1.x-imx  (origin/linux-imx-patch)
- Merge branch 'linux-imx-patch' into linux-fus-6.6.x 
- Rework arm32 device tree 
- Add F&S versions of lt9211 bgride and nv3051d panel drivers 
- Merge branch 'fsimx93' into linux-fus-6.6.x 
- of: property: Make 'no port node found' output a debug message 
- Merge remote-tracking branch 'origin/fsimx93' into linux-fus-6.6.x 
- fslc-6.6.69-2.2.0  (origin/linux-fslc-6.6.x-2.2.x-imx)
- Merge branch 'linux-fslc-6.6.x-2.2.x-imx' into linux-fus-6.6.x 
- Improve pca963x-fus driver 
- Improve fsim93 display device trees 
- Improve picocoremx93 device trees 
- Fix some warnings 
- Set LED7 for F&S displays to unused on fsimx93/8ulp 
- arch:arm64:dts: Correct ENET2_TD3 pinb configuration in fs-osm-sf-mx93.dtsi 
- arm64:boot:dts:F+S:PicoCoreMX8ULP: keep Power in Suspend for WLAN Device 
- arm64:boot:dts:F+S: add bdinfo for fsimx8ulp  (origin/fsimx93, fsimx93)
- Merge branch 'fsimx93' into linux-fus-6.6.x 
- arm64:boot:dts:F+S: update fs-osm-sf-mx93-adp-osm-bb to rev1.20 
- dts:F+S:fsimx93: add CONFIG_IMX93_TOUCH_RESET 
- dts:F+S: use correct eeprom driver for fsimx93 
- Fix merge error 
- dts:F+S: remove UART_C/UART_D define in OSM93 
- dts:F+S: update cm33 node for fsimx93 
- dts:F+S:displays: add clock-frequency = 400kHz for TOUCH_I2C  (tag: v6.6.69-fs0.3, tag: fsimx93-Y2025.02-pre,)


meta-fus-scarthgap-5.0.4-fs0.2-fsimx93-Y2025.02-pre ()
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
- recipes-bsp: Improve Dependency Decleraton to Prevent Race Conitions 
- recipe-kernel: update linux rev 
- recipes-bsp: update u-boot rev 
- recipes-bsp: update atf rev 
- Improve fus-setup-release 
- Remove nboot reciepes from F&S layer 
- Do not use meta-imx as base layer anymore 
- update srcrev for U-Boot and Linux  (tag: scarthgap-5.0.4-fs0.2-pre, tag: fsimx93-Y2025.02-pre)


atf-lf_v2.10 ()
-----------------------------------------
Supported boards: PicoCoreMX93, OSM93, PicoCoreMX8ULP, OSM8ULP

- plat:imx:imx93: allow OCRAM access in NonSecure state
- plat:imx:imx93: support varius LPUART Devices for different Boards
- plat:imx:imx93: allow OCRAM access in NonSecure state

firmware-imx-8.26 ddr synopsys ()
-------------------------------------------
Supported boards: PicoCoreMX93, OSM93

(no changes)


firmware-ele-imx-1.3.0 ()
-------------------------------------------
Supported boards: PicoCoreMX93, OSM93, PicoCoreMX8ULP, OSM8ULP

(no changes)


Examples
--------

(no changes)


Documentation
-------------

- FSiMX93_FirstSteps_eng.pdf
- LinuxOnFSBoards_eng.pdf

Please download the hardware documentation directly from our website.
Then you always have the newest version.
