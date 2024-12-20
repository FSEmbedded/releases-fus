F&S i.MX6SX Yocto Release 2024.12 (fsimx6sx-Y2024.12)
==============================================================

Please see the file

  doc/FSiMX6SX_FirstSteps_eng.pdf

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

This is a major release for all F&S boards and modules based on 
the i.MX6-SoloX CPUs from NXP. 

Currently these are the modules efusA9X, efusA9Xr2, PicoCOMA9X, PicoCoreMX6SX.

More boards may be added to this family in the future.
All these boards can work with software that is created from this release
package.

Please note that Yocto releases use a 'Y' for the version number. The
version counting is independent form other releases.


The release consists of the following files and directories:

README.txt               Release notes (this text)
setup-yocto              Script to download and install the Yocto release
fs-release-manifest.xml  Release Manifest, containing the used versions 
                         as git hashes
binaries/                Precompiled images (full names)
sdcard/                  Precompiled images (names as expected by
                         install script)
doc/                     Hardware and software manuals, schematics


Here are some highlights of this release.


1. New Linux Kernel 5.15.160

1. Update Linux Kernel to patch level 5.15.160
 This fixes several smaller bugs and CVEs.
 For more information please see
 https://cdn.kernel.org/pub/linux/kernel/v5.x/ChangeLog-5.15.72
 to
 https://cdn.kernel.org/pub/linux/kernel/v5.x/ChangeLog-5.15.160

2. New bootloader U-Boot 2021.04

 The U-Boot is now based on 2021.04.
 Additional to the security and feature updates of the mainline U-Boot,
 there have been many updates on the fsimage command and the general layout
 of the bootloaders in the flash memory.

3. Tested with Yocto poky layer version 4.0.20

 This fixes several smaller bugs and CVEs, like CVE-2024-6387 OpenSSH
 signal handler race condition.
 For more information, please see
 https://docs.yoctoproject.org/4.0.20/migration-guides/release-notes-4.0.19.html
 to
 https://docs.yoctoproject.org/4.0.20/migration-guides/release-notes-4.0.20.html

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

6. Support Silex WLAN  Chip on the efusA9X(r2)

 The new driver version is based on version 4.5.25.38 of the original
 Qualcomm driver which is available in branch CNSS.LEA.NRT_3.1 on
 repository (tag v4.5.25.38)
 There is also a Silex-specific version available on request that
 improves roaming, adds bang radar and other improvements. Ask
 F&S if interested.


Knwon Issues:

1. The Slilex Bluetooth Chip on the efusmxA9X(r2) is not supported.

   There is currently no driver available for the Linux Kernel 5.15.
   For Silex Bluetooth chip support, please use the release fsimx6sx-B2019.11.1
   for basic Bluetooth evaluation.


=========================================================================

The following list shows the most noticeable changes in this release in
more detail since our last release for this platform. Please note that the
source code is also used for other platforms. This is why you will
also find references to other CPU types and F&S boards here in the
change log.

nbootimx6sx_51.bin (VN51)
------------------------------------
Supported boards: efusA9X, efusA9Xr2, PicoCOMA9X, PicoCoreMX6SX

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



u-boot-2021.04-fsimx6sx-2024.12
-----------------------------------------------
Supported boards: efusA9X, efusA9Xr2, PicoCOMA9X, PicoCoreMX6SX

- Update to NXP u-boot-201.04
- Improve Uboot versioning
- Fix bootaux command
- Fix fat_size for files bigger than 2GB
- Drop board revision from BOARD-CFG names
- addfsheader.sh: Check for crc32 and xxd before using them
- Remove sha256 support



linux-5.15.160-fsimx6sx-2024.12
-----------------------------------------------
Supported boards: efusA9X, efusA9Xr2, PicoCOMA9X, PicoCoreMX6SX

- Update to NXP Linux Version lf-5.15.71-2.2.1
- Switch to FSL_ASOC_CARD sound driver for sgtl5000
- Add F&S Versioning for kernel and device tree
- Improve uart dma support
- Add leds-pca963x-fus driver and revert the original to 
  the mainline driver
- Enable power key support for PicoCore boards
- Improve SDIO stability for Azurewave wlan chips
- Add support to disable pin controls nodes in the device tree
- Fix Realtek Ethernet Phy Bug in Low Power Mode
- Fix backlight flicker for inverted pwm
- Improve auxiliary_core driver
- Fix picocoma9x rtscts pad settings
- PCOMA9X: Increase CMA size to 200MB
- Apply patches from mainline linux-5.15.160
- Apply patches for Silex-Wlan Chip



meta-fus-fsimx6sx-2024.12
-----------------------------------------------
Supported boards: efusA9X, efusA9Xr2, PicoCOMA9X, PicoCoreMX6SX

- Remove weston G2D default support for fsimx6sx



meta-silex-fus-fsimx6sx-2024.12
-----------------------------------------------
Supported boards: efusA9X, efusA9Xr2

- Create layer


examples-V1
--------

(no changes)


Documentation
-------------

- Update to version 2.3 of FSiMX6SX_FirstSteps_eng.pdf
- Update to version 0.22 of LinuxOnFSBoards_eng.pdf

Please download the hardware documentation directly from our website.
Then you always have the newest version.

