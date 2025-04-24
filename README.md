<div align="center">
<a href="https://dawndrums.tn"><img title="dawnwos" src="assets/dawnos.png" width="50%"/></a>
</div>

## Overview

This is the main repository for DawnOS. By following the guidelines, you should be able to create a full DawnOS image from source.

## Prerequisites
Install necessary build tools and toolchain

```
sudo apt-get install device-tree-compiler libncurses5 libncurses5-dev build-essential libssl-dev mtools bc python dosfstools
```

## Build
Script and configuration files are under `build` to build u-boot, kernel and rootfs.
```
git clone -b dawnos https://github.com/dawndrums/build.git
```
## Bootloader
```
git clone https://github.com/dawndrums/rkbin.git
git clone https://github.com/dawndrums/u-boot.git
```
You should get the following the folders
```
build rkbin u-boot
```

Build u-boot for divine d.

```
./build/mk-uboot.sh divine-d.
```
This will generate images under `out/u-boot`
```
ls out/u-boot
```
This should output
```
idbloader.img  rk3588_spl_loader_vx.xx.xxx.bin  spi  uboot.img u-boot.itb
```
The SPI content is only used to flash the on-board SPI flash, used for SBCs. Divine D. won't include any SPI flash, but we left it for legacy and in case it's useful. 
`idbloader.img` and `u-boot.itb` (`uboot.img` is the combination of both) are used to add u-boot to the full image at the correct sector addresses.
In the case the bootloader needs to be changed. It can be done by either alter the flashed image on a storage medium (i.e., sdcard) as :
```
sudo dd if=./idbloader.img of=/path/to/storage bs=512 seek=64
sudo dd if=./u-boot.itb of=/path/to/storage bs=512 seek=16384
```
Or by flashing using `rkdeveloptool`, for example the eMMC, under Maskrom mode:

```
sudo rkdeveloptool db rk3588_spl_loader_vx.xx.xxx.bin
sudo rkdeveloptool wl 64 out/u-boot/idbloader.img
sudo rkdeveloptool wl 16384 out/u-boot/u-boot.itb
```

## Kernel
WIP
## Rootfs and DawnOS Image
WIP
