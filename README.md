# F&S i.MX8MM  Buildroot Release 2026.07 (fsimx8mm-Y2026.07)

This is a major release for F&S modules based on the i.MX8MM SoC,
based on the [NXP lf-6.6.52-2.2.2 release](https://www.nxp.com/docs/en/release-note/RN00210_LF6.6.52_2.2.2.pdf).

**Supported Boards**

- PicoCoreMX8MM-DDR3L
- PicoCoreMX8MM-LPDDR4
- PicoCoreMX8MMr2-LPDDR4
- OSM-SF-MX8MM

Please see the new revision of following file

  [FSiMX8MM_FirstSteps_eng.pdf](https://www.fs-net.de/assets/download/docu/common/en/FSiMX8MM_FirstSteps_eng.pdf)

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

Please note that Yocto releases use a 'B' for the version number. The
version counting is independent form other releases.

## Content

The release consists of the following files and directories:

| File                    | Purpose                                                 |
| ------------------------| --------------------------------------------------------|
| README.md               | Release notes                                           |
| setup-buildroot         | Script to download and install the Yocto release        |
| helper-setup-buildroot  | Helper script for setup-yocto                           |
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
git clone -b fsimx8mm-B2026.07 https://github.com/FSEmbedded/releases-fus.git
cd releases-fus
./setup-buildroot <build_dir>
./setup-buildroot --docker <build_dir>
cd buildroot-fus
make fsimx8mm_wayland_defconfig
make
```

## Highlights

Here are some highlights of this release.

### 1. New Linux Kernel 6.6.142

The Linux kernel is now based on 6.6.142, which offers several new bug and security fixes.

### 2. New bootloader U-Boot 2024.04

The U-Boot is now based on 2024.04.

[!CAUTION]
To update from older releases, please:

1. Install U-Boot first
2. Then reset the board to start the new U-Boot
3. Then install NBoot.

### 3. New Buildroot version 2025.02.16

Buildroot now has a 3-year LTS cycle starting with 2025.02 with a patch level upgrade aproximatly every month.

Since the last release most packages have been updated to more current versions and sbom support has been implemented.

### 4. Improve linux-examples-fus

Update the examples to the new linux version.

### 3. Improve linux-examples-fus
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
    git clone -b fsimx8mm-2026.07 https://github.com/FSEmbedded/releases-fus.git
    ```

 2. Prepare Buildroot-Build environment
    Run setup-buildroot to prepare your Buildroot-Build environment. The script will read the repo manifest.xml
    file and syncs all repositories that are needed for Buildroot.

    ```sh
     cd releases-fus/
     ./setup-buildroot <buildroot-buildir>
    ```

 3. Prepare Docker-Environment
    The ./setup-buildroot script is capable of setting up a Docker environment in which the bitbake program
    can be executed for the Buildroot system. This command will open a docker shell, where you can execute
    all buildroot commands as usual.

    ```sh
     ./setup-buildroot <buildroot-buildir> --docker
     cd buildroot-fus/
    ```

### 5. New Version naming for F&S Linux, U-Boot and buildroot-fus

 Linux, U-Boot and buildroot-fus now get their own version number to be more transparent and flexible.
 The Version numbers reflect the Version of the original package, if needed the NXP version and the
 F&S Version. For example the linux version name is composed like this

 [Version Orig. Kernel]-[Version IMX]-[Version FS]

 linux-v6.6.101-2.2.1-fus1.0

 This way it is easier to recognize the applied patch levels and the same package versions can
 be used in multiple releases.

 The actual packages versions are marked as annotated tags in the git history.
 The Name of the overall release (like fsimx93-Y2025.08) is still set as a light tag.

### 6. New CVE Tracker Tool fs-cve-tracker

 The F&S CVE Tracker Tool can help you to keep track of the current CVE status of your buildroot image.
 It will launch a local version of [Dependency Track](https://dependencytrack.org) and upload the SBOM
 of your Buildroot Build to it. Dependency Track will scan your SBOM for vulnerabilities, which can be downloaded in VEX
 format. The F&S CVE Tracker Tool can also be used to improve your VEX file by marking already fixed CVEs
 or sorting out CVEs which affect components that are not in your build configuration.

 You can also use Dependency Track to audit the remaining CVEs an generate Audit Reports for your documentation.

 For a quick start you can run the following command after your Buildroot Build has finished:

```bash
./setup-buildroot --cve-tracker
```

This command will install Dependency Track to your system, upload the SBOM from your build and improve your
vulnerabilities scan to sort out as many false positives as possible.

Please note that this may take a while on first run.

## Known Issues

SD-Card detect will not work correctly on the PCore-BBDSI Starterkit. If you want to test SD-Card, you can add
the device tree flag "broken-cd" to the sdcard-node. This will be fixed in the next BBDSI revision.

## Changelog

The following list shows the most noticeable changes in this release in
more detail since our last release for this platform. For a detailed description
please check the respective git histories.

### [u-boot-v2024.04-fus1.8](https://github.com/FSEmbedded/u-boot-fus/tree/v2024.04-fus1.8)

- Update to U-Boot version 2024.04
- Add OP-TEE Support per default
- Add Secure-Boot support per default
- Add option to group ATF/TEE with U-Boot image
- Improve boot from device environment handling

### [linux-v6.6.142-2.2.2-fus1.1](https://github.com/FSEmbedded/linux-fus/tree/v6.6.129-2.2.2-fus1.2)

- Merge fsimx8mm/mp/mn_defconfigs into single fsimx8_defconfig
- Update to version 6.6.129
- Fix OSM8MM USB host
- Fix fsimx8mm sdcard reset
- Remove unneeded Pull-Ups and Pull-Downs

### [buildroot-2025.02.15-fus1.0](https://github.com/FSEmbedded/buildroot-fus/tree/buildroot-2025.02.16-fus1.0)

- Improve fsmx8mm defconfigs
- Update ftom buildroot-2025.02.15 to buildroot-2025.02.16
- Fix Weston version selection and improve weston setup for init.d
- Add new boards and display devicetrees for fsimx8mm

### [atf-v2.10-fus1.4](https://github.com/FSEmbedded/atf-fus/tree/v2.10-fus1.4)

- Apply changes from lf-6.6.52-2.2.2

### [nboot-2026.03](https://github.com/FSEmbedded/meta-fus-nboot/tree/fsimx8mm-2026.03)

- Update to U-Boot version 2024.04

### [linux-examples-fus-fus1.1](https://github.com/FSEmbedded/linux-examples-fus/tree/fus1.1)

- Port ADC test tool to i.MX8MM using the recommended IIO framework
- Migrate gpio.c from deprecated sysfs to libgpiod
- Upgrade PWM control to Hz and percentage with polarity support

### Documentation

- [FSiMX8MM_FirstSteps_eng.pdf](https://www.fs-net.de/assets/download/docu/common/en/FSiMX8MM_FirstSteps_eng.pdf)
- [LinuxOnFSBoards_eng.pdf](https://www.fs-net.de/assets/download/docu/common/en/LinuxOnFSBoards_eng.pdf)

Please download the hardware documentation directly from our website.
Then you always have the newest version.

For further support please contact us in the [F&S Forum](https://forum.fs-net.de/)
