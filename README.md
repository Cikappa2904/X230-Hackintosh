# macOS on ThinkPad X230


[![ThinkPad](https://img.shields.io/badge/ThinkPad-X230-blue.svg)](https://psref.lenovo.com/syspool/Sys/PDF/withdrawnbook/ThinkPad_X230.pdf)
[![MacOS Catalina](https://img.shields.io/badge/Catalina-10.15-red.svg)](https://www.apple.com/)
[![MacOS Big Sur](https://img.shields.io/badge/Big_Sur-11.6.2-blue.svg)](https://www.apple.com/macos/big-sur/)
[![Release](https://img.shields.io/badge/Download-latest-brightgreen.svg)](https://github.com/Cikappa2904/X230-Hackintosh/releases/latest)
[![OpenCore](https://img.shields.io/badge/OpenCore-0.7.3-blue.svg)](https://github.com/acidanthera/OpenCorePkg/releases/0.7.3)




## READ THE ENTIRE README.MD BEFORE YOU START

### I am not responsible for any damages you may cause

- Complete EFI packs are available in the releases page.
- Please **do not clone or download** the main branch for daily use: it may include **unstable code** just because it is my repository.
- This EFI works with Big Sur, should work with Catalina (Monterey has some problems)
- With every EFI update you retrieve from here please remember to go through the post install guide.



<details>
<summary><strong> SUMMARY </strong></summary>
<br>

> ### Non-Fuctional

| Feature                              | Status | Dependency          |
| :----------------------------------- | ------ | ------------------- |
| Fingerprint Reader                   | ❌   | `DISABLED` in BIOS to save power. |
| Wireless WAN                         | ❌   | `DISABLED` in BIOS to save power. |
| VGA Port                             | ❌   | Does not exist on real apple computers. |

> ### Video and Audio

| Feature                              | Status | Dependency          |
| :----------------------------------- | ------ | ------------------- |
| Full Graphics Accleration (QE/CI)    | ✅   | `WhateverGreen.kext`  |
| Audio Recording                      | ✅   | `AppleALC.kext` with Layout ID = 55 and `SSDT-HPET.aml`   |
| Audio Playback                       | ✅   | `AppleALC.kext` with Layout ID = 55 and `SSDT-HPET.aml`   |
| Automatic Headphone Output Switching | ✅   | `AppleALC.kext` with Layout ID = 55 and `SSDT-HPET.aml`   |
| Dock Audio Port                      | ✅   | `AppleALC.kext` with Layout ID = 55 and `SSDT-HPET.aml`   |

> ### Power, Charge, Sleep and Hibernation

| Feature                              | Status | Dependency          |
| :----------------------------------- | ------ | ------------------- |
| Battery Percentage Indication        | ✅   | `ECEnabler.kext`            | 
| iGPU Power Management                | ✅   | `XCPM`, enabled by [`SSDT-PM.aml`](https://github.com/Piker-Alpha/ssdtPRGen.sh) |
| S3 Sleep/ Hibernation Mode 3         | ✅   | `SSDT-PWTK.aml` |  |   
| Custom Charge Threshold              | ✅   | `SSDT-EC.aml`, [YogaSMC.kext](https://github.com/zhen-zen/YogaSMC), and [YogaSMCPane](https://github.com/zhen-zen/YogaSMC)|
| Fan Control                          | ✅   | `SSDT-EC.aml`, [YogaSMC.kext](https://github.com/zhen-zen/YogaSMC), and [YogaSMCPane](https://github.com/zhen-zen/YogaSMC)|
| Battery Life                         | ✅   | Native, comparable to Windows/Linux. |

> ### Input/ Output

| Feature                              | Status | Dependency          |
| :----------------------------------- | ------ | ------------------- |
| WiFi                                 | ✅   | `AirportItlwm.kext`  |
| Bluetooth                            | ✅   | `IntelBluetoothFirmware.kext`  |
| Ethernet                             | ✅   | `IntelMausi.kext`  |
| USB 2.0, USB 3.0                     | ✅   | `USBPorts.kext`    |
| USB Power Properties in macOS        | ✅   | `SSDT-EC-USBX.aml` |

> ### Display, TrackPad, TrackPoint, and Keyboard

| Feature                              | Status | Dependency          |
| :----------------------------------- | ------ | ------------------- |
| Brightness Adjustments | ✅  | `WhateverGreen.kext`, `SSDT-PNLF.aml` and `BrightnessKeys.kext`|
| TrackPoint             | ✅  | `VoodooPS2Controller.kext` |
| TrackPad               | ✅  | `VoodooPS2Controller.kext` |
| Built-in Keyboard      | ✅  | `VoodooPS2Controller.kext` |
| Multimedia Keys        | ✅  | `BrightnessKeys.kext` and [YogaSMC](https://github.com/zhen-zen/YogaSMC) |

> ### macOS Continuity

| Feature                              | Status | Dependency          |
| :----------------------------------- | ------ | ------------------- |
| iCloud, iMessage, FaceTime           | ✅   | Whitelisted Apple ID, Valid SMBIOS  |
| AirDrop                              | ✅   | Not tested  |
| Time Machine                         | ✅   | Native  |

</details>

<details>
<summary><strong> REFERENCES </strong></summary>
<br>

Read these before you start:

- [dortania's Hackintosh guides](https://github.com/dortania).
- [dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/).
- [dortania's OpenCore Post Install Guide](https://dortania.github.io/OpenCore-Post-Install/).
- [dortania/ Getting Started with ACPI](https://dortania.github.io/Getting-Started-With-ACPI/).
- [dortania/ opencore `multiboot`](https://github.com/dortania/OpenCore-Multiboot).
- [dortania/ `USB map` guide](https://dortania.github.io/OpenCore-Post-Install/usb/).
- [WhateverGreen Intel HD Manual](https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md).
- `Configuration.pdf` and `Differences.pdf` in each `OpenCore` releases.

</details>

<details>
<summary><strong> REQUIREMENTS </strong></summary>
<br>

- A macOS machine(optional): to create the macOS installer.
- Flash drive, 12GB or more, for the above purpose.  
- Xcode works fine for editing plist files on macOS, but I prefer [PlistEdit Pro](https://www.fatcatsoftware.com/plisteditpro/).  
- [ProperTree](https://github.com/corpnewt/ProperTree) if you need to edit plist files on Windows.  
- [MaciASL](https://github.com/acidanthera/MaciASL), for patching ACPI tables and editing ACPI patches.
- [MountEFI](https://github.com/corpnewt/MountEFI) to quickly mount EFI partitions.  
- [IORegistryExplorer](https://developer.apple.com/downloads), for diagnosis.  
- [Hackintool](https://www.insanelymac.com/forum/topic/335018-hackintool-v286/), for diagnostic ONLY, Hackintool should not be used for patching, it is outdated.
- Patience and time, especially if this is your first time Hackintosh-ing.

</details>

<details>
<summary><strong> HARDWARE </strong></summary>
<br>

| Category  | THINKPAD X230            | THINKPAD T530            | THINKPAD T430s            |
| --------- | ------------------------ | ------------------------ | ------------------------- |
| CPU       | Intel Core i5-3320M      | Intel Core i5-3320M      |  Intel Core i7-3520M      |
| SSD       | Samsung 870 Evo 250GB    | SanDisk A400 256GB       |  Samsung 870 Evo 256GB    |
| Display   | 12.5' IPS HD (1366x1768) | 15.6' TN FHD (1920x1080) |  14' TN HD+ (1600x900)    |
| WiFi & BT | Intel Wireless-AC 7260   | DW1550 (BCM94352HMB)     |  Intel Centrino N-6205    |

- Refer to [X230-Platform_Specifications](https://psref.lenovo.com/syspool/Sys/PDF/withdrawnbook/ThinkPad_X230.pdf) for possible stock ThinkPad X230 configurations.

</details>

<details>
<summary><strong> GETTING STARTED </strong></summary>
<br>

Before you do anything, please familiarize yourself with basic Hackintosh terminologies and the basic Hackintosh process by throughly reading Dortania guides as linked in `REFERENCES`

- Creating a macOS installer: refer to [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)
- [**README-HARDWARE**](/Other/README_HARDWARE.md): Requirements before installing.
- [**README-OTHERS**](/Other/README_OTHERS.md): for post installation settings and other remarks.

</details>



> ## CONTACT

- Email: 2904cikappa@gmail.com

> ## SUPPORT

<details>
<summary><strong> CREDITS </strong></summary>
<br>

- [Apple](https://www.apple.com) for macOS.
- [Acidanthera](https://github.com/acidanthera) for all the kexts/utilities that they made.
- [Rehabman](https://github.com/RehabMan) and [Daliansky](https://github.com/daliansky) for the patches and guides and kexts.
- [George Kushnir](https://github.com/n4ru) for modified BIOS.
- [Dortania](https://github.com/dortania) for for the OpenCore Install Guide.
- [simprecicchiani](https://github.com/simprecicchiani) for inspirational ThinkPad configurations.
- [zhen-zen](https://github.com/zhen-zen) for **YogaSMC**.
- [banhbaoxamlan](https://github.com/banhbaoxamlan/X230-Hackintosh) for the original EFI

</details>
