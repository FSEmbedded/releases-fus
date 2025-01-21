F&S i.MX8M-Mini OSM Yocto Release 2024.10.1 (osm8mm-Y2024.10.1)
==============================================================

Please see the file

  doc/FSiMX8MM_FirstSteps_eng.pdf

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

This is a maintenance release specific for the module "FS 8MM OSM-SF".

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

u-boot-2021.04-osm8mm-2024.10.1 ()
-----------------------------------------------
Supported boards: OSM8MM
- Remove unwanted internal pull-ups for osm8mm


linux-5.15.160-osm8mm-2024.10.1 ()
-----------------------------------------------
Supported boards: OSM8MM
- Remove unwanted internal pull-ups for osm8mm
- Add support for new LVDS display on osm8mm
- Set LED7 for F&S displays to unused
- Add hysteresis for touch interrupt on ADP-OSM-BB
- Set Atheros ethernet phy link detection to interrupt
- Increase deassert delay for reset of Realtek phy


meta-fus-osm8mm-2024.10.1 ()
-----------------------------------------------
Supported boards: OSM8MM
- Add support for LVDS display on osm8mm


atf-5.15.71-fsimx8mm-2024.10 ()
-----------------------------------------

(no changes)


firmware-imx-8.10.1 ddr synopsys ()
-------------------------------------------

(no changes)



linux-examples-fus-fs1
-------------------------------------------

(no changes)



Documentation
-------------

- Update to version 1.9 of FSiMX8MM_FirstSteps_eng.pdf
- Update to version 0.22 of LinuxOnFSBoards_eng.pdf

Please download the hardware documentation directly from our website.
Then you always have the newest version.

