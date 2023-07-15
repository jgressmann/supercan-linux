# Devel Kernel Module

## Building

Install `dkms` if you haven't already. This will take care of installing the headers for your kernels.

Then, from `Linux/supercan_usb-x.y.z`, do

```
make V=1 KERNELRELEASE=$(uname -r) -C /lib/modules/$(uname -r)/build M=$PWD
```


## Signing


If you are using secure boot or locked down kernel you might need to sign the kernel module prior to loading.

This works for Ubuntu 21.10:

```
sudo kmodsign sha512 \
	/var/lib/shim-signed/mok/MOK.priv \
    /var/lib/shim-signed/mok/MOK.der \
	$PWD/supercan_usb.ko

```



## Loading


```
sudo modprobe can-dev
sudo rmmod supercan_usb 2>/dev/null || true && sudo insmod $PWD/supercan_usb.ko
```

