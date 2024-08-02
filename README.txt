F&S i.MX8M-Plus Yocto Release 2024.07 (fsimx8mp-Y2024.07)
==============================================================

Please see the file

  doc/FSiMX8MP_FirstSteps_eng.pdf

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

This is a maintenance release for all F&S boards and modules based on the
i.MX8M-Plus CPU (Solo, Dual and Quad), i.e. PicoCoreMX8MP(r2), armStoneMX8MP,
efusmx8mp or SMARCMX8MP (FSSMMX8MP). More boards may be added to this family 
in the future.
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

u-boot-2021.04-fsimx8mp-2024.07 ()
-----------------------------------------------
Supported boards: PicoCoreMX8MP PicoCoreMX8MPr2 armStonemx8MP
                  efusmx8mp SMARCMX8MP
- Check for crc32 and xxd before using them during build
- Add command fsimage boot 
- Add support for FSSMMX8MP
- Add loading of secondary partition Images to fsimx8mp
- Add support for boards with DRAM over 3GB
- Improve sub xhci driver 
- Add RDC Configuration for M7 usage
- Add board-cfg information to linux bdinfo


linux-5.15.160-fsimx8mp-2024.07 ()
-----------------------------------------------
Supported boards: PicoCoreMX8MP PicoCoreMX8MPr2 armStonemx8MP
                  efusmx8mp SMARCMX8MP
- Update to patch level 5.15.160
- Improve imx8mp LVDS clock to support more displays
- Add support for fsimx8mp BT070L1060CS0I1ADA display
- Add support for fsimx8mp EE1010B1T display
- Add support for FSSMMX8MP
- Fix RPMSG failure on boot
- Improve Cortex-M7 Support
- Add efusmx8mp spi nand support
- Fix fsimx8mp DSP dram reservation
- Fix imx uart dma watermark level
- Fix fsimx8mp sgtl5000 mclock issue
- Fix number of chip-selects property in all F&S DTS



meta-fus-fsimx8mp-2024.07 ()
-----------------------------------------------
Supported boards: PicoCoreMX8MP PicoCoreMX8MPr2 armStonemx8MP
                  efusmx8mp SMARCMX8MP
- Add support for FSSMMX8MP
- Add F&S psplash Logo
- Remove fbida from fus-image-std
- Tested with Yocto poky layer version 4.0.20



atf-5.15.71-fsimx8mp-2024.07 ()
-----------------------------------------
Supported boards: PicoCoreMX8MP PicoCoreMX8MPr2 armStonemx8MP
                  efusmx8mp SMARCMX8MP
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

- Update to version 1.6 of FSiMX8MP_FirstSteps_eng.pdf
- Update to version 0.19 of LinuxOnFSBoards_eng.pdf

Please download the hardware documentation directly from our website.
Then you always have the newest version.

