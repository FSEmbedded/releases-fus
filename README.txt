F&S i.MX8M-Mini Buildroot Release 2023.11 (fsimx8mm-B2023.11)
==============================================================

Please see the file

  doc/FSiMX8MM_FirstSteps_eng.pdf

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

This is a major release for all F&S boards and modules based on the
i.MX8M-Mini CPU (Solo, Dual and Quad), i.e. PicoCoreMX8MM(r2)-LPDDR4, 
PicoCoreMX8MM-DDR3L
More boards may be added to this family in the future.
All these boards can work with software that is created from this release
package.

Please note that Buildroot releases use a 'Y' for the version number. The
version counting is independent form other releases.


The release consists of the following files and directories:

Readme.txt    Release notes (this text)
setup-buildroot         Script to download and install the Buildroot release
binaries/               Precompiled images (full names)
sdcard/                 Precompiled images (names as expected by
                        install script)
doc/                    Hardware and software manuals, schematics


!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!                               Attention                                     !
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
To use this release, you will have to update to Nboot fsimx8mm-2023.10 and 
U-boot fsimx8mm-2023.11 first. For this we have added an U-Boot update script 
named  "update-all.scr" to the sdcard directory. Rename it to
"update.scr" and copy everything to an USB-Stick. Plug the USB-Stick to the 
board and start it. After the bootdelay the update should begin automatically. 
The board will reset 2 times. It will install Nboot, Uboot and Sysimg.
When everything is complete the line 
"---- update COMPLETE! ----"
will be printed to the console.
Unplug the USB stick or the update will run again on the next reboot.
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!                               Attention                                     !
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!


Here are some highlights of this release.

1. New Linux Kernel 5.15.131

 The Linux kernel is now based on 5.15.131
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

 Of course, there are also many changes for other CPU types (like x86)
 and other graphics cores (like AMD, Nvidia, Intel) but these are not
 of interest here.

2. New bootloader U-Boot 2021.04

 The U-Boot is now based on 2021.04.
 Additional to the security and feature updates of the mainline U-Boot,
 there have been many updates on the fsimage command and the general layout
 of the bootloaders in the flash memory. Because of this, it is necessary to
 update first the U-Boot, reset and the Nboot.
 You can use the update.scr from the sdcard directory for this.

3. New Buildroot version 2023.02.6 

 Updating Buildroot to Version 2023.02.6. This provides many new package
 versions like Weston 10.0.3, imx-gpu-viv 6.4.3.p4.8 or  Busybox 1.36.1.
 There is also a package for QT6.3 available, but it currently doesn't support
 the examples and crosscompiled qmake, so it is reather experimental in this
 release.

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

=========================================================================

The following list shows the most noticeable changes in this release in
more detail since our last release for this platform. Please note that the
source code is also used for other platforms. This is why you will
also find references to other CPU types and F&S boards here in the
change log.

u-boot-2021.04-fsimx8mm-2023.11 ()
-----------------------------------------------
Supported boards: PicoCoreMX8MM-LPDDR4 PicoCoreMX8MMr2-LPDDR4
                  PicoCoreMX8MM-DDR3L 

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
- Fix fat_size for files bigger than 2GB
- Drop board revision from BOARD-CFG names
- Add option -b to fsimage save to select boot partition
- Add command fsimage boot to show current boot settings
- On fsimx8mm, add old device tree names for compatibility
- Fix default entry for environment in NAND
- addfsheader.sh: Check for crc32 and xxd before using them


linux-5.15.71-fsimx8mm-2023.11 ()
-----------------------------------------------
Supported boards: PicoCoreMX8MM-LPDDR4 PicoCoreMX8MMr2-LPDDR4
                  PicoCoreMX8MM-DDR3L

- Update to NXP Linux Version lf-5.15.71-2.2.1
- Remove fsimx8m support
- Switch to FSL_ASOC_CARD sound driver for sgtl5000
- Add F&S Versioning for kernel and device tree
- Improve uart dma support
- Add leds-pca963x-fus driver and revert the original to 
  the mainline driver
- Enable power key support for PicoCore boards
- Improve fsimx8m variants uart clock speed
- Improve SDIO stability for Azurewave wlan chips
- Add support to disable pin controls nodes in the device tree
- Fix picocoremx8mp Bluetooth error after suspend-to-mem
- Apply patches from mainline linux-5.15.131
- Use new naming convention for PicoCoreMX8MM boards
- Add DTS version for fsimx8mm
- Fix Realtek Ethernet Phy Bug in Low Power Mode
- Don't use nand-on-flash-bad block table for fsimx8mm


buildroot-fsimx8mm-2023.11 ()
-----------------------------------------------
Supported boards: PicoCoreMX8MM-LPDDR4 PicoCoreMX8MMr2-LPDDR4
                  PicoCoreMX8MM-DDR3L
- Update to Buildroot 2023.02.6
- Update IMX specific packages to NXP Yocto version lf-5.15.71-2.2.1
- Add F&S Kernel and U-Boot versioning
- Add F&S psplash bootscreen



atf-5.15.71-fsimx8mm-2023.11 ()
-----------------------------------------
Supported boards: PicoCoreMX8MM-LPDDR4 PicoCoreMX8MMr2-LPDDR4
                  PicoCoreMX8MM-DDR3L

- Update to NXP version lf-5.15.71-2.2.1



firmware-imx-8.10.1 ddr synopsys ()
-------------------------------------------

(no changes)



Examples
--------

(no changes)



Documentation
-------------

- Update to version 1.8 of FSiMX8MM_FirstSteps_eng.pdf
- Update to version 0.21 of LinuxOnFSBoards_eng.pdf

Please download the hardware documentation directly from our website.
Then you always have the newest version.

