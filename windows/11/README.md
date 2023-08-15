# Notes for making a custom windows 11 image

## Pare down to one Windows 11 image

Get the list of images available

```

Dism /Get-WimInfo /WimFile:"c:\iso_files\sources\install.wim"

...

Index : 10
Name : Windows 11 Pro for Workstations
Description : Windows 11 Pro for Workstations
Size : 16,781,355,713 bytes

```

Select the desired image

```
Dism /export-image /SourceImageFile:c:\iso_files\sources\install.wim /SourceIndex:10 /DestinationImageFile:c:\iso_files\install.wim /Compress:max /CheckIntegrity
```

Overwrite the image

```
move c:\ISO_Files\install.wim c:\ISO_Files\sources\install.wim
...
Overwrite c:\ISO_Files\sources\install.wim? (Yes/No/All): yes
        1 file(s) moved.
```

Verify there's only one edition left

```

Dism /Get-WimInfo /WimFile:"c:\iso_files\sources\install.wim"

Deployment Image Servicing and Management tool
Version: 10.0.22621.1

Details for image : c:\iso_files\sources\install.wim

Index : 1
Name : Windows 11 Pro for Workstations
Description : Windows 11 Pro for Workstations
Size : 16,781,355,713 bytes

The operation completed successfully.

```

Finally, generate the .iso
```
oscdimg.exe -m -o -u2 -udfver102 -bootdata:2#p0,e,bc:\iso_files\boot\etfsboot.com#pEF,e,bc:\iso_files\efi\microsoft\boot\efisys.bin c:\iso_files c:\MyISO.iso
```


























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
