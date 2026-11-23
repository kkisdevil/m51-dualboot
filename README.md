# m51-dualboot

Dual-boot for the Samsung Galaxy M51 (SM-M515F, Snapdragon 730G / SM7150) — research-stage.

## Status: research, depends on native Linux first

Dual-boot only comes **after** single-boot Linux works on m51. That work lives in the sister repo [m51-linux-boot](https://github.com/kkisdevil/m51-linux-boot). This repo is the boot-manager side: choosing between Android (UN1CA / stock) and Linux at boot.

## Why there is no universal Samsung dual-boot

Samsung phones have no UEFI, no GRUB, no EFI System Partition. The boot chain is BootROM → XBL/SBL → Samsung's proprietary ABL → TrustZone → boot.img, each stage signature-verified. A boot manager can only ever be a second-stage bootloader smuggled into the `boot` partition, ported per SoC and per device.

Every historic dual-boot project is dead: EFIDroid (last pushed 2018, Samsung ports only Galaxy S5 and Note 4), DualBootPatcher (2018), MultiROM / kexec-hardboot (dead ~2017, broken by Android 8 early-mount).

## The live pattern

lk2nd / U-Boot as a second-stage bootloader — actively maintained, gives fastboot + boot menu + mainline-kernel boot — but it covers old SoCs only, no SM7150, no m51 yet. That is the port this repo tracks.

There is no PC-style UEFI here: the "UEFI" layer *is* U-Boot's EFI, chainloaded as a second stage. Dual-boot is partition-based (Linux EFI partition on `cache`, rootfs on `userdata`), and only after single-boot Linux works.

## Scope

m51-first, research-stage. Not a universal Samsung dual-boot manager — that name would promise something that doesn't exist.

## Licence and credits

GPL-3.0. See [CREDITS.md](CREDITS.md).
