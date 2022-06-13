# Ryzentosh - Catalina/Big Sur


finder: ![finder:About my mac](about.png)

**By downloading/cloning this repo, you agree that you take all risks to yourself and cant blame me for it**

**Before installing, generate new PlatformInfo in both postInstall/install configs (`gensmbios`)**

## Install 

Its quite simple, create USB drive for boot.(8GB USB should do the trick) Check out opencore guide for creating USB. Then simply copy `EFI` folder from `install` folder of this repo. You also need to change few bios settings and those settings are: 

**disable:**

* fast boot
* com/serial port
* secure boot
* parallel port
* if 4G decoding is enabled, then disable resize bar

**enable:**

* 4G decoding
* switch sata operation to AHCI

## After install 

Once youve installed MacOS on you system, you need to mount efi partition of your system drive, use `MountEFI` utility, then copy `EFI` from `postInstall` folder and voila! You now have working MacOS on regular old PC.


## Specs 
- AMD Ryzen 5 5600x (6c, 12th)
- AMD Radeon RX580 8GB (XFX)
- Asus B450MK-I 
- 16GB DDR4 2666MHz
- Realtek ALC887
- latest bios

## Known issues
- 3.5 line-in mic. doesnt work (could be fixed, but the quality of audio will be worse)
- VM machines (virtulbox runs fine, but docker, Paralels does not)
