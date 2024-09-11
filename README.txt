F&S armStoneMX8MP Yocto Release 2024.07.1 (armstonemx8mp-Y2024.07.1)
====================================================================

Please see the file

  doc/FSiMX8MP_FirstSteps_eng.pdf

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

This is a maintenance release for armStoneMX8MP.

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

1. Add support for armStoneMX8MP revision 1.10 

 It feature an optional RS485 transceiver, an EEPROM, a new audio codec
 and several smaller bug fixes and improvements.

=========================================================================

The following list shows the most noticeable changes in this release in
more detail since our last release for this platform. Please note that the
source code is also used for other platforms. This is why you will
also find references to other CPU types and F&S boards here in the
change log.

u-boot-2021.04-fsimx8mp-2024.07.1 ()
-----------------------------------------------
Supported boards: armStonemx8MP

- Add support for armStoneMX8MP Rev 110
- Support output of checksum in fsimage
- Improve boottime for fastboot



linux-5.15.160-fsimx8mp-2024.07.1 ()
-----------------------------------------------
Supported boards: armStonemx8MP
- Add support for armStoneMX8MP Rev 110
- Disable SD UHS support by default for
  armstonemx8mp

meta-fus-fsimx8mp-2024.07 ()
-----------------------------------------------

(no changes)


atf-5.15.71-fsimx8mp-2024.07 ()
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

- Update to version 1.7 of FSiMX8MP_FirstSteps_eng.pdf
- Update to version 0.19 of LinuxOnFSBoards_eng.pdf

Please download the hardware documentation directly from our website.
Then you always have the newest version.

