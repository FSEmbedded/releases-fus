# F&S armStoneMX8MPr2 Yocto Release 2025.12 (armstonemx8mpr2-Y2025.12)

This is a minor release for the armStonemx8MPr2 module based on the i.MX8MP SoC,
and the [NXP lf-6.6.52-2.2.2 release](https://www.nxp.com/docs/en/release-note/RN00210_LF6.6.52_2.2.2.pdf).

Please note, that this release only supports the board armStoneMX8MPr2. Also there will be no
F&S Development Machine, containing this release. It will be added in the next fsimx8mp-Y2025.12.1
release soon.

**Supported Boards**

- armStoneMX8MPr2

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
| sbom/                   | SBOMs of release binaries in SPDX and CycloneDX format  |

**Warning**
The precompiled images are for testing and evaluation purposes only!
DO NOT USE in production or mission-critical environments!

## How to build

Use the latest F&S Development Machine from the [F&S website](https://www.fs-net.de/)
To build the example release binaries, run:

```bash
git clone -b armstonemx8mpr2-Y2025.12 https://github.com/FSEmbedded/releases-fus.git
cd releases-fus
./setup-yocto <build_dir>
./setup-yocto --docker <build_dir>
cd yocto-fus
DISTRO=fus-imx-wayland MACHINE=fsimx8mp . fus-setup-release.sh
bitbake fus-image-std
```

## Highlights

Here are some highlights of this release.

### 1. New Linux Kernel 6.6.129

Add armstonemx8mpr2 support.

### 2. Update U-Boot v2024.04-fus1.8

Add armstonemx8mpr2 support.

### 3. New Yocto version 5.0.17 Scarthgap

Add armstonemx8mpr2 support.

## Known Issues

## Changelog

The following list shows the most noticeable changes in this release in
more detail since our last release for this platform. For a detailed description
please check the respective git histories.

### [u-boot-v2024.04-fus1.8](https://github.com/FSEmbedded/u-boot-fus/tree/v2024.04-fus1.8)

- Add armstonemx8mpr2 support

### [linux-v6.6.129-2.2.2-fus1.4](https://github.com/FSEmbedded/linux-fus/tree/v6.6.129-2.2.2-fus1.4)

- Add armstonemx8mpr2 support

### [meta-fus-yocto-5.0.17-fus1.2](https://github.com/FSEmbedded/meta-fus/tree/yocto-5.0.17-fus1.2)

- Add armstonemx8mpr2 support

### [linux-examples-fus-fus1.1](https://github.com/FSEmbedded/linux-examples-fus/tree/fus1.1)

(no changes)

### nboot-fsimx8mp-2026.05

- Add armstonemx8mpr2 support

### Documentation

- [FSiMX8MP_FirstSteps_eng.pdf](https://www.fs-net.de/)
- [LinuxOnFSBoards_eng.pdf](https://www.fs-net.de/assets/download/docu/common/en/LinuxOnFSBoards_eng.pdf)

Please download the hardware documentation directly from our website.
Then you always have the newest version.

For further support please contact us in the [F&S Forum](https://forum.fs-net.de/)
