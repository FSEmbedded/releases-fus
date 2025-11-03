# F&S i.MX8ULP Yocto Release 2025.11 (fsimx8ulp-Y2025.11)

This is a main release for all F&S boards and modules based on the i.MX8ULP SoC,
based on the [NXP lf-6.6.52-2.2.1 release](https://www.nxp.com/docs/en/release-note/RN00210.pdf).

**Supported Boards**
- PicoCoreMX8ULP rev 1.10
- OSM-SF-MX8ULP rev 1.10

Please see the new revision of following file

  [FSiMX8ULP_FirstSteps_eng.pdf](https://www.fs-net.de/de/imx8ulp)

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

Please note that Yocto releases use a 'Y' for the version number. The
version counting is independent form other releases.

## Content

The release consists of the following files and directories:

| File                    | Purpose                                                 |
| ------------------------| --------------------------------------------------------|
| README.md               | Release notes                                           |
| setup-yocto             | Script to download and install the Yocto release        |
| helper-setup-yocto      | Helper script for setup-yocto                           |
| fs-release-manifest.xml | Release Manifest, containing the used versions          |
| binaries/               | Precompiled images (full names)                         |
| sdcard/                 | Precompiled images (names as expected by install script)|
| doc/                    | Manuals and documentation                               |
| spdx/ 				  | SBOMs of release binaries in SPDX format                |


## Highlights

Here are some highlights of this release.

### 1. New Linux Kernel 6.6.112

 The F&S Kernel is now based on the [linux-fslc kernel](https://github.com/Freescale/linux-fslc/).

 The fslc kernel has LTS updates for the NXP release versions, so security
 fixes can be applied more easily.

 The Linux kernel is now based on 6.6.112
 - EEVDF replaces the existing CFS code scheduler.
 - ReiserFS Officially Declared "Obsolete"
 - KSMBD Declared Stable
 - CephFS Completes Multi-Year Effort Adding FSCRYPT Support.
 - EXT4 Lands A Nice Performance Improvement
 - Tmpfs Gains New Features
 - NFS Enables NFSv4.2 READ_PLUS Option By Default
 - Brings Fixes, Partially Recovers From Scrub Performance Regression
 - Adding Randomized Kmalloc Caches (Linux Security)
 - Various Security improvements (Linux Security)
 - Various kernel graphics improvements

 ...
 Many other improvements.

  (https://www.phoronix.com/review/linux-66-features)

 Of course, there are also many changes for other CPU types (like x86)
 and other graphics cores (like AMD, Nvidia, Intel) but these are not
 of interest here.

### 2. New bootloader U-Boot 2024.04

 The U-Boot is now based on 2024.04.
 Add support for Secure-Boot,  A/B Update, OP-TEE to the U-Boot.

### 3. New Yocto version 5.0.13 Scarthgap

 Updating poky to Version 5.0.13 Scarthgap.
 Updating other layers to their latest commits.

 The meta-fus layer in now split into meta-fus-bsp and meta-fus-sdk.
 The meta-fus-bsp layer adds basic board support, while meta-fus-sdk
 adds additional features, which are note necessary to run the board.

 The meta-fus layer is now based on meta-freescale and not meta-imx.
 meta-freescale offers better long time support and more stable releases,
 while meta-imx supports the newest features but is not as stable and
 suitable for production.
 The meta-imx layers are still downloaded for reference,  but not included
 into the build.
 If you need features from them, please consider adding the changes to your
 own meta-layer.

### 4. New Docker based building system

 The F&S releases now support Docker containers as default building machines.
 By using the Docker environment, the build process can be executed on any Linux host,
 as long as the Docker is installed.
 Starting FS_Development_Machine-Fedora-40_V0.2 Docker will be pre-installed and the
 development machines will not support support building the releases directly anymore.

 If you do not want to use Docker, please check the Dockerfile for the dependencies.
 https://github.com/FSEmbedded/docker-fus/

 1. Download manifest repository

	```
	git clone -b fsimx8ulp-Y2025.11 https://github.com/FSEmbedded/releases-fus.git
	```

 2. Prepare Yocto-Build environment
	Run setup-yocto to prepare your Yocto-Build environment. The script will read the repo manifest.xml
	file and syncs all repositories that are needed for Yocto.

	```
	 cd releases-fus/
	 ./setup-yocto <yocto-buildir>
	```

 3. Prepare Docker-Environment
	The ./setup-yocto script is capable of setting up a Docker environment in which the bitbake program
	can be executed for the Yocto system. This command will open a docker shell, where you can execute
	all yocto commands as usual.

	```
	 ./setup-yocto <yocto-buildir> --docker
	  cd yocto-fus/
	```

### 5. New Version naming for F&S Linux, U-Boot and meta-fus

 Linux and U-Boot and meta-fus now get their own version number to be more transparent and flexible.
 The Version numbers reflect the Version of the original package, if needed the NXP version and the
 F&S Version. For example the linux version name is composed like this

 [Version Orig. Kernel]-[Version IMX]-[Version FS]

 linux-v6.6.101-2.2.1-fus1.0

 This way it is easier to recognize the applied patch levels and the same package versions can
 be used in multiple releases.

 The actual packages versions are marked as annotated tags in the git history.
 The Name of the overall release (like fsimx93-Y2025.08) is still set as a light tag.

## Changelog

The following list shows the most noticeable changes in this release in
more detail since our last release for this platform. For a detailed description
please check the respective git histories.

### [u-boot-v2024.04-fus1.2](https://github.com/FSEmbedded/u-boot-fus/tree/v2024.04-fus1.2)

- Update to version v2024.04
- Add support for fsimx8ulp boards
- Add F&S update support
- Add F&S boot strategy support
- Add fsimage support
- Add OP-TEE Support
- Add A/B update support
- Add Secure-Boot support

### [linux-v6.6.112-2.2.1-fus1.2](https://github.com/FSEmbedded/linux-fus/tree/v6.6.112-2.2.1-fus1.2)

- Update to version 6.6.112
- Add support for fsimx8ulp boards
- Add bluetooth support
- Add F&S displays support
- Add bdinfo support


### [meta-fus-yocto-5.0.13-fus1.2](https://github.com/FSEmbedded/meta-fus/tree/yocto-5.0.13-fus1.2)

- Split meta-fus in meta-fus-bsp and meta-fus-sdk
- Add fsimx8ulp support
- Update layer to yocto scarthgap
- Add dynamic layers for basler and qt6
- Clone fus specific gits from github again
  (Do not use the local gits anymore)
- Add additional test packages to the fus-image-sdt
- Use meta-freescale as base layer instead of meta-imx
- Add possibility to add Chromium and SPDX generation
  via the fus-setup-release script
- Add bcsend support to connect to the board via FSDeviceSpy
- Improve remote desktop support
- Update Kernel, Uboot, and ATF to the latest F&S versions


### [atf-v2.10-fus1.1](https://github.com/FSEmbedded/atf-fus/tree/v2.10-fus1.1)

- Preselect CLKMUX for TPM6/TPM7
- Support various LPUART Devices for different Boards
- Support Suspend for DSL and PD/DPD

### [nboot-2025.11](https://github.com/FSEmbedded/meta-fus-nboot/tree/fsimx8ulp-Y2025.11)

- Add fsimx8ulp boards support
- Add F&S specific container layout
- firmware-upower-1.3.1
- firmware-ele-imx-2.0.2.1


### [linux-examples-fus-fs1](https://github.com/FSEmbedded/linux-examples-fus/tree/fs1)

(no changes)


### Documentation

- [FSiMX8ULP_FirstSteps_eng.pdf](https://www.fs-net.de/de/imx8ulp)
- [LinuxOnFSBoards_eng.pdf](https://www.fs-net.de/assets/download/docu/common/en/LinuxOnFSBoards_eng.pdf)

Please download the hardware documentation directly from our website.
Then you always have the newest version.
