F&S i.MX8M-Plus Yocto Pre Release 2025.03 (fsimx8mp-Y2025.03-pre)
==============================================================

Please see the file

  doc/FSiMX8MP_FirstSteps_eng.pdf

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

This is a major pre-release for all F&S boards and modules based on the
i.MX8M-Plus CPU (Solo, Dual and Quad), i.e. PicoCoreMX8MP(r2), armStoneMX8MP,
efusmx8mp or SMARCMX8MP (FSSMMX8MP). More boards may be added to this family 
in the future.
All these boards can work with software that is created from this release
package.

Please note that Yocto releases use a 'Y' for the version number. The
version counting is independent form other releases.

The release consists of the following files and directories:

Readme-yocto-f+s.txt    	Release notes (this text)
setup-yocto             	Script to download and install the Yocto release
fs-release-manifest.xml  	Release Manifest, containing the used versions 
binaries/               	Precompiled images (full names)
sdcard/                 	Precompiled images (names as expected by
                        	install script)
doc/                    	Hardware and software manuals, schematics

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!                               Attention                                     !
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
This is a pre-release and not suitable for production!
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!                               Attention                                     !
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

This pre release is based on NXP lf-6.6.52-2.2.0 release.

Here are some highlights of this release.

1. New Linux Kernel based on lf-6.6.52-2.2.0 with patchleve 6.6.69
	The F&S Kernel is now based on the linux-fslc kernel.
	https://github.com/Freescale/linux-fslc/
	The fslc kernel has LTS updates for the NXP release versions, so security
	fixes can be applied more easily.

2. Old bootloader U-Boot 2021.04

	In the final release, the bootloader will be based on version 2024.04.

3. New Yocto version 5.0 Scarthgap

	Updating Yocto to Version 5.0.4 Scarthgap.

	The meta-fus layer is now based on meta-freescale and not meta-imx.
	meta-freescale offers better long time support and more stable releases,
	while meta-imx supports the newest features but is not as stable and 
    suitable for production.
	The meta-imx layers are still downloaded for reference,  but not included
	into the build.
	If you need features from them, please consider adding the changes to your
	own meta-layer.

4. New Docker based building system

	The F&S releases now support Docker containers as default building machines.
	By using the Docker environment, the build process can be executed on any Linux host,
	as long as the Docker is installed.
	Starting FS_Development_Machine-Fedora-40_V0.2 Docker will be pre-installed and the
	development machines will not support support building the releases directly anymore.

	If you do not want to use Docker, please check the Dockerfile for the dependencies.
	https://github.com/FSEmbedded/docker-fus/

 1.Download manifest repository

	 git clone -b fsimx8mp-Y2025.03-pre https://github.com/FSEmbedded/releases-fus.git

 2. Prepare Yocto-Build environment
	Run setup-yocto to prepare your Yocto-Build environment. The script will read the repo manifest.xml
	file and syncs all repositories that are needed for Yocto.

	 cd releases-fus/
	 ./setup-yocto <yocto-buildir>

 3. Prepare Docker-Environment
	The ./setup-yocto script is capable of setting up a Docker environment in which the bitbake program
	can be executed for the Yocto system. This command will open a docker shell, where you can execute 
	all yocto commands as usual.

	 ./setup-yocto --docker


=========================================================================

The following list shows the most noticeable changes in this release in
more detail since our last release for this platform. Please note that the
source code is also used for other platforms. This is why you will
also find references to other CPU types and F&S boards here in the
change log.

u-boot-v2021.04-fs0.1-pre
-----------------------------------------------
Supported boards: PicoCoreMX8MP PicoCoreMX8MPr2 armStonemx8MP
                  efusmx8mp SMARCMX8MP




linux-v6.6.69-fs0.4-pre
-----------------------------------------------
Supported boards: PicoCoreMX8MP PicoCoreMX8MPr2 armStonemx8MP
                  efusmx8mp SMARCMX8MP

- Update fsimx8 boards to Kernel 6.6



meta-fus-yocto-5.0.4-fs0.3-pre
-----------------------------------------------
Supported boards: PicoCoreMX8MP PicoCoreMX8MPr2 armStonemx8MP
                  efusmx8mp SMARCMX8MP

- Update fsimx8 boards to Yocto 5.0
- Use Kernel and U-Boot version specific recipes



atf-5.15.71-fsimx8mp-2024.07
-----------------------------------------
Supported boards: PicoCoreMX8MP PicoCoreMX8MPr2 armStonemx8MP
                  efusmx8mp SMARCMX8MP

(no changes)

firmware-imx-8.10.1 ddr synopsys
-------------------------------------------

(no changes)

Examples
--------

(no changes)

Documentation
-------------

- Update to version 1.6 of FSiMX8MP_FirstSteps_eng.pdf
- Update to version 0.19 of LinuxOnFSBoards_eng.pdf

Please download the hardware documentation directly from our website.
Then you always have the newest version.
