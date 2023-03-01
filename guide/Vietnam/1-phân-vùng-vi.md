<img align="right" src="https://github.com/PhucHauDeveloper/Port-Windows-11-Xiaomi-Mi-Mix-2s/blob/b71fde07677d753897aa44eaec1914f54c57cede/guide/png/Xiaomi%20Mi%20Mix%202s%20Windows.png?raw=true" width="350" alt="Windows 11 Running On A Xiaomi Mi Mix 2s">


# Running Windows on the Xiaomi Mi Mix 2s

## Installation

## Partitioning your device

### Prerequisites

- Only releases, I put everything you need in it!

### Notes:
> **Warning** if you delete any partitions via diskpart later on or now windows will send a ufs command that gets misinterpreted which erase all your ufs
- All your data will be erased! Backup now if needed.
- These commands have been tested.
- Ignore `udevadm` warnings
- Do not run the same command twice
- DO NOT REBOOT YOUR PHONE if you think you made a mistake, ask for help in the [Facebook](https://www.facebook.com/ThaiHoangPhucHau/)

#### ⚠️ Do not run all commands at once, execute them in order!

##### ⚠️ DO NOT MAKE ANY MISTAKE!!! YOU CAN BREAK YOUR DEVICE WITH THE COMMANDS BELOW IF YOU DO THEM WRONG!!!

#### First hold shift + right click on the folder, select "Open in Terminal" if you don't want flashboot error

```cmd
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\usbflags\18D1D00D0100" /v "osvc" /t REG_BINARY /d "0000" /f
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\usbflags\18D1D00D0100" /v "SkipContainerIdQuery" /t REG_BINARY /d "01000000" /f
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\usbflags\18D1D00D0100" /v "SkipBOSDescriptorQuery" /t REG_BINARY /d "01000000" /f
```

##### Boot TWRP recovery through the PC with the command
```cmd
fastboot boot <twrp.img>
```

#### Unmount all partitions
Go to TWRP settings and unmount all partitions

#### Start ADB shell
```cmd
adb shell
```

#### Resize the partition table
> So that the Windows partitions can fit
```sh
sgdisk --resize-table 64 /dev/block/sda
```

#### Start parted
```sh
parted /dev/block/sda
```


#### Delete the `userdata` partition
> You can make sure that 32 is the userdata partition number by running
>  `print all`
```sh
rm 21
```

#### Create partitions
> If you get any warning message telling you to ignore or cancel, just type i and enter



<details>
<summary><b><strong>For 64GB Models</strong></b></summary>

  
  - Create the ESP partition (stores Windows bootloader data and EFI files)
```sh
mkpart esp fat32 6559MB 7000MB
```

- Create the main partition where Windows will be installed to
```sh
mkpart win ntfs 7000MB 40GB
```
  
- Create Android's data partition
```sh
mkpart userdata ext4 40GB 59.1GB
```

  </summary>
</details>


<details>
<summary><b><strong>For 128GB Models</strong></b></summary>


- Create Android's data partition
```sh
mkpart userdata ext4 11.8GB 68.6GB
```

- Create the main partition where Windows will be installed to
```sh
mkpart win ntfs 68.6GB 126GB
```

- Create the ESP partition (stores Windows bootloader data and EFI files)
```sh
mkpart esp fat32 126GB 127GB 
```
  </summary>
</details>

<details>
<summary><b><strong>For 256GB Models</strong></b></summary>


- Create Android's data partition
```sh
mkpart userdata ext4 11.8GB 134.6GB
```

- Create the main partition where Windows will be installed to
```sh
mkpart win ntfs 134.6GB 254GB
```

- Create the ESP partition (stores Windows bootloader data and EFI files)
```sh
mkpart esp fat32 254GB 255GB
```
  </summary>
</details>

#### Make ESP partiton bootable so the EFI image can detect it
```sh
set 21 esp on
```

#### Quit parted
```sh
quit
```

#### Reboot to TWRP

#### Start the shell again on your PC
```cmd
adb shell
```

#### Format partitions
-  Format the ESP partiton as FAT32
```sh
mkfs.fat -F32 -s1 /dev/block/by-name/esp
```

-  Format the Windows partition as NTFS
```sh
mkfs.ntfs -f /dev/block/by-name/win
```

- Format data
```sh
mkfs.ntfs -f /dev/block/by-name/win
```
Or go to Wipe menu(twrp) and press Format Data, 
then type `yes`.

#### Check if Android still starts
Just restart the phone, and see if Android still works


## [Next step: Installing Windows](/guide/English/2-install-en.md)
