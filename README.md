# F&S i.MX6SX  Buildroot Release 2026.06 (fsimx6sx-B2026.05)

This is a major release for F&S modules based on the i.MX6SX SoC,
based on the [NXP lf-6.6.52-2.2.2 release](https://www.nxp.com/docs/en/release-note/RN00210_LF6.6.52_2.2.2.pdf).

**Supported Boards**

- efusA9X
- efusA9Xr2
- PicoCoreMX6SX
- PicoCOMA9X

Please see the new revision of following file

  [FSiMX6SX_FirstSteps_eng.pdf](https://www.fs-net.de/assets/download/docu/common/en/FSiMX6SX_FirstSteps_eng.pdf)

for a description of how everything is installed and used. This doc
sub-directory also contains other documentation, for example about the
hardware of the boards and the starter kits.

Please note that Buildroot releases use a 'B' for the version number. The
version counting is independent form other releases.

## Content

The release consists of the following files and directories:

| File                    | Purpose                                                 |
| ------------------------| --------------------------------------------------------|
| README.md               | Release notes                                           |
| setup-buildroot         | Script to download and install the Buildroot release    |
| helper-setup-buildroot  | Helper script for setup-buildroot                       |
| fs-release-manifest.xml | Release Manifest, containing the used versions          |
| binaries/               | Precompiled images (full names)                         |
| sdcard/                 | Precompiled images (names as expected by install script)|
| doc/                    | Manuals and documentation                               |
| sbom/                   | SBOMs of release binaries in SPDX and CycloneDX format  |
| dl/                     | Firmware packages provided locally to buildroot         |

**Warning**
The precompiled images are for testing and evaluation purposes only!
DO NOT USE in production or mission-critical environments!

## How to build

Use the latest F&S Development Machine from the [F&S website](https://www.fs-net.de/)
To build the example release binaries, run:

```bash
git clone -b fsimx6-B2026.05 https://github.com/FSEmbedded/releases-fus.git
cd releases-fus
./setup-buildroot <build_dir>
./setup-buildroot --docker <build_dir>
cd buildroot-fus
make fsimx6_wayland_defconfig
make
```

## Highlights

Here are some highlights of this release.

### 1. New Linux Kernel 6.6.129

The Linux kernel is now based on 6.6.129, which offers several new bug and security fixes.

### 2. New LTS Buildroot version 2025.02.13

Buildroot now has a 3-year LTS cycle starting with 2025.02 with a patch level upgrade aproximatly every month.

Since the last release most packages have been updated to more current versions and sbom support has been implemented.

### 3. Improve linux-examples-fus

Update the examples to the new linux version.

### 4. New Docker based building system

 The F&S releases now support Docker containers as default building machines.
 By using the Docker environment, the build process can be executed on any Linux host,
 as long as the Docker is installed.
 Starting FS_Development_Machine-Fedora-40_V0.3 Docker will be pre-installed and the
 development machines will not support support building the releases directly anymore.

 If you do not want to use Docker, please check the Dockerfile for the dependencies.
 https://github.com/FSEmbedded/docker-fus/

 1. Download manifest repository

    ```sh
    git clone -b fsimx6-B2026.05 https://github.com/FSEmbedded/releases-fus.git
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

## Changelog

The following list shows the most noticeable changes in this release in
more detail since our last release for this platform. For a detailed description
please check the respective git histories.

### [u-boot-v2021.04-fs1.4](https://github.com/FSEmbedded/u-boot-fus/tree/v2021.04-fs1.4)

- Fix several open CVEs

### [linux-v6.6.129-2.2.2-fus1.4.1](https://github.com/FSEmbedded/linux-fus/tree/v6.6.129-2.2.2-fus1.4.1)

- Unify defconfigs of fsimx6, fsimx6l and fsimx6sx
- Fix Power Managent warning regarding fsimx6sx Boards without GPU
- Add Silex driver for Linux 6.6

### [buildroot-2025.02.13-fus1.1](https://github.com/FSEmbedded/buildroot-fus/tree/buildroot-2025.02.13-fus1.1)

- Improve fsimx6sx defconfigs
- Improve imx-gstreamer recipes for Linux 6.6
- Improve silex-wlanbt-fs package for Linux 6.6

### [linux-examples-fus-fus1.1](https://github.com/FSEmbedded/linux-examples-fus/tree/fus1.1)

- Port ADC test tool to i.MX8MM using the recommended IIO framework
- Migrate gpio.c from deprecated sysfs to libgpiod
- Upgrade PWM control to Hz and percentage with polarity support

### nbootimx6_51.bin (VN51)

(no changes)

### Documentation

- [FSiMX6SX_FirstSteps_eng.pdf](https://www.fs-net.de/assets/download/docu/common/en/FSiMX6SX_FirstSteps_eng.pdf)
- [LinuxOnFSBoards_eng.pdf](https://www.fs-net.de/assets/download/docu/common/en/LinuxOnFSBoards_eng.pdf)

Please download the hardware documentation directly from our website.
Then you always have the newest version.

For further support please contact us in the [F&S Forum](https://forum.fs-net.de/)

