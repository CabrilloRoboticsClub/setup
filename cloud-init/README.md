# cloud-init Configuration for Dev Disks 

This is the customization of the developer disks. 

## Image Preparation 

From a fresh install of Ubuntu do the following. 

### Install cloud-init

```console
$ sudo apt update -y && sudo apt install -y cloud-init
```

### Bugfix 

cloud-init has a bug on Desktop systems: 

https://bugs.launchpad.net/cloud-init/+bug/2008952

The workaround is to apply the patch in this directory:

```console
sudo patch -d /usr/lib/systemd/system/ -p0  < cloud-init.service.patch 
```

### Update the Kernel Commandline 

Add the URL to the kernel commandline: 

```console
$ sudo patch -d /etc/default -p0  < grub.patch
$ sudo update-grub 
```

### Re-Run cloud-init 

If you make a mistake this command will run `cloud-init` on the next boot:

```console
$ sudo cloud-init clean --logs
```

## Data
 
Both `meta-data` and `user-data` MUST be present in this directory. 
