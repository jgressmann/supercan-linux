# SuperCAN Linux kernel module

This repository contains the Linux kernel driver code for [SuperCAN](https://github.com/jgressmann/supercan), an open source USB to CAN-FD protocol.

_NOTE: the code in this repository requires sources from the SuperCAN repository. It will not build if cloned by itself._

The main branch of this repository aims to stay compatible with the mainline Linux kernel. Branches for older kernels exist and are somewhat maintained.

## Building the kernel module

### DKMS setup

Install `dkms` if you haven't already, for instance
```
sudo apt-get install dkms
```


### Checkout the branch matching your kernel version

You may need to checkout the proper branch to build the driver module.

The command `uname -r` will tell you what kernel version is currently running.
The output will be something like `5.10.0-28-generic` which would indicate kernel version `5.10`.

Checkout the branch matching your kernel version, e.g. `git checkout pre-v5.11`.
To get a list of the available branches, run `git branch -a`.


### Setup the kernel module sources

```
<path to supercan>/Linux/dkms-init.sh
```

### Add, build & install the kernel module

```
sudo dkms add <path to supercan>/Linux/supercan_usb-<version>
sudo dkms build supercan_usb/<version>
sudo dkms install supercan_usb/<version>
```

### Uninstall and remove the kernel module

```
sudo dkms uninstall supercan_usb/<version>
sudo dkms remove supercan_usb/<version> --all
```

