F&S i.MX8M-Plus Yocto Release 2023.09 (fsimx8mp-Y2023.09)
==============================================================

Please see the file

  doc/FSiMX8MP_FirstSteps_eng.pdf

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

This is a major release for all F&S boards and modules based on the
i.MX8M-Plus CPU (Solo, Dual and Quad), i.e. PicoCoreMX8MP(r2), armStoneMX8MP 
or efusmx8mp. More boards may be added to this family in the future.
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
To use this release, you will have to update to Nboot 2023.09 and 
U-boot Y2023.09 first. For this we have added an U-Boot update script named 
"update.scr_disbaled" to the sdcard directory. Remove the "_disabled" and copy 
everything to an USB-Stick. Plug the USB-Stick to the board and start it.
After the bootdelay the update should begin automatically. 
The board will reset 2 times. It will install Nboot, Uboot and Sysimg.
When everything is complete the line 
"---- update COMPLETE! ----"
will be printed to the console.
Unplug the USB stick or the update will run again on the next reboot.
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!                               Attention                                     !
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!


Here are some highlights of this release.

1. New Linux Kernel 5.15.71

 The Linux kernel is now based on 5.15.71
 - New optimizations for EXT4.
 - OverlayFS has better performance and copying up more attributes.
 - Many graphics improvements among the DRM/KMS drivers.
 - Linux 5.15 I/O can achieve up to ~3.5M IOPS per-core.
 - The PREEMPT_RT locking code was merged as a big step forward towards 
  getting 
  the real-time (RT) patches upstreamed in the Linux kernel.
 - Various scheduler improvements.
 - Various power management improvements.
 - Opt-in L1 data cache flushing on context switching as a security 
  feature for the paranoid and other specialized conditions.
 - Improvements around compile-time and run-time detection of buffer overflows.
 - Additional protection around side channel attacks via clearing used registers
  prior to returning, making use of the compiler-side support.

  (https://www.phoronix.com/review/linux-515-features)

 Of course there are also many changes for other CPU types (like x86)
 and other graphics cores (like AMD, Nvidia, Intel) but these are not
 of interest here.

2. New bootloader U-Boot 2021.04

 The U-Boot is now based on 2021.04.
 Additional to the security and feature updates of the mainline U-Boot,
 there has been many updates on the fsimage command and the general layout
 of the bootloaders in the flash memory. Because of this, it is necessary to
 update first the U-Boot, reset and the Nboot.
 You can use the update.scr from the sdcard directory for this.

3. New Yocto version 4.0 Kirstone 

 Updating Yocto to Version 4.0 Kirkstone. This provides many new package
 versions like Qt6.3 or Chroium 101.
 We have also updated the poky layer to version 4.0.11

4. Improved Image versioning

 The exact versions of Nboot, U-Boot and Linux Kernel will now be printed 
 during the boot process. 
 If the image is build with an tagged commit the tag name will be printed.
 If the commit is not tagged, the git commits hash will be printed.
 If the image is based on an uncommitted git, the flag "-dirty" will be added 
 to the last commits name.

 We use an own Linux version string that will be printed additionally to the
 mainline Linux version. This way modules that are built for the same Linux 
 version with just some slight changes, can still be loaded without rebuilding
 the whole rootfile system.

 Linux device trees are also versioned with the current version of the linux git.

 You can check the versions of the different components at runtime at /sys/bdinfo/

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

u-boot-2021.04-fsimx8mp-Y2023.09 ()
-----------------------------------------------
Supported boards: PicoCoreMX8MP PicoCoreMX8MPr2 armStonemx8MP
                  efusmx8mp

- Update to NXP u-boot-201.04
- Add mcu_rdc settings to fsimx8mp
- Improve Uboot versioning
- Fix bootaux command
- Introduce crc32 checksums for fsimage save command
- Nboot can now be written to NAND flash with U-Boot
  (No kobs tool needed anymore)
- Relocate U-Boot and Environment in fsimage save if needed
- Have new NAND/MMC layouts for fsimx8mm/mn/mp
- Uboot is now located in the boot partition of eMMC



linux-5.15.71-fsimx8mp-Y2023.09 ()
-----------------------------------------------
Supported boards: PicoCoreMX8MP PicoCoreMX8MPr2 armStonemx8MP
                  efusmx8mp

- Update to NXP Linux Version lf-5.15.71-2.2.0
- Remove fsimx8m support
- Switch to FSL_ASOC_CARD sound driver for sgtl5000
- Add F&S Versioning for kernel and device tree
- Improve uart dma support
- Add leds-pca963x-fus driver and revert the original to 
  the mainline driver
- Enable power key support for PicoCore boards
- Add imx8mp basler isp camera support
- Add ast-adp-edt2 adapter support for efusmx8mp
- Improve fsimx8m variants uart clock speed
- Improve SDIO stability for Azurewave wlan chips
- Add support to disable pin controls nodes in the device tree
- Fix picocoremx8mp Bluetooth error after suspend-to-mem



meta-fus-fsimx8mp-Y2023.09 ()
-----------------------------------------------
Supported boards: PicoCoreMX8MP PicoCoreMX8MPr2 armStonemx8MP
                  efusmx8mp

- Create standalone meta-fus repository
- Update meta-fus to Kirkstone (Yocto 4.0)
- Add new packages to fus-image-std:
  fiwared, can-utils, libgpiod-tools, spitools
- Add asound.state for wm8960 codec
- Fix out-of-tree kernel module building
- Add optional nxp-wifi driver support for Azurewave wlan
- Add image for fsimx8mp basler camera support
- Add calibration file for TSC2004 touch chip
- Add layer versions to the final image
- Set default Linux terminal to vt100
- Remove U-Boot from sysimg
- Add update script for updating NBoot, U-Boot and sysimg



atf-5.15.71-fsimx8mp-2023.09 ()
-----------------------------------------
Supported boards: PicoCoreMX8MP PicoCoreMX8MPr2 armStonemx8MP
                  efusmx8mp

- Update to NXP version lf-5.15.71-2.2.1



firmware-imx-8.10.1 ddr synopsys ()
-------------------------------------------

(no changes)



Examples
--------

(no changes)



Documentation
-------------

- Update to version 1.5 of FSiMX8MP_FirstSteps_eng.pdf
- Update to version 0.19 of LinuxOnFSBoards_eng.pdf

Please download the hardware documentation directly from our website.
Then you always have the newest version.

