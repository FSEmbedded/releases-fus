# F&S PicoCoreMX8MMr4 Yocto Release 2026.08 (picocoremx8mmr4-lpddr4-Y2026.08)

This is a minor release for the PicoCoreMX8MMr4-LPDDR4 module based on the i.MX8MM SoC,
and the [NXP lf-6.6.52-2.2.2 release](https://www.nxp.com/docs/en/release-note/RN00210_LF6.6.52_2.2.2.pdf).

Please note, that this release only supports the board PicoCoreMX8MMr4-LPDDR4. Also there will be no
F&S Development Machine, containing this release. It will be added in the next fsimx8mm-Y2026.XX
release soon.

**Supported Boards**

- PicoCoreMX8MMr4-LPDDR4

Please see the new revision of following file

  [FSiMX8MM_FirstSteps_eng.pdf](https://www.fs-net.de/en)

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
git clone -b picocoremx8mmr4-lpddr4-Y2026.08 https://github.com/FSEmbedded/releases-fus.git
cd releases-fus
./setup-yocto <build_dir>
./setup-yocto --docker <build_dir>
cd yocto-fus
DISTRO=fus-imx-wayland MACHINE=fsimx8mm . fus-setup-release.sh
bitbake fus-image-std
```

## Highlights

Here are some highlights of this release.

### 1. New Linux Kernel 6.6.142

Add PicoCoreMX8MMr4 support.

### 2. Update U-Boot v2024.04-fus1.9

Add PicoCoreMX8MMr4 support.

### 3. New Yocto version 5.0.19 Scarthgap

Add PicoCoreMX8MMr4 support.

## Known Issues

## Changelog

The following list shows the most noticeable changes in this release in
more detail since our last release for this platform. For a detailed description
please check the respective git histories.

### [u-boot-v2024.04-fus1.9](https://github.com/FSEmbedded/u-boot-fus/tree/v2024.04-fus1.9)

- Add PicoCoreMX8MMr4 support

### [linux-v6.6.142-2.2.2-fus1.2](https://github.com/FSEmbedded/linux-fus/tree/v6.6.142-2.2.2-fus1.2)

- Add PicoCoreMX8MMr4 support

### [meta-fus-yocto-5.0.19-fus1.0](https://github.com/FSEmbedded/meta-fus/tree/yocto-5.0.19-fus1.0)

- Add PicoCoreMX8MMr4 support

### [linux-examples-fus-fus1.1](https://github.com/FSEmbedded/linux-examples-fus/tree/fus1.1)

(no changes)

### nboot-fsimx8mm-2026.08

- Add PicoCoreMX8MMr4 support

### Documentation

- [FSiMX8MM_FirstSteps_eng.pdf](https://www.fs-net.de/)
- [LinuxOnFSBoards_eng.pdf](https://www.fs-net.de/assets/download/docu/common/en/LinuxOnFSBoards_eng.pdf)

Please download the hardware documentation directly from our website.
Then you always have the newest version.

For further support please contact us in the [F&S Forum](https://forum.fs-net.de/)
