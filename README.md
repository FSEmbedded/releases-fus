# F&S i.MX6UL  Yocto Release 2026.07 (fsimx6ul-Y2026.07)

This is a major release for F&S modules based on the i.MX6UL SoC,
and the [NXP lf-6.6.52-2.2.2 release](https://www.nxp.com/docs/en/release-note/RN00210_LF6.6.52_2.2.2.pdf).

**Supported Boards**

- PicoCOM1.2
- PicoCOMA7
- efusA7UL
- PicoCoreMX6UL
- PicoCoreMX6UL100

Please see the new revision of following file

  [FSiMX6UL_FirstSteps_eng.pdf](https://www.fs-net.de/en)

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
| sbom/                   | SBOMs of release binaries in SPDX and CycloneDX format  |

**Warning**
The precompiled images are for testing and evaluation purposes only!
DO NOT USE in production or mission-critical environments!

## How to build

Use the latest F&S Development Machine from the [F&S website](https://www.fs-net.de/)
To build the example release binaries, run:

```bash
git clone -b fsimx6ul-Y2026.07 https://github.com/FSEmbedded/releases-fus.git
cd releases-fus
./setup-yocto <build_dir>
./setup-yocto --docker <build_dir>
cd yocto-fus
DISTRO=fus-imx-wayland MACHINE=fsimx6ul . fus-setup-release.sh
bitbake fus-image-std
```

## Highlights

Here are some highlights of this release.

### 1. New Linux Kernel 6.6.142

The Linux kernel is now based on 6.6.142, which offers several new bug and security fixes.

### 2. Update U-Boot v2021.04-fs1.4

Fix several open CVEs. See sbom/cyclonedx/vex-u-boot-v2021.04-fs1.4.json for details.

### 3. New Yocto version 5.0.18 Scarthgap

Updating poky to Version 5.0.18 Scarthgap.
Updating other layers to their latest commits.

The meta-fus layer in now split into meta-fus-bsp and meta-fus-sdk. The meta-fus-bsp layer adds basic board support, while meta-fus-sdk adds additional features, which are note necessary to run the board.

The meta-fus layer is now based on meta-freescale and not meta-imx. meta-freescale offers better long time support and more stable releases, while meta-imx supports the newest features but is not as stable and suitable for production. The meta-imx layers are still downloaded for reference, but not included into the build. If you need features from them, please consider adding the changes to your own meta-layer.

### 4. Improve linux-examples-fus

Update the examples to the new linux version.

### 5. New Docker based building system

 The F&S releases now support Docker containers as default building machines.
 By using the Docker environment, the build process can be executed on any Linux host,
 as long as the Docker is installed.
 Starting FS_Development_Machine-Fedora-40_V0.2 Docker will be pre-installed and the
 development machines will not support support building the releases directly anymore.

 If you do not want to use Docker, please check the Dockerfile for the dependencies.
 https://github.com/FSEmbedded/docker-fus/

 1. Download manifest repository

    ```sh
    git clone -b fsimx6ul-Y2026.07 https://github.com/FSEmbedded/releases-fus.git
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

### 6. New Version naming for F&S Linux, U-Boot and meta-fus

 Linux and U-Boot and meta-fus now get their own version number to be more transparent and flexible.
 The Version numbers reflect the Version of the original package, if needed the NXP version and the
 F&S Version. For example the linux version name is composed like this

 [Version Orig. Kernel]-[Version IMX]-[Version FS]

 linux-v6.6.101-2.2.1-fus1.0

 This way it is easier to recognize the applied patch levels and the same package versions can
 be used in multiple releases.

 The actual packages versions are marked as annotated tags in the git history.
 The Name of the overall release (like fsimx93-Y2025.08) is still set as a light tag.

### 7. New CVE Tracker Tool fs-cve-tracker

 The F&S CVE Tracker Tool can help you to keep track of the current CVE status of your yocto image.
 It will launch a local version of [Dependency Track](https://dependencytrack.org) and upload the SBOM
 of your Yocto Build to it. Dependency Track will scan your SBOM for vulnerabilities, which can be downloaded in VEX
 format. The F&S CVE Tracker Tool can also be used to improve your VEX file by marking already fixed CVEs
 or sorting out CVEs which affect components that are not in your build configuration.

 You can also use Dependency Track to audit the remaining CVEs an generate Audit Reports for your documentation.

 For a quick start you can run the following command after your Yocto Build has finished:

```bash
./setup-yoto --cve-tracker
```

This command will install Dependency Track to your system, upload the SBOM from your build and improve your
vulnerabilities scan to sort out as many false positives as possible.

Please note that this may take a while on first run.

### 8. Silex WLAN-Chip support

The Silex-WLAN Chip is supported in this release, but not enabled by default.
To add it to the build, uncomment the following lines in the fs-release-manifest.xml

```xml
<!--
  Uncomment for SILEX WLAN chip support
  <project name="meta-silex-fus" revision="9e6b7784640fb118103da71399ef66245055af54" upstream="scarthgap" path="yocto-fus/sources/meta-silex-fus" remote="fus"/>
-->
```

## Known Issues

- No Blutetooth support for Silex and NXP WLAN driver

## Changelog

The following list shows the most noticeable changes in this release in
more detail since our last release for this platform. For a detailed description
please check the respective git histories.

### [u-boot-v2021.04-fs1.4](https://github.com/FSEmbedded/u-boot-fus/tree/v2021.04-fs1.4)

- Fix several open CVEs

### [linux-v6.6.142-2.2.2-fus1.1](https://github.com/FSEmbedded/linux-fus/tree/v6.6.142-2.2.2-fus1.1)

- Update to version 6.6.142
- Fix Linux CMA allocation for boards >= 2GB DRAM
- Update Silex Wlan driver to Kernel 6.6
- Add GPIO line names to the devicetrees

### [meta-fus-yocto-5.0.18-fus1.1](https://github.com/FSEmbedded/meta-fus/tree/yocto-5.0.18-fus1.1)

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
- Add experimental kernel mainline support
- Add chromium support with NXP hardware acceleration patches
- Add OpenSSL Provider for SE050 security chip
- Update fus-image-std packages
- Update to Yocto 5.0.18
- Add F&S Release Name to fus-image-std
- Remove glmark2 from fus-image-std
- Only create SBOM for runtime-packages for now
- Add u-boot-fus explicitly to the CylconeDX SBOM
- Use NXP wlan driver as default driver

### [linux-examples-fus-fus1.1](https://github.com/FSEmbedded/linux-examples-fus/tree/fus1.1)

- Port ADC test tool to i.MX8MM using the recommended IIO framework
- Migrate gpio.c from deprecated sysfs to libgpiod
- Upgrade PWM control to Hz and percentage with polarity support

### nbootimx6ul_53 (VN53)

- Support additional boards
- Add quick memtest

### Documentation

- [FSiMX6UL_FirstSteps_eng.pdf](https://www.fs-net.de/)
- [LinuxOnFSBoards_eng.pdf](https://www.fs-net.de/assets/download/docu/common/en/LinuxOnFSBoards_eng.pdf)

Please download the hardware documentation directly from our website.
Then you always have the newest version.

For further support please contact us in the [F&S Forum](https://forum.fs-net.de/)
