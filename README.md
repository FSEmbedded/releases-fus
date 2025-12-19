# F&S MX8MP  Yocto Release 2025.12 (fsimx8mp-Y2025.12)

This is a main release for F&S modules based on the i.MX8MP SoC,
based on the [NXP lf-6.6.52-2.2.1 release](https://www.nxp.com/docs/en/release-note/RN00210.pdf).

**Supported Boards**

- PicocoreMX8MP
- PicocoreMX8MPr2
- armStoneMX8MP
- efusMX8MP
- SMARCMX8MP
- FS8MPOSM-SF

Please see the new revision of following file

  [FSiMX8MP_FirstSteps_eng.pdf](https://www.fs-net.de/en)

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
| spdx/                   | SBOMs of release binaries in SPDX format                |

## How to build

Use the latest F&S Development Machine from the [F&S website](https://www.fs-net.de/)
To build the example release binaries, run:

```bash
git clone -b fsimx8mp-Y2025.12 https://github.com/FSEmbedded/releases-fus.git
cd releases-fus
./setup-yocto <build_dir>
./setup-yoto --docker <build_dir>
cd yocto-fus
DISTRO=fus-imx-wayland MACHINE=fsimx8mp . fus-setup-release.sh
bitbake fus-image-std
```

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

### 2. New bootloader U-Boot 2024.04a

 The U-Boot is now based on 2024.04.

- Add support for i.MX8ULP and i.MX91/93.
- Add support for TCP, HTTP and IPv6 handling to net infrastructure.
- Switch default NFS implementation to NFSv3, use fallback to NFSv1/v2 if
  NFSv3 is not available on host (net/nfs.c).
- Add support for VPL (Verifying Program Loader) to verify signatures and to
  decide which software to load, for example software set A or B. VPL is
  started after TPL and before SPL.
- Add PWM and backlight support for i.MX8M.
- Add support for PWM controlled LEDs (led_pwm.c).
- Add hexdump_line() to format one line of hexdump. Add hex_dump_to_buffer(),
  print_hex_dump() and print_hex_dump_bytes() to format hex dumps in RAM or
  print them directly.
- Add support for I3C in drivers/i2c/imx_i3c.c on NXP SOCs.
- Add support for virtual I2C device in drivers/i2c/imx_virt_i2c.c. The I2C is
  actually handled by Cortex-M, CortexA just sends RPMsg to it.
- Add support for bootflow menues with expo and scenes. The menu is
  handled by an exposition (expo) and can consist of several scenes (e.g.
  screens with a menu each). A scene can consist of several menu entries.
- Add fonts 8x16, sun12x22 and ter16x32 (to include/).
- Add support for RGBA pixel format in BMP images.
- Add support for a new hush parser from current Busybox in addition to the
  hush parser from 2005.
- Remove legacy drivers for many i.MX devices; they require Driver Model now.
- Add support for Link Time Optimization (CONFIG_LTO) on ARM.
- Move many CONFIG settings from .h to Kconfig.

[!CAUTION]
To update from older releases, please:

1. Install U-Boot first
2. Then reset the board to start the new U-Boot
3. Then install NBoot.

### 3. New Yocto version 5.0.14 Scarthgap

 Updating poky to Version 5.0.14 Scarthgap.
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

    ```sh
    git clone -b picocoremx8mm-ddr3l-Y2025.12 https://github.com/FSEmbedded/releases-fus.git
    ```

 2. Prepare Yocto-Build environment
    Run setup-yocto to prepare your Yocto-Build environment. The script will read the repo manifest.xml
    file and syncs all repositories that are needed for Yocto.

    ```sh
     cd releases-fus/
     ./setup-yocto <yocto-buildir>
    ```

 3. Prepare Docker-Environment
    The ./setup-yocto script is capable of setting up a Docker environment in which the bitbake program
    can be executed for the Yocto system. This command will open a docker shell, where you can execute
    all yocto commands as usual.

    ```sh
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

### 6. Experimental Mainline Kernel support

We have added a patchset to enable mainline kernel support for fsimx8mp boards to the meta-fus layer.
You can test it by adding the following line to your conf/local.conf file in your yocto build directory:
```
IMX_DEFAULT_BSP:forcevariable = "mainline"
```
Most of the peripheries are working.
We are planning to enable the mainline kernel for older architectures per default.
For further support please contact the F&S Forum.

## Known Issues

- F&S Over the Air Update is not supported

## Changelog

The following list shows the most noticeable changes in this release in
more detail since our last release for this platform. For a detailed description
please check the respective git histories.

### [u-boot-v2024.04-fus1.4](https://github.com/FSEmbedded/u-boot-fus/tree/v2024.04-fus1.4)

- Update to version v2024.04
- Add OP-TEE Support per default
- Add Secure-Boot support per default
- Add OSM8MP support
- Add option to group ATF/TEE with U-Boot image
- Support boot_instance USB2
- Enable Watchdog in UBoot

### [linux-v6.6.112-2.2.1-fus1.4](https://github.com/FSEmbedded/linux-fus/tree/v6.6.112-2.2.1-fus1.4)

- Update to version 6.6.112
- Add OSM8MP support
- Merge fsimx8mm/mp/mn_defconfigs into single fsimx8_defconfig
- Add options in Device-Tree to configure ON_OFF button behavior
- Add fs-specific tags and GPIO names for fsimx8mp device-trees
- Add picocoremx8mp SD_A_CD device tree config
- Fix handling of chip select for SPI_A and SPI_B on OSM8MP
- Change i2c address of mipi2lvds1 adapter

### [meta-fus-yocto-5.0.14-fus1.0](https://github.com/FSEmbedded/meta-fus/tree/yocto-5.0.14-fus1.0)

- Split meta-fus in meta-fus-bsp and meta-fus-sdk
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
- Add OSM8MP support
- Add experimental kernel mainline support
- Add chromium support with NXP hardware acceleration patches
- Add OpenSSL Provider for SE050 security chip
- Update fusimage-std packages

### [atf-v2.10-fus1.2](https://github.com/FSEmbedded/atf-fus/tree/v2.10-fus1.2)

- Update to v2.10
- Support various UART Devices for different Boards

### [nboot-2025.12](https://github.com/FSEmbedded/meta-fus-nboot/tree/fsimx8mp-Y2025.12)

- Update to version v2024.04
- Add CRC32 output of DRAM-TIMING
- Add prototype for SPL_MULTI_DTB_FIT
- Support boot_instance USB2
- Support new board variants

### [linux-examples-fus-fs1](https://github.com/FSEmbedded/linux-examples-fus/tree/fs1)

(no changes)

### Documentation

- [FSiMX8MP_FirstSteps_eng.pdf](https://www.fs-net.de/)
- [LinuxOnFSBoards_eng.pdf](https://www.fs-net.de/assets/download/docu/common/en/LinuxOnFSBoards_eng.pdf)

Please download the hardware documentation directly from our website.
Then you always have the newest version.

For further support please contact us in the [F&S Forum](https://forum.fs-net.de/)
