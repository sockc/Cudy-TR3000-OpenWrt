# Cudy TR3000 V1 (128MB) — OpenWrt U-Boot Mod

GitHub Actions firmware builds **only** for Cudy TR3000 V1, 128MB NAND, **OpenWrt U-Boot layout**.

- Target / subtarget: `mediatek/filogic`
- Device profile: `cudy_tr3000-v1-ubootmod`
- Pinned source tag: `v24.10.6`
- Expected sysupgrade image: `*cudy_tr3000-v1-ubootmod-squashfs-sysupgrade.itb`

## Build

1. Open **Actions → Build TR3000 U-Boot Mod → Run workflow**.
2. By default the workflow uploads an artifact and creates a GitHub Release.
3. Download the `sysupgrade.itb` and check its SHA256 against `SHA256SUMS`.
4. Inspect `effective.config` and `BUILDINFO.txt` in the release.

## Packages

Edit `packages.txt`, one official feed package per line. Build fails if a requested package is unavailable.
Third-party applications require separately maintained feeds and testing; they are not bundled by default.

## Flashing warning

**Do not flash to stock Cudy layout, the 256MB variant, or an unverified device.**
This only builds a sysupgrade image and does not convert bootloaders or partition layouts.
Before upgrading, back up your configuration and verify:
```sh
ubus call system board
cat /proc/mtd
```
Use compatible TR3000 OpenWrt U-Boot layout and follow device-specific instructions.
Never flash `preloader.bin` or `bl31-uboot.fip` through the normal sysupgrade interface.

Build validation on GitHub Actions is pending.
