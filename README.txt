F&S i.MX8M-Plus OSM Yocto Release 2025.04.1 (osm8mp-Y2025.04.1)
==============================================================

Please see the file

  doc/FSiMX8MP_FirstSteps_eng.pdf

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

This is a maintenance release specific for the module "FS 8MP OSM-SF".

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

1. Update Linux Kernel to patch level 5.15.160
 This fixes several smaller bugs and CVEs.
 For more information please see
 https://cdn.kernel.org/pub/linux/kernel/v5.x/ChangeLog-5.15.72
 to
 https://cdn.kernel.org/pub/linux/kernel/v5.x/ChangeLog-5.15.160

 Also adds support for the new F&S LVDS Displays and improves the
 Cortex-M support in Linux and adds SPI-NOR flash support to the
 efusmx8mp.

2. Improved boot loader U-Boot 2021.04

 Several bug fixes and improvements, like the Resource Domain Control
 support in U-Boot device tree and an improved xhci USB driver.

3. Tested with Yocto poky layer version 4.0.20

 This fixes several smaller bugs and CVEs, like CVE-2024-6387 OpenSSH
 signal handler race condition.
 For more information, please see
 https://docs.yoctoproject.org/4.0.20/migration-guides/release-notes-4.0.19.html
 to
 https://docs.yoctoproject.org/4.0.20/migration-guides/release-notes-4.0.20.html


=========================================================================

The following list shows the most noticeable changes in this release in
more detail since our last release for this platform. Please note that the
source code is also used for other platforms. This is why you will
also find references to other CPU types and F&S boards here in the
change log.

u-boot-v2021.04-fs1.0.1 ()
-----------------------------------------------
Supported boards: OSM8MP
- Fix warnings for function-prototypes
- Update ADP-OSM-BB to revision 1.30 for osm8mp
- Fix SDIO_A for high speed SDHC cards on ADP-OSM-BB



linux-v5.15.160-fs1.0.1 ()
-----------------------------------------------
Supported boards: OSM8MP
- Update ADP-OSM-BB to revision 1.30 for osm8mp
- Fix SDIO_A for high speed SDHC cards on ADP-OSM-BB



meta-fus-yocto-4.0.20-fs1.0 ()
-----------------------------------------------
Supported boards: OSM8MP
- fs-setup-release: ensures active shell, when sourced script failes
- Add support for OSM8MP
- Use only annotated Tag for UBoot version
- Remote "-F+S" from UBoot header under Yocto



atf-5.15.71-fsimx8mp-2024.07 ()
-----------------------------------------
Supported boards: PicoCoreMX8MP PicoCoreMX8MPr2 armStonemx8MP
                  efusMX8MP FSSMMX8MP OSM8MP
- Fix poweroff command and ON/OFF button in imx_system_off()
- Fix debug build console for fsimx8mp



firmware-imx-8.10.1 ddr synopsys ()
-------------------------------------------

(no changes)



linux-examples-fus-fs1
-------------------------------------------

(no changes)



Documentation
-------------

- Update to version 1.8 of FSiMX8MP_FirstSteps_eng.pdf
- Update to version 0.22 of LinuxOnFSBoards_eng.pdf

Please download the hardware documentation directly from our website.
Then you always have the newest version.

