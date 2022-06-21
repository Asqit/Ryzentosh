# Ryzentosh

_an opencore configuration for AMD based systems_

![finder>about this mac](about.png)

## Specs

| Type    | Name                            |
| ------- | ------------------------------- |
| CPU     | AMD Ryzen 5 5600x               |
| GPU     | Sapphire RX570 4GB (downgraded) |
| MB      | Asus B450MK                     |
| RAM     | 16GB ddr4 2666Mhz               |
| AUDIO   | Realtek ALC887                  |
| NETWORK | Realtek RTL811H                 |
| SSD     | Adata SX6000NP                  |
| BIOS    | 3211 (downgraded)               |

## BIOS settings

Its crucial part of success. These are recomended settings for running MacOS on regular beige PC.

**Disable:**

- fast boot
- com/serial/parallel
- secure boot
- resize bar

**Enable:**

- 4G decoding
- SATA operations to AHCI

## Installation

**WARNING:Continue on your own risk. I share my config with no waranty. If anything happens to your iron, its not on me**

### Edit of `config.plist`

I recommend using `OCAuxiliaryTools` or `propertree` as config editor.

**Kernel**

If your core count differs from mine, then your should edit three lines in `kernel > patch`. Edits are following:

1. `B8 06 0000 0000`
2. `BA 06 0000 0000`
3. `BA 06 0000 0000`

The edits are simple, there are in `HEX` format. here is the syntax: `BX <phys core count> 0000 0000`

<details>
<summary>HEX TABLE</summary>

| DEC | HEX |
| --- | --- |
| 2   | 02  |
| 4   | 04  |
| 6   | 06  |
| 8   | 08  |
| 12  | 0C  |
| 16  | 10  |
| 24  | 18  |
| 32  | 20  |
| 64  | 40  |

</details>

**elsewhere**

You do best if you check recomended settings for your chipset. Since mine is B450, I don't need `SSDT-CPUR.aml` and I also have different settings elsewhere.
Check best settings for yourself [here](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)

**PlatformInfo**

It is **required** that you generate yourself new SMBIOS information, so that there won't be conflict. Use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) utility or [OCAuxiliaryTools](https://github.com/ic005k/OCAuxiliaryTools/releases) for that.

### Installation itself

Download mac os you want using `macrecovery` tool located at [opencore](https://github.com/acidanthera/OpenCorePkg/releases) package. Meanwhile you can start working on your USB.
create folder named: `com.apple.recovery.boot`. You can also copy the `EFI` folder from `install` folder onto your USB.

Once you finish downloading the macOS, check results folder, you grab all files called something like: "base_system" and place the into the `com.apple.recovery.boot` folder you created earlier.

Great work! Now reboot your machine and boot into your USB (`F8` or `F11` are boot keys that some system uses). You should see black screen with white text. Select option with .dmg as file extension. (could be named after your USB).

Here comes the crucial part of all this.
Your computer will try booting MacOS.
If you find any trouble, you have to google for solution. It everything goes well you should see installation window.
format your drive with `APFS` and install mac os.

## Post Install

Great! You have installed MacOS into your super RGB gaming machine, Steave jobs would be proud of you!

Now if you plug out your USB are reboot, nothing will happen(no boot), that is because MacOS is installed, but without bootloader.

To install opencore bootloader you will need [this](https://github.com/corpnewt/MountEFI) utility. Run it and select your system drive. Then just simply copy my `EFI` folder from postInstall into the EFI drive that you just mounted.

**important** udate your postInstall `config.plist` with changes that you've done to your installation `config.plist`

If all of this is done, then you can reboot your machine and boot to your freshly install mac os.

## Known issues

1. 3.5 line-in microphone does not work (Could be fixed, by using VoodooHDA, but you will have to live with worse quality)
2. unknown CPU in `finder > about this mac`
3. All electron/Chromium based application are laggy on resize,manipulation (MS Edge, VS code, Messenger...)
4. VM LVL2 application does not work (Docker, Parallels...[virtualbox does])
5. USB Bluetooth
