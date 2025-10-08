F&S i.MX6UL Yocto Release 2024.03.1 (fsimx6ul-Y2024.03.1)
==============================================================

Please see the file

  doc/FSiMX6UL_FirstSteps_eng.pdf

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

This is a maintenance release for all F&S boards and modules based on
the i.MX6-UltraLite and i.MX6ULL CPUs from NXP.

Currently these are the modules efusA7UL, PicoCOM1.2, PicoCoreMX6UL,
PicoCoreMX6UL100 and PicoCOMA7.

More boards may be added to this family in the future.
All these boards can work with software that is created from this release
package.

Please note that Yocto releases use a 'Y' for the version number. The
version counting is independent form other releases.


The release consists of the following files and directories:

Readme.txt 				Release notes (this text)
setup-yocto       		Script to download and install the Yocto release
fs-release-manifest.xml	Release Manifest, containing the used versions
binaries/               Precompiled images (full names)
sdcard/                 Precompiled images (names as expected by
                        install script)
doc/                    Hardware and software manuals, schematics

Here are some highlights of this release.

1. New Linux Kernel v5.15.185-2.2.0-fs1.0

 The F&S Kernel is now based on the linux-fslc kernel.
 The fslc kernel has LTS updates for the NXP release versions, so security fixes
 can be applied more easily.
 The Linux kernel is now based on mainline version 5.15.185 and NXP Version 2.2.0

2. New bootloader U-Boot u-boot-2021.04-v2021.04-fs1.2

 Provide some minor bug fixes.

2. meta-fus layer is now based on poky 4.0.29

 We have updated the poky layer to version 4.0.29 and many other layers
 to their latest versions. For a detailed description see fs-release-manifest.xml

3. New Version naming for F&S Linux, U-Boot and meta-fus

 Linux and U-Boot and meta-fus now get their own version number to be more
 transparent and flexible.
 The Version numbers reflect the Version of the original package, if needed
 the NXP version and the F&S Version. For example the linux   version name is
 composed like this

 [Version Orig. Kernel]-[Version IMX]-[Version FS]

 linux-v5.15.185-2.2.0-fs1.0

 This way it is easier to recognize the applied patch levels and the same
 package versions can be used in multiple releases.

 The actual packages versions are marked as annotated tags in the git history.
 The Name of the overall release (like fsimx93-Y2025.08) is still set as a light tag.


Known Issues

1. This Release does not support the Silex WLAN chip on the modules efusA7UL

The Silex WLAN  chip is not supported in this release-
If you need Silex WLAN chip support, please contact F&S.

=========================================================================

The following list shows the most noticeable changes in this release in
more detail since our last release for this platform. Please note that the
source code is also used for other platforms. This is why you will
also find references to other CPU types and F&S boards here in the
change log.

nbootimx6_52.bin (VN52)
------------------------------------
Supported boards: efusA7UL PicoCOM1.2 PicoCoreMX6UL PicoCoreMX6UL100 PicoCOMA7

- Change DRAM Timing for PicoCOMA7



u-boot-2021.04-v2021.04-fs1.2
-----------------------------------------------
Supported boards: efusA7UL PicoCOM1.2 PicoCoreMX6UL PicoCoreMX6UL100 PicoCOMA7

- video_link: Remove video_off variable
- mxs_nand_fus.c: Handle 0-bits in empty pages
- Improve fsimx6/sx realtek delay after HW reset



linux-v5.15.185-2.2.0-fs1.0
-----------------------------------------------
Supported boards: efusA7UL PicoCOM1.2 PicoCoreMX6UL PicoCoreMX6UL100 PicoCOMA7

- Fix number of chip-selects property in all F&S DTS
- Fix imx uart dma watermark level
- Fix ipu_pixel_clk parent recognition
- gpmi-nand-fus.c: Handle 0-bits in empty pages
- Add armstonea9r3q default touch controller
- Update to v5.15.185



meta-fus-yocto-4.0.29-fs1.1
-----------------------------------------------
Supported boards: efusA7UL PicoCOM1.2 PicoCoreMX6UL PicoCoreMX6UL100 PicoCOMA7

- Update to 4.0.29
- Add i.MX6UL touchscreen controller rules



linux-examples-fus-fs1
----------------------------------------------

(no changes)



Documentation
-------------

- Update to version 2.5 of FSiMX6UL_FirstSteps_eng.pdf
- Update to version 0.22 of LinuxOnFSBoards_eng.pdf

Please download the hardware documentation directly from our website.
Then you always have the newest version.

