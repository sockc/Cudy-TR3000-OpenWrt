# Cudy TR3000 V1 (128MB) — OpenWrt U-Boot Mod

GitHub Actions custom firmware for **Cudy TR3000 V1 128MB NAND with OpenWrt U-Boot layout only**.

- Target: `mediatek/filogic`
- Device: `cudy_tr3000-v1-ubootmod` (fixed; not user-selectable)
- OpenWrt source: `v24.10.6` (pinned)
- Upgrade image: `*cudy_tr3000-v1-ubootmod*squashfs-sysupgrade.itb`

## Build with selected software

1. Go to **Actions → Build TR3000 U-Boot Mod → Run workflow**.
2. Tick **LuCI Web admin (HTTPS)**, **SmartDNS + LuCI app**, and/or **Tailscale**. All three default to enabled.
3. Optionally turn off **Publish firmware in Releases**.
4. Run workflow. Download the artifact; if publishing is enabled, download from **Releases**.
5. Compare image checksum with `SHA256SUMS` before flashing.

### Option mapping (official OpenWrt 24.10 feeds)

| Checkbox | Packages |
| --- | --- |
| LuCI | `luci`, `luci-ssl`, `luci-app-firewall` |
| SmartDNS | `smartdns`, `luci-app-smartdns` |
| Tailscale | `tailscale` |

SmartDNS LuCI app pulls LuCI dependencies even when the separate LuCI option is disabled. Installing Tailscale does **not** automatically log in to a tailnet: complete setup after installation. SmartDNS also requires post-install DNS configuration; no DNS takeover is hardcoded.

The common tools in `packages.txt` are included in every build. The workflow generates `requested-packages.txt` and `effective.config`, and fails if requested packages cannot be selected. A failed compilation does not publish a release.

Official branches are used for feeds via the pinned OpenWrt source's default feeds configuration. No third-party feeds are required for these three options.

## Safety

**Never flash this image onto stock partition layout, TR3000 256MB, or other router models.** Verify installed firmware and flash layout:

```sh
ubus call system board
cat /proc/mtd
```

Back up your config before upgrading. Only use the `sysupgrade.itb` for compatible OpenWrt U-Boot Mod sysupgrade. Bootloader artifacts are not regular firmware upgrades.

GitHub Actions build has not yet been run/validated.
