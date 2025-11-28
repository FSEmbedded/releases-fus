F&S i.MX6 Buildroot Maintenance Release 2024.04.1 (fsimx6-B2024.04.1)
==============================================================

Please see the file

  doc/FSiMX6_FirstSteps_eng.pdf

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

This is a minor release for all F&S boards and modules based on
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

1. New Linux Kernel v5.15.185-2.2.0-fs1.1

 The F&S Kernel is now based on the linux-fslc kernel.
 The fslc kernel has LTS updates for the NXP release versions, so security fixes
 can be applied more easily.
 The Linux kernel is now based on mainline version 5.15.185 and NXP Version 2.2.0

2. New Version naming for F&S Linux

 Linux now gets his own version number to be more transparent and flexible.
 U-Boot will follow this scheme soon.
 The Version numbers reflect the Version of the original package, if needed
 the NXP version and the F&S Version. For example the linux version name is
 composed like this

 [Version Orig. Kernel]-[Version IMX]-[Version FS]

 linux-v5.15.185-2.2.0-fs1.1

 This way it is easier to recognize the applied patch levels and the same
 package versions can be used in multiple releases.

 The actual packages versions are marked as annotated tags in the git history.
 The Name of the overall release (like fsimx93-Y2025.08) is still set as a light tag.
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
(no changes)



u-boot-2021.04-fsimx6-2024.04
-----------------------------------------------
Supported boards: armStoneA9, armStoneA9r2, armStoneA9r3, armStoneA9r4,
                  efusA9, efusA9r2, PicoMODA9, NetDCUA9, QBlissA9, QBlissA9r2
(no changes)



linux-v5.15.185-2.2.0-fs1.1
-----------------------------------------------
Supported boards: armStoneA9, armStoneA9r2, armStoneA9r3, armStoneA9r4,
                  efusA9, efusA9r2, PicoMODA9, NetDCUA9, QBlissA9, QBlissA9r2

- Change native cs to gpio cs
- Fix number of chip-selects property in all F&S DTS
- Fix imx uart dma watermark level
- Fix ipu_pixel_clk parent recognition
- gpmi-nand-fus.c: Handle 0-bits in empty pages
- Add armstonea9r3q default touch controller
- Update to v5.15.185



buildroot-fsimx6-2024.04.1
-----------------------------------------------
Supported boards: armStoneA9, armStoneA9r2, armStoneA9r3, armStoneA9r4,
                  efusA9, efusA9r2, PicoMODA9, NetDCUA9, QBlissA9, QBlissA9r2

- Update fsimx6 to Buildroot 2023.02.11
- Several packages like python, tar, xwayland and many others get updates



Examples fs1
--------

(no changes)



Toolchain
---------

(no changes)



Documentation
-------------

(no changes)

Please download the hardware documentation directly from our website.
Then you always have the newest version.

