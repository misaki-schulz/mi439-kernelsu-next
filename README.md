# KernelSU-Next kernel for Xiaomi Redmi 8 / 8A / 7A (mi439)

Public builds of a Linux 4.19.325 kernel with **KernelSU-Next** (`legacy`) for the Xiaomi Redmi 8 family based on the sdm439 platform.

## Download

**[AnyKernel3-kernel-7.zip](https://github.com/misaki-schulz/mi439-kernelsu-next/releases/download/v3.4.0-legacy-run7/AnyKernel3-kernel-7.zip)** — flashable AnyKernel3 package.

See [Releases](https://github.com/misaki-schulz/mi439-kernelsu-next/releases) for all builds.

## Build details

| Item | Value |
| --- | --- |
| Kernel | Linux 4.19.325 |
| Device | Xiaomi Redmi 8 / 8A / 7A (mi439, sdm439) |
| Defconfig | `vendor/mi439-stock_defconfig` + `vendor/xiaomi-sdm439.config` |
| Targets | `Image.gz`, `dtbo.img` |
| KernelSU-Next | `v3.4.0-legacy` (version `33318`) |
| KSU hook | Syscall table patching (`CONFIG_KSU_SYSCALL_TABLE_HOOK=y`) |
| Source commit | `b9bcd1fac` |
| CI run | `42468626622` |

## Package contents

- `Image.gz` — kernel image
- `dtbo.img` — device tree overlays for `sdm439-olive` and `sdm439-pine`
- AnyKernel3 installer (`anykernel.sh`, `META-INF`, `tools`)

## Flashing

1. Boot into TWRP / recovery.
2. Flash `AnyKernel3-kernel-7.zip`.
3. Reboot.

The package repacks the existing `boot` image and flashes the `dtbo` partition. Device check is disabled (`do.devicecheck=0`); it targets mi439 (`olive` / `olivelite` / `pine`).

> Warning: flashing a custom kernel can brick your device or break the boot. Back up your boot/dtbo partitions first.
