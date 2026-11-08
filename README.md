# KernelSU-Next kernel for Xiaomi Redmi 8 / 8A / 7A (mi439)

Public builds of a Linux 4.19.325 kernel with **KernelSU-Next** (`legacy`) for the Xiaomi Redmi 8 family based on the sdm439 platform.

## Download

**[AnyKernel3-kernel-9.zip](https://github.com/misaki-schulz/mi439-kernelsu-next/releases/download/v3.4.0-legacy-run9/AnyKernel3-kernel-9.zip)** — flashable AnyKernel3 package.

- sha256: `73b2f6ee19109407914e9028dc62db9289ab501eaa8685cd8aa4341aedd4ef96`
- size: 16,737,744 bytes

See [Releases](https://github.com/misaki-schulz/mi439-kernelsu-next/releases) for all builds.

## Build details

| Item | Value |
| --- | --- |
| Kernel | Linux 4.19.325 |
| Device | Xiaomi Redmi 8 / 8A / 7A (mi439, sdm439) |
| Defconfig | `vendor/mi439-stock_defconfig` + `vendor/xiaomi-sdm439.config` |
| Targets | `Image.gz-dtb`, `dtbo.img` |
| KernelSU-Next | `v3.4.0-legacy` (version `33318`) |
| KSU hook | Syscall table patching (`CONFIG_KSU_SYSCALL_TABLE_HOOK=y`) |
| Source commit | `9ef7d914d` |
| CI run | `42485120730` |

## Package contents

- `Image.gz-dtb` — kernel image **with the device DTBs appended** (`sdm439-pine`, `sdm439-olive`)
- `dtbo.img` — device tree overlays for `sdm439-olive` and `sdm439-pine`
- AnyKernel3 installer (`anykernel.sh`, `META-INF`, `tools`)

## Camera SMMU fix (run 9)

The camera SMMU context banks are brought up by the `qcom,msm-cam-smmu-cb`
child devices, whose probes can still be pending when the JPEG driver
registers. The driver then hit `strcmp(NULL, "jpeg_enc0")` and panicked the
kernel at boot. It now skips banks that have no name yet and returns
`-EPROBE_DEFER`, so the JPEG driver retries once the banks are up.

> `Image.gz-dtb` (not a bare `Image.gz`) is required: the boot image for mi439
> appends the DTBs to the kernel, and AnyKernel3 only drops the previous boot
> image's DTB when the provided kernel is named `*-dtb`. Shipping a bare
> `Image.gz` reuses the DTB of the previously installed kernel and causes a
> camera/SMMU NULL dereference panic at boot.

## Flashing

1. Boot into TWRP / recovery.
2. Flash `AnyKernel3-kernel-9.zip`.
3. Reboot.

The package repacks the existing `boot` image and flashes the `dtbo` partition. Device check is disabled (`do.devicecheck=0`); it targets mi439 (`olive` / `olivelite` / `pine` / `olivewood`).

> Warning: flashing a custom kernel can brick your device or break the boot. Back up your boot/dtbo partitions first.
