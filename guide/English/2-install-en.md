<img align="right" src="https://github.com/PhucHauDeveloper/Port-Windows-11-Xiaomi-Mi-Mix-2s/blob/b71fde07677d753897aa44eaec1914f54c57cede/guide/png/Xiaomi%20Mi%20Mix%202s%20Windows.png?raw=true" width="350" alt="Windows 11 Running On A Xiaomi Mi Mix 2s">


# Running Windows on the Xiaomi Mi Mix 2s

## Installation

## Installing Windows

### Prerequisites

- Only releases, I put everything you need in it!
- I highly recommend using a good connection cable or at least it's stable otherwise you'll need to read the device recovery guide!


### Flash the uefi image
> If you already have TWRP or any else custom recovery installed, just hold the power and vol+ buttons at startup

```cmd
fastboot flash boot uefi.img
```

#### Enter Mass Storage

> Note: In UEFI boot:
> 
>+ Volume up button is to move up (vertical menu) or move left.
>
>+ The volume down button is for scrolling down (vertical menu) or scrolling right.
>
>+ Power button to select.

After rebooting the phone, use the volume button (volume down button) to enter the UEFI menu, then press the power button twice to enter the full menu, then press the volume down button four times (to move to "Mass Storage"). Press the power button to select, then press volume down to move to the. Press the power button to select. Now you can plug in the computer to proceed to the next step.

### Install

> Using the Partition Wizard(in soft folder), select the esp partition and change the letter to whatever you want (E, F, G, H, etc) 

> Then open Dism++ inside the folder I built.Click "Select file" in the upper right corner of the program, click "Apply image", now select install.win file from working directory. Then select the partition that shows up when you plug your phone in mass storage mode. Click "ok" to proceed with the flash, this process will take from 10-60 minutes depending on the device, go make a cup of coffee and stay away from the connection cable if you do not want to redo this process.


### Install Drivers

> In DISM++, after flashing there will be an open session line on the screen, click on it, select the driver section, press add and navigate to the driver folder. Note that you should use my driver if you don't want usb errors later. Wait a moment for the process to complete


### Create Windows bootloader files for the EFI

>Copy EFI file (using explorer++ in tool folder) to the ESP partition. Then reboot your device and enjoy the result.
  

## Boot into Windows
>Flash UEFI to enter windows
```cmd
fastboot flash boot uefi.img
```

## Boot back into Android
> Use your backup boot image from TWRP

### If you don't want to do these to convert android and windows side by side, read dualboot guide

## Finished!
