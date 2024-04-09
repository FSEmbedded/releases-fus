F&S i.MX8ULP Yocto Pre Release 2024.04 (fsimx8ULP-Y2024.04-pre)
==============================================================

Please see the file

  doc/FSiMX8ULP_FirstSteps_eng.pdf

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

This is a major pre release for all F&S boards and modules based on the
i.MX8ULP CPU, i.e. PicoCoreMX8ULP or SolderCore8ULP

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

u-boot-v2023.04-fs0.2-fsimx8ulp-Y2024.04-pre ()
-----------------------------------------------
Supported boards: PicoCoreMX8ULP and SolderCore8ULP
-board: fsimx8ulp: remove unnecessary configuration
-dts: cleanup fsimx8ulp.dts
-use fdt_fixup_memory to set correct ram-size in linux fdt
-remove incompatible pin muxing and board configuration
-provide board specific defconfigs
-include/improve devicetree for PicoCore8ULP and SolderCore8ULP
-include ram timings for Nanya, Samsung, Foresee and micron


linux-v6.1.55-fs0.2-fsimx8ulp-Y2024.04-pre ()
-----------------------------------------------
Supported boards: PicoCoreMX8ULP and SolderCore8ULP
-arm64:configs:fsimx8ulp_defconfig: add TOUCHSCREEN_ILITEK module
-dts:F+S:picocoremx8ulp: increase i2c frequency
-gpu:drm:bridge:tc358775: use framesync mode
-gpu:drm:bridge:tc358775: improve reset sequence
-dts:F+S:picocoremx8ulp: add dts for BT070L1060CS0I1AD-A display
-dts:F+S:fsimx8ulp: seperate dtsi for soldercore and picocore 8ulp
-leds: Add leds-pca963x-fus driver
-dts:F+S:picocoremx8ulp: add audio config for AP Domain
-Add PWM usage for driver gpio-pca953x.c
-dts: F+S: add picocoremx8ulp devicetree
-dts: fsimx8ulp.dts: define ele-reserved node on reserved memory

meta-fus-mickledore-4.2.4-fs0.2-fsimx8ulp-Y2024.04-pre ()
-----------------------------------------------
Supported boards: PicoCoreMX8ULP

- Rework meta-fus structure
  Use meta-fus-bsp and meta-fus-sdk, add initial support for fsimx93,
  and fsimx8ulp.
- conf:machine:fsimx93: enable 2d acceleration
- Improve linux-fus recipe for fsimx93


atf-lf_v2.8 ()
-----------------------------------------
Supported boards: PicoCoreMX93, PicoCoreMX8ULP, SolderCore8ULP

- Use NXP version lf-6.1.55-2.2.0



firmware-imx-8.22 ddr synopsys ()
-------------------------------------------

(no changes)



Examples
--------

(no changes)



Documentation
-------------

- Initial version 1.0 of FSiMX8ULP_FirstSteps_eng.pdf
- Update to version 0.20 of LinuxOnFSBoards_eng.pdf

Please download the hardware documentation directly from our website.
Then you always have the newest version.

