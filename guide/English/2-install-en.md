<img align="right" src="https://github.com/PhucHauDeveloper/Port-Windows-11-Xiaomi-Mi-Mix-2s/blob/b71fde07677d753897aa44eaec1914f54c57cede/guide/png/Xiaomi%20Mi%20Mix%202s%20Windows.png?raw=true" width="350" alt="Windows 11 Running On A Xiaomi Mi Mix 2s">


# Running Windows on the Xiaomi Mi Mix 2s

## Installation

## Installing Windows

### Prerequisites

- Only releases, I put everything you need in it!
### Flash the uefi image from TWRP/or 
> If you already have TWRP/any else custom recovery installed, just hold the power and vol+ buttons at startup

```cmd
fastboot flash boot uefi.img
```

#### Enter Simple Init
> Reboot phone,
> ##############################################
  

### Assign letters to disks
  

#### Start the Windows disk manager

> Once the X3 Pro is detected as a disk

```cmd
diskpart
```


### Assign `X` to Windows volume

#### Select the Windows volume of the phone
> Use `list volume` to find it, it's the one named "WINVAYU"

```diskpart
select volume <number>
```

#### Assign the letter X
```diskpart
assign letter=x
```

### Assign `Y` to esp volume

#### Select the ESP volume of the phone
> Use `list volume` to find it, it's the one named "ESPVAYU"

```diskpart
select volume <number>
```

#### Assign the letter Y

```diskpart
assign letter=y
```

#### Exit diskpart
```diskpart
exit
```

  
  

### Install

> Replace `<path/to/install.wim>` with the actual install.wim path,

> `install.wim` is located in sources folder inside your ISO
> You can get it either by mounting or extracting it

```cmd
dism /apply-image /ImageFile:<path/to/install.wim> /index:1 /ApplyDir:X:\
```

### Check what type of panel you have

> Open cmd

```cmd
adb shell cat /proc/cmdline
```
> Look for `msm_drm.dsi_display0` almost at the bottom

> If your device is `Tianma` `msm_drm.dsi_display0` will be `dsi_j20s_36_02_0a_video_display`

> If your device is `Huaxing` `msm_drm.dsi_display0` will be `dsi_j20s_42_02_0b_video_display`, if it is, go to the drivers folder `Vayu-Drivers/components/QC8150/Device/DEVICE.SOC_QC8150.VAYU/Drivers/Touch/` and delete `j20s_novatek_ts_fw01.bin`, finally rename `j20s_novatek_ts_fw02.bin` to `j20s_novatek_ts_fw01.bin`

### Install Drivers

> Replace `<vayudriversfolder>` with the location of the drivers folder

```cmd
driverupdater.exe -d <vayudriversfolder>\definitions\Desktop\ARM64\Internal\vayu.txt -r <vayudriversfolder> -p X:
```

  

### Create Windows bootloader files for the EFI

```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

  
  

## Allow unsigned drivers

> If you don't do this you'll get a BSOD

```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set {default} testsigning on
```

## Boot into Windows

### Move the `<uefi.img>` file to the device

```cmd
adb push <uefi.img> /sdcard
```

#### if you have a microSD card use this

```cmd
adb push <uefi.img> /external_sd
```


### Make a backup of your existing boot image
> You need to do it just once

> Put it to the microSD card if possible


### Flash the uefi image from TWRP
Navigate to the `uefi.img` file and flash it into boot

## Boot back into Android
> Use your backup boot image from TWRP

## Finished!
