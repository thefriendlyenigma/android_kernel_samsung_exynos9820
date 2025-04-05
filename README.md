# Docker Configuration for EternityROM v4.0 for the Samsung S10e
A simple custom kernel built for [EternityROM](https://xdaforums.com/t/port-rom-14-eternityrom-v4-0-oneui-6-1-1-for-n10-s10-series.4670331/), a custom Android 14 ROM for the Exynos variant of the Samsung s10e. Made to be compatible for running Docker containers, following instructions from [here](https://github.com/ravindu644/Android-Kernel-Tutorials?tab=readme-ov-file#-customizing-the-kernel-permanent-method) and [the kernel section here](https://gist.github.com/FreddieOliveira/efe850df7ff3951cb62d74bd770dce27) .

Following the script specified, I've built the kernel with the respective flags enabled for Docker support, with the exception of:

- Optional Features
  - `CONFIG_CGROUP_HUGETLB` as one of its dependencies appears to be hard-set to "No" by the system, 
  - `CONFIG_EXT3_FS_XATTR`, as the option is not present in the kernel build options at all.
- Storage Drivers
  - Due to not intending to use either BTRFS or ZFS (and I'm not sure whether they would work anyway)
  - `CONFIG_BTRFS_FS`
  - `CONFIG_BTRFS_FS_POSIX_ACL`
  - zfs

## Installation
The tested method I have used is with the `odin4` Linux binary and a clean EternityROM v4.0 installed.

1. Have a clean EternityROM v4.0 installed on your S10e
2. Have adb installed on your PC and accessible to the PATH on the command line.
3. Have a working Odin installation and accessible to PATH on the command line. You can find this by searching.
4. Download `boot.img.tar` from the Releases section.
3. Enable Developer Settings from the Settings app, if you haven't already.
3. Enable USB Debugging.
4. Connect the S10e to your computer with a USB cable.
5. Accept the prompt to allow USB debugging from your PC.
6. Type in `adb reboot download` on your terminal.
7. Wait for the light blue "Downloading..." screen to appear on your S10e.
8. If using a Linux PC: open the directory `boot.img.tar` is inside with your terminal, then type in `odin4 -a boot.img.tar`
9. If using a Windows PC: open Odin, then select boot.img.tar in the AP section.
10. The device should flash, and then reboot.


## Building
Remains unchanged from the process described below: with your development environment ready (tested inside an Ubuntu 24.04 LTS container), clone the repo using the command:

``` shell
git clone --recurse-submodules https://github.com/thefriendlyenigma/android_kernel_samsung_exynos9820.git
```

Enter the resultant directory, then build with the command:

``` shell
./build.sh -m beyond0lte
```


# Original Readme Below
## ExtremeKernel for Exynos 9820 devices ##

### Features ###

- TBD

### Supported devices: ###

G970F - S10e - beyond0lte

G970N - S10e (Korean) - beyond0lteks

G973F - S10 - beyond1lte

G973N - S10 (Korean) - beyond1lteks

G975F - S10+ - beyond2lte

G975N - S10+ (Korean) - beyond2lteks

G977B - S10 5G - beyondx

G977N - S10 5G (Korean) - beyondxks

N970F - Note 10 - d1

N971N - Note 10 5G (Korean) - d1xks

N975F - Note 10+ - d2s

N976B - Note 10+ 5G - d2x

N976N - Note 10+ 5G (Korean) - d2xks

### Build instructions: ###

1. Set up build environment as per Google documentation

https://source.android.com/docs/setup/start/requirements

2. Properly clone repository with submodules (KernelSU and toolchains)

```git clone --recurse-submodules https://github.com/ExtremeXT/android_kernel_samsung_exynos9820.git```

3. Build for your device

```./build.sh -m beyond2lte```

4. Fetch the flashable zip of the kernel that was just compiled

```build/out/[your_device]/ExtremeKernel...zip```

5. Flash it using a supported recovery like TWRP

6. Enjoy!
