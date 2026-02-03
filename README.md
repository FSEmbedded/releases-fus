# F&S MX8MM  Yocto Release 2024.10.1 (fsimx8mm-Y2024.10.1)

This is a maintenance release for F&S modules of the i.MX8MM SoC family,
based on the [NXP lf-5.15.71_2.2.2 release](https://www.nxp.com/docs/en/release-note/L5.15.71_2.2.2_LINUX_RN.pdf).

**Supported Boards**

- PicocoreMX8MM-LPDDR4
- PicocoreMX8MMr2-LPDDR4
- PicocoreMX8MM-DDR3L
- FS8MMOSM-SF

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
| fs-release-manifest.xml | Release Manifest, containing the used versions          |
| binaries/               | Precompiled images (full names)                         |
| sdcard/                 | Precompiled images (names as expected by install script)|
| doc/                    | Manuals and documentation                               |

## How to build

Use the latest F&S Development Machine from the [F&S website](https://www.fs-net.de/)
To build the example release binaries, run:

```bash
git clone -b fsimx8mm-Y2024.10.1 https://github.com/FSEmbedded/releases-fus.git
cd releases-fus
./setup-yocto <build_dir>
cd <build_dir>/yocto-fus
DISTRO=fus-imx-wayland MACHINE=fsimx8mm . fus-setup-release.sh
bitbake fus-image-std
```

## Highlights

Here are some highlights of this release.

### 1. Update Linux Kernel to patch level 5.15.197

Applying the latest bug and security fixes.

### 2. Tested Yocto version 4.0.32 Kirkstone

 Updating poky to Version 4.0.32 Kirkstone.
 Updating other layers to their latest commits.

## Adding support for FSOSM8MM

Adding  support for the FSOSM8MM modules to the architecture specific releases

## Known Issues

None

## Changelog

The following list shows the most noticeable changes in this release in
more detail since our last release for this platform. For a detailed description
please check the respective git histories.

### [u-boot-v2021.04-fs1.3](https://github.com/FSEmbedded/u-boot-fus/tree/v2021.04-fs1.3)

- Add OSM8MM support
- Switching to UART DM model

### [linux-v5.15.197-2.2.0-fs1.0](https://github.com/FSEmbedded/linux-fus/tree/v5.15.197-2.2.0-fs1.0)

- Fix number of chip-selects property in all F&S DTS
- Fix imx uart dma watermark level
- Update to v5.15.197

### [meta-fus-yocto-4.0.29-fs1.1](https://github.com/FSEmbedded/meta-fus/tree/yocto-4.0.29-fs1.1)

- Add OSM8MM support

### [nboot-fsimx8mm-2024.09.4]

- Add OSM8MM support

### [linux-examples-fus-fs1](https://github.com/FSEmbedded/linux-examples-fus/tree/fs1)

(no changes)

### Documentation

- [FSiMX8MM_FirstSteps_eng.pdf](https://www.fs-net.de/)
- [LinuxOnFSBoards_eng.pdf](https://www.fs-net.de/assets/download/docu/common/en/LinuxOnFSBoards_eng.pdf)

Please download the hardware documentation directly from our website.
Then you always have the newest version.

For further support please contact us in the [F&S Forum](https://forum.fs-net.de/)
