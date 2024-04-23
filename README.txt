F&S i.MX6 Buildroot Release 2024.04 (fsimx6-B2024.04)
==============================================================

Please see the file

  doc/FSiMX6_FirstSteps_eng.pdf

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

This is a major release for all F&S boards and modules based on
the i.MX6 CPUs from NXP.

Currently these are the modules armStoneA9, armStoneA9r2, armStoneA9r3, armStoneA9r4,
efusA9, efusA9r2, PicoMODA9, NetDCUA9, QBlissA9, QBlissA9r2

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


Here are some highlights of this release.


1. New Linux Kernel 5.15.148

 The Linux kernel is now based on 5.15.148
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
 of the bootloaders in the flash memory.

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

Known Issues:

1. The ADP-mPCIe-Wlan adapter does not work with this release

 The PCIe card is recogniced correctly, but the mwifiex-pcie driver load.

=========================================================================

The following list shows the most noticeable changes in this release in
more detail since our last release for this platform. Please note that the
source code is also used for other platforms. This is why you will
also find references to other CPU types and F&S boards here in the
change log.

nbootimx6_51.bin (VN51)
------------------------------------
Supported boards: armStoneA9, armStoneA9r2, armStoneA9r3, armStoneA9r4,
                  efusA9, efusA9r2, PicoMODA9, NetDCUA9, QBlissA9, QBlissA9r2

[VN49]
- 0005378: [NBoot] Ad9 support for new boards efusA9Xr2, armStoneA9R3,
            armStoneA9r4, PicoCoreMX6SXr2

[VN50]
- 0005541: [NBoot] NAND dump does not work
- 0005540: [NBoot] Memory errors on armStoneA9
- 0005542: [NBoot] Board revision is wrong on armStoneA9

[VN51]
- 0005951: [NBoot] Add new board NetDCUA7
- 0005950: [NBoot] Add secure boot for UL with MMC



u-boot-2021.04-fsimx6-2024.04
-----------------------------------------------
Supported boards: armStoneA9, armStoneA9r2, armStoneA9r3, armStoneA9r4,
                  efusA9, efusA9r2, PicoMODA9, NetDCUA9, QBlissA9, QBlissA9r2

- Update to NXP u-boot-2021.04
- Improve Uboot versioning
- Fix bootaux command
- Fix fat_size for files bigger than 2GB
- Drop board revision from BOARD-CFG names
- addfsheader.sh: Check for crc32 and xxd before using them
- Remove sha256 and led blinking support

linux-5.15.71-fsimx6-2024.04
-----------------------------------------------
Supported boards: armStoneA9, armStoneA9r2, armStoneA9r3, armStoneA9r4,
                  efusA9, efusA9r2, PicoMODA9, NetDCUA9, QBlissA9, QBlissA9r2

- Update to NXP Linux Version lf-5.15.71-2.2.1
- Switch to FSL_ASOC_CARD sound driver for sgtl5000
- Add F&S Versioning for kernel and device tree
- Improve uart dma support
- Add leds-pca963x-fus driver and revert the original to
  the mainline driver
- Improve SDIO stability for Azurewave wlan chips
- Add support to disable pin controls nodes in the device tree
- Apply patches from mainline linux-5.15.131
- Fix Realtek Ethernet Phy Bug in Low Power Mode
- Fix backlight flicker for inverted pwm
- Use common dtsi files for efus and armstone boards

buildroot-fsimx6-2024.04
-----------------------------------------------
Supported boards: armStoneA9, armStoneA9r2, armStoneA9r3, armStoneA9r4,
                  efusA9, efusA9r2, PicoMODA9, NetDCUA9, QBlissA9, QBlissA9r2

- Update fsimx6 to Buildroot 2023.02.6
- Update fsimx6 IMX specific packages to NXP Yocto version
  lf-5.15.71-2.2.1
- Add F&S Kernel and U-Boot versioning
- Add F&S psplash bootscreen
- Add support for weston fbdev-backend.



Examples fs1
--------

(no changes)



Toolchain
---------
fs-toolchain-11.2-armv7ahf.tar.bz2 for Linux



Documentation
-------------

- Update to version 4.4 of FSiMX6_FirstSteps_eng.pdf
- Update to version 0.22 of LinuxOnFSBoards_eng.pdf

Please download the hardware documentation directly from our website.
Then you always have the newest version.

