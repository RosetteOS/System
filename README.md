# NebulaOS Kernel SDK

This repository contains the Linux 6.6 and Buildroot SDK used by
[NebulaOS](https://github.com/coreflake1/NebulaOS) on the Creality Ender-3 V3 KE
(Ingenic X2000).

The [RosetteOS firmware repository](https://github.com/RosetteOS/RosetteOS) uses this repository as a
build input. It fetches the exact commit pinned in `RosetteOS/manifests/dependencies.conf`; the pin,
not a moving branch, defines the kernel and Buildroot revision used for a firmware build.

## You probably don't want to build this repo directly

For a complete RosetteOS image, follow the build and installation instructions in the
[RosetteOS firmware repository](https://github.com/RosetteOS/RosetteOS). Its build fetches the pinned
System commit and applies the qualified kernel variants before compiling.

## The 8 build-time variants

These live in RosetteOS, not here — this repository holds the base kernel source they patch at build
time. They are applied by
[`scripts/build/apply-qualified-baseline.sh`](https://github.com/RosetteOS/RosetteOS/blob/main/scripts/build/apply-qualified-baseline.sh):

1. PREEMPT_RT
2. WiFi SDIO IRQ priority
3. VSYNC-gated display panning
4. A pinctrl ownership fix
5. The final backlight controller
6. PWM state readback
7. The final touch driver
8. Disabling WiFi roaming

## If you're setting up a device

The install, update, and recovery docs live in RosetteOS:

- [Build From Source](https://github.com/RosetteOS/RosetteOS/blob/main/docs/BUILD_FROM_SOURCE.md)
- [A/B Slot Model](https://github.com/RosetteOS/RosetteOS/blob/main/docs/A_B_SLOT_MODEL.md)

## License

This is a whole SDK — kernel, Buildroot, u-boot, and a handful of vendored tools — each under its
own upstream license, so there's no single root `LICENSE` file that covers everything. The kernel
itself is at `kernel/kernel-6.6/COPYING` (GPL-2.0) and `kernel/kernel-6.6/LICENSES/`; other
top-level directories have their own license files. GitHub's license detector only looks at the
repo root, so it'll correctly show "no license detected" here — check the specific subdirectory
you're actually using.
