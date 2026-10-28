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
this README described it that way. On 2026-10-28 the laptop could not read the main partition any more,
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
├── Rescue/                (Clonezilla, GParted, Memtest86+, Rescatux, SystemRescue)
└── Windows/               (Windows 10, Windows 11)
```

Each leaf file (e.g. `Windows10.iso.md`) documents the project name, the official download URL,
and any notes on the specific build/edition present on the drive.

## Status on the drive (2026-10-28)

**On the drive, checksum verified on 2026-10-28:** CachyOS 260809 (re-downloaded, the first copy was cut off), Garuda Mokka (latest), Pop!_OS 24.04 Intel build 20, KDE neon (user, 2026-10-25), Deepin 25.2.0.

**On the drive, not re-verified yet:** Manjaro GNOME 26.1.0, BigLinux 2026-08-08, Debian 13.7.0 netinst, Ubuntu 26.04.1 desktop, AlmaLinux 9.8 minimal, CentOS Stream 9 boot.

**Listed here but not on the drive yet** (the entries are the shopping list): Arch, AnduinOS, elementary OS, Kali, Linux Mint 22.3, Ubuntu MATE, Ubuntu Server, Fedora 44 KDE, Fedora 44 Workstation, Rocky 9.8, Clonezilla, GParted, Memtest86+, Rescatux, SystemRescue, Windows 10, Windows 11. Zorin OS 18.1 Core is downloaded on the laptop but not copied to the drive yet.

The mobile systems (GrapheneOS, LineageOS, /e/OS, postmarketOS, Ubuntu Touch, Plasma Mobile) are flashed onto phones, not booted from a PC, so they do not belong on this drive.
