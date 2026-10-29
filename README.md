# the-handy-os-drive

A link manifest for my personal **Easy2Boot** multiboot USB drive (SanDisk Cruzer Glide, 233 GB).

This repo mirrors the folder structure of the ISO directory on the drive, but instead of the
actual ISO/image files it contains a small `.md` file per entry with a link to the **official**
download source for that image. It does not contain any of the actual binaries: GitHub can't
host tens of GB of ISOs, and shipping links to official sources is more auditable and safer
than shipping the binaries themselves.

## Why this exists

If the drive is ever lost, damaged, or its integrity is in doubt (suspected tampering,
unexpected modification, etc.), this manifest lets the drive be rebuilt from trusted upstream
sources rather than from copies of unknown provenance.

**Always verify before booting anything:** download only from the linked official page, then
check the file's SHA256 checksum (and PGP signature, where the project publishes one) against
the value posted on that same official page before writing it to media or booting it. Do not
trust an ISO, including a copy already sitting on a drive, just because it's named correctly.

## The drive today

- Tool: **Easy2Boot (E2B)**. Data partition: NTFS, label `EASY2BOOT`, about 230 GB. A small second partition holds the boot files.
- Adding an image is a plain file copy into `_ISO/` on the drive; the Linux ones live in `_ISO/LINUX/<family>/<name>/`. This repo's `ISOs/Linux/` mirrors that.
- Mount on Linux without sudo: `udisksctl mount -b /dev/sdX1`. Check `lsblk` for model `Cruzer Glide` first; the device letter changes.

### History: it used to be Ventoy

Until late October 2026 this was a Ventoy drive (exFAT data partition plus a small `VTOYEFI` partition), and
this README described it that way. On 2026-10-28 the drive stopped being readable on one of my machines,
and the drive turned out to carry Easy2Boot instead. The decision was to **keep Easy2Boot** and not go
back to Ventoy. Ventoy-specific advice (`Ventoy2Disk.sh`, `VTOYEFI`, enrolling the Ventoy key under
Secure Boot) no longer applies.

## Structure

```
ISOs/
├── Linux/
│   ├── Arch-family/       (Arch, BigLinux, CachyOS, Garuda, Manjaro)
│   ├── Debian-family/     (AnduinOS, Debian, elementary OS, Kali, Mint, Pop!_OS, Ubuntu variants, Zorin)
│   ├── Fedora-family/     (AlmaLinux, CentOS Stream, Fedora KDE/Workstation, KDE neon, Rocky)
│   └── Other/             (Deepin)
├── Rescue/                (Clonezilla, GParted, Memtest86+, Rescatux, SystemRescue; on the drive in _ISO/RESCUE and _ISO/UTILITIES_MEMTEST)
└── Windows/               (Windows 10, Windows 11)
```

Each leaf file (e.g. `Windows10.iso.md`) documents the project name, the official download URL,
and any notes on the specific build/edition present on the drive.

## Layout rule on the drive

Every image sits in its own short, named folder. No loose ISOs at family level. Easy2Boot's own helper scripts live in `_ISO/_Tools/`; the boot files in the drive root (`grldr`, `menu.lst`, `*PESE.ini`, `unattend.xml` etc.) must stay there.

## Status on the drive (2026-10-29)

**31 images, about 98 GB used.**

- **Checksum verified against official sources:** every Linux image listed under `Linux/`, plus Ubuntu Server 26.04.1, Rocky 9.8 minimal, SystemRescue 13.02 and Clonezilla 3.3.3-37.
- **Size-only (no official checksum available):** Zorin OS 18.1, GParted 1.8.1, Memtest86+ 9.00, Rescatux 0.74.
- **Not booted yet.** Nothing has been boot-tested.

**Listed here but not on the drive:** AnduinOS, elementary OS, Ubuntu MATE (no 26.04 release published), Windows 10 and Windows 11 (Microsoft only hands out one-time download links, so these are added by hand).

The mobile systems (GrapheneOS, LineageOS, /e/OS, postmarketOS, Ubuntu Touch, Plasma Mobile) are flashed onto phones, not booted from a PC, so they do not belong on this drive.
