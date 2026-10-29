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
│   ├── Debian-family/     (AnduinOS, antiX, Debian, elementary OS, Kali, KDE neon, LMDE, Mint, MX Linux,
│   │                        Pop!_OS, Q4OS, Ubuntu variants, Zorin OS 18.1 + legacy 32-bit 15.3)
│   ├── Fedora-family/     (AlmaLinux, Bazzite, CentOS Stream, Fedora KDE/Workstation/Server, Nobara, Rocky)
│   └── Other/             (Deepin)
├── Rescue/                (Clonezilla, GParted, Memtest86+, Rescatux, SystemRescue; on the drive in _ISO/RESCUE and _ISO/UTILITIES_MEMTEST)
└── Windows/               (Windows 10, Windows 11)
```

Each leaf file (e.g. `Windows10.iso.md`) documents the project name, the official download URL,
and any notes on the specific build/edition present on the drive.

## Layout rule on the drive

Every image sits in its own short, named folder. No loose ISOs at family level. The boot files in the drive root (`grldr`, `menu.lst`, `*PESE.ini`, `unattend.xml` etc.), plus `_ISO/e2b/` and `_ISO/MAINMENU/`, are core to Easy2Boot and must stay. Everything else Easy2Boot ships by default that wasn't actually in use — `_ISO/_Tools/` (Windows-only desktop utilities), `_ISO/docs/` (reference material), the Windows post-install automation kit (`_ISO/WINDOWS/installs/`), and empty placeholder folders (`WINPE`, `WIN`, `BACKUP`, `AUTO`, `ANTIVIRUS`, `DOS`) — was removed to keep the top level readable.

## Status on the drive (2026-10-29)

**35 images, about 125 GB used** (Windows 10 x86, and Q4OS still finishing a copy to the drive as of this update).

- **Checksum verified against official sources:** every Linux image listed under `Linux/`, plus Ubuntu Server 26.04.1, Rocky 9.8 minimal, SystemRescue 13.02 and Clonezilla 3.3.3-37.
- **Size-only (no official checksum available):** Zorin OS 18.1, Zorin OS 15.3 Lite (32-bit), antiX 26.1 (32-bit), Q4OS 5.10 (32-bit), GParted 1.8.1, Memtest86+ 9.00, Rescatux 0.74.
- **Not booted yet.** Nothing has been boot-tested.

**Two genuinely 32-bit-only machine support:** antiX 26.1 and Zorin OS 15.3 Lite (and Q4OS 5.10) were added specifically for an old 32-bit-only Acer laptop that can't run any current mainstream distro. Zorin OS 15.3 is a legacy build kept for this reason; on 64-bit hardware use Zorin-OS-18.1-Core-64-bit.iso instead.

**Listed here but not on the drive:** AnduinOS (upstream only publishes torrents, no direct HTTP link).

**Now on the drive (previously listed as missing):** elementary OS 8.1, Ubuntu MATE 24.04.3, Windows 10 (x64 and x32), Windows 11.

The mobile systems (GrapheneOS, LineageOS, /e/OS, postmarketOS, Ubuntu Touch, Plasma Mobile) are flashed onto phones, not booted from a PC, so they do not belong on this drive.
