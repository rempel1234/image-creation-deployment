# How to create, update, and use a kickstart file for Oracle Linux 8

First off, if you just want to use this copy 

1. ks.cfg to the root directory of the ISO
1. isolinux.cfg to the isolinux directory of the ISO
1. grup.cfg to the EFI/BOOT directory of the ISO
1. make an EFI bootable ISO from that

Please note, if you didn't do anything to convert the updated folder to an ISO, it won't kickstart...

## Download the Oracle Linux 8 ISO

1. Browse to https://www.oracle.com/linux/technologies/oracle-linux-downloads.html
1. Click on **Oracle Linux yum server**
1. Scroll down to the most recent Oracle Linux 8 edition, select the full ISO
1. Download it

## Create a kickstart file for Oracle Linux 8

1. Install Oracle Linux with as close to the desired configuration as possible
1. Copy the /root/anaconda-kickstart.cfg
1. Extract the Oracle Linux 8 ISO
   ```
   mkdir OracleLinux-R8-U8
   cd OracleLinux-R8-U8
   isoinfo.exe -R -X -i ../OracleLinux-R8-U8-x86_64-dvd.iso
   # some dump reason it's read-only, so make a read-write copy
   cd ..
   cp OracleLinux-R8-U8 OracleLinux-R8-U8-copy
   cd OracleLinux-R8-U8-copy
   ```
1. edit the isolinux/isolinux.cfg to use the kickstart file
1. edit the EFI/BOOT/grub.cfg to use the kickstart file


## Creating the custom ISO

```
mkisofs -o ~/Downloads/ol8-test.iso \
-b isolinux/isolinux.bin -J -R -l -c isolinux/boot.cat \
-no-emul-boot -boot-load-size 4 \
-boot-info-table -eltorito-alt-boot -b images/efiboot.img \
-no-emul-boot -graft-points -joliet-long \
-V "OL-8-8-0-BaseOS-x86_64" .
```

### Install Requirements ###

https://docs.oracle.com/en/operating-systems/oracle-linux/8/install/install-PreparingToInstall.html#install-requirements


### Generating the anaconda.ks
