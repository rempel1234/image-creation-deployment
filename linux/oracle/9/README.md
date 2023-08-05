## Obtaining Oracle Linux 9

1. Follow the directions in https://docs.oracle.com/en/operating-systems/oracle-linux/9/install/install-AutomatinganOracleLinuxInstallationbyUsingKickstart.html
1. Download the from https://yum.oracle.com/oracle-linux-isos.html

## Installing mkisofs onto Windows

1. Install gitbash
1. Copy the cdrtfe bin files and cywin.dll into /usr/bin in gitbash

## Extracting the ISO
```

7z x OracleLinux-R9-U2-x86_64-dvd.iso -oOracleLinux-R9

```

## Where to put the .cfg's

```
cp ks.cfg OracleLinux-R9
cp isolinux.cfg OracleLinux-R9/isolinux
cp grub.cfg OracleLinux-R9/EFI/BOOT
```

## Generating the ISO

```
mkisofs -o ~/Downloads/ol9-2test.iso \
-b isolinux/isolinux.bin -J -R -l -c isolinux/boot.cat \
-no-emul-boot -boot-load-size 4 \
-boot-info-table -eltorito-alt-boot -b images/efiboot.img \
-no-emul-boot -graft-points -joliet-long \
-V "OL-9-2-0-BaseOS-x86_64" .
```
