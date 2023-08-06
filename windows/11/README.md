# Notes for making a custom windows 11 image
## Extracting the ISO
```
7z x Win11_22H2_English_x64v2.iso -oWin11_22H2

```
## Update the AutoUnattend.xml

1. Mount the Windows 11 ISO
1. Create an empty folder and copy **D:\Sources\install.wim** into it
1. Uncheck the read-only square
1. Open Windows System Image Manager
1. Load the install.wim into it
1. Open the Autounattend.xml

https://www.elevenforum.com/t/create-custom-windows-11-iso-file.443/

https://www.windowsafg.com/win10x86_x64_uefi.html

https://schneegans.de/windows/unattend-generator/

https://www.youtube.com/watch?v=ZCDRDE5Uhp0

## Install the Unattend.xml
https://gist.github.com/asheroto/c4a9fb4e5e5bdad10bcb831e3a3daee6

## Make Win11 ISO
```
mkisofs   -no-emul-boot \
  -b "boot/etfsboot.com" \
  -boot-load-seg 0 \
  -boot-load-size 8 \
  -eltorito-alt-boot \
  -eltorito-platform efi \
  -no-emul-boot \
  -b "efi/microsoft/boot/efisys.bin" \
  -boot-load-size 1 \
  -iso-level 4 \
  -UDF \
  -o ~/Downloads/Win11_22H2-test.iso \
  .

```
