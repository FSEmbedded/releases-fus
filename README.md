# F&S i.MX93  Yocto Release 2025.08.1 (fsimx93-Y2025.08.1)

This is a maintenance release for F&S modules based on the i.MX93 SoC,
based on the [NXP lf-6.6.52-2.2.2 release](https://www.nxp.com/docs/en/release-note/RN00210_LF6.6.52_2.2.2.pdf).

**Supported Boards**

- PicoCoreMX93
- efusMX93
- OSM-SF-MX93
- PicoCom93

Please see the new revision of following file

  [FSiMX93_FirstSteps_eng.pdf](https://www.fs-net.de/en)

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

## How to build

Use the latest F&S Development Machine from the [F&S website](https://www.fs-net.de/)
To build the example release binaries, run:

```bash
git clone -b fsimx93-Y2025.08.1 https://github.com/FSEmbedded/releases-fus.git
cd releases-fus
./setup-yocto <build_dir>
./setup-yocto --docker <build_dir>
cd yocto-fus
DISTRO=fus-imx-wayland MACHINE=fsimx93 . fus-setup-release.sh
bitbake fus-image-std
```

## Highlights

Here are some highlights of this release.

### 1. New Linux Kernel 6.6.119

The Linux kernel is now based on 6.6.119

### 2. New Yocto version 5.0.15 Scarthgap

Updating poky to Version 5.0.15 Scarthgap.
Updating other layers to their latest commits.

### 3. Improve linux-examples-fus

Update the examples to the new linux version.

### 4. New CVE Tracker Tool fs-cve-tracker

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

## Known Issues

## Changelog

The following list shows the most noticeable changes in this release in
more detail since our last release for this platform. For a detailed description
please check the respective git histories.

### [u-boot-v2024.04-fus1.5](https://github.com/FSEmbedded/u-boot-fus/tree/v2024.04-fus1.5)

- Add support for PicoComMX93

### [linux-v6.6.119-2.2.2-fus1.0](https://github.com/FSEmbedded/linux-fus/tree/v6.6.119-2.2.2-fus1.0)

- Update to version 6.6.119
- Add support for PicoComMX93

### [meta-fus-yocto-5.0.15-fus1.0](https://github.com/FSEmbedded/meta-fus/tree/yocto-5.0.15-fus1.0)

- Add support for PicoComMX93

### [atf-v2.10-fus1.3](https://github.com/FSEmbedded/atf-fus/tree/v2.10-fus1.3)

- Apply changes from lf-6.6.52-2.2.2

### [nboot-2026.02.1](https://github.com/FSEmbedded/meta-fus-nboot/tree/fsimx8mp-Y2026.02.1)

- Add support for PicoComMX93

### [linux-examples-fus-fus1.1](https://github.com/FSEmbedded/linux-examples-fus/tree/fus1.1)

- Port ADC test tool to i.MX93 using the recommended IIO framework
- Migrate gpio.c from deprecated sysfs to libgpiod
- Upgrade PWM control to Hz and percentage with polarity support

### Documentation

- [FSiMX93_FirstSteps_eng.pdf](https://www.fs-net.de/)
- [LinuxOnFSBoards_eng.pdf](https://www.fs-net.de/assets/download/docu/common/en/LinuxOnFSBoards_eng.pdf)

Please download the hardware documentation directly from our website.
Then you always have the newest version.

For further support please contact us in the [F&S Forum](https://forum.fs-net.de/)
