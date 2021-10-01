# labrador-linux5-64
Linux 5 kernel source code for "Caninos Labrador v3.0".

## Release Notes
Experimental!

## About
This repository contains the source code of Caninos Labrador's 64bits linux
kernel. Boards newer than "Labrador Core v3.0" should work fine with this
kernel.

## Usage
Prior to compilation, make sure you have the following libraries and/or
tools installed on your machine:
1) GNU Binutils environment
2) Native GCC compiler
3) GCC cross-compiler targeting "gcc-aarch64-linux-gnu"
4) Make build tool
5) Git client
6) Bison and Flex development libraries
7) NCurses development libraries
8) LibSSL development libraries

```
$ sudo apt-get update
$ sudo apt-get install build-essential binutils gcc-aarch64-linux-gnu make git
$ sudo apt-get install bison flex libncurses-dev libssl-dev
```

After installing these tools, clone this repository in your computer.
Then, go to it's main directory and execute it's makefile.

```
$ git clone https://github.com/caninos-loucos/labrador-linux5-64.git
$ cd labrador-linux5-64 && make
```

## Incremental Build
If you want to do an incremental build, execute the following commands:

1) To load "Labrador Core v3.0"'s configuration
```
make config
```
>Note: this will overwrite all configurations already set up.

2) To change which modules are compiled into your kernel image
```
make menuconfig
```
3) To compile the device tree binary blob
```
make dtbs
```
4) To compile your kernel image
```
make kernel
```
5) To reset everything
```
make clean
```

## Kernel Installation
After a successful build, the kernel should be avaliable at "output" folder.
The modules are located at "output/lib/modules". Do the following:

1) Copy the modules to the folder "/lib/modules" at your SDCARD/EMMC system's
root.

```
$ sudo cp -r output/lib/modules $ROOTFS/lib/
```

2) Copy the Image file to the "/boot/" folder at your SDCARD/EMMC system's root.

```
$ sudo cp output/Image $ROOTFS/boot/
```

3) Copy the device tree files to "/boot/" folder at your SDCARD/EMMC
system's root.

```
$ sudo cp output/v3psci.dtb $ROOTFS/boot/
```
>Note: $ROOTFS must be replaced by the complete directory path of your target
system's root mounting point.

## Bootloader Installation

1) To update the bootloader in a SDCARD use:
```
$ sudo dd if=bootloader.bin of=/dev/$DEVNAME conv=notrunc seek=1 bs=512
```

> Note: $DEVNAME is the name of the target device. It is not a partition name.
You can use lsblk, to know it's name. The file "bootloader.bin" is located at 
the folder "boot" of this repository.

2) To update the EMMC's bootloader from a live Linux system booted from SDCARD 
use:
```
$ sudo dd if=bootloader.bin of=/dev/mmcblk2 conv=notrunc seek=1 bs=512
```

3) The bootloader uses the configuration file "config.json". A sample is located 
at the folder "boot" of this repository. It must be copied to the folder 
"/boot/" of your SDCARD/EMMC system's root. 
To copy this file to your system use:
```
$ sudo cp config.json $ROOTFS/boot/
```
>Note: $ROOTFS must be replaced by the complete directory path of your target
system's root mounting point.

## Contributing

**Caninos Loucos Forum: <https://forum.caninosloucos.org.br/>**

**Caninos Loucos Website: <https://caninosloucos.org/>**

