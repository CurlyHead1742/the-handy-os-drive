# the-handy-os-drive

A link manifest for my personal Ventoy multiboot USB drive.

This repo mirrors the folder structure of the `ISOs/` directory on the drive, but instead of the
actual ISO/image files it contains a small `.md` file per entry with a link to the **official**
download source for that image. It does not contain any of the actual binaries — GitHub can't
host ~78GB of ISOs, and shipping links to official sources is more auditable and safer than
shipping the binaries themselves.

## Why this exists

If the drive is ever lost, damaged, or its integrity is in doubt (suspected tampering,
unexpected modification, etc.), this manifest lets the drive be rebuilt from trusted upstream
sources rather than from copies of unknown provenance.

**Always verify before booting anything:** download only from the linked official page, then
check the file's SHA256 checksum (and PGP signature, where the project publishes one) against
the value posted on that same official page before writing it to media or booting it. Do not
trust an ISO — including a copy already sitting on a drive — just because it's named correctly.

## Structure

```
ISOs/
├── Linux/
│   ├── Arch-family/       (Arch, BigLinux, Garuda, Manjaro)
│   ├── Debian-family/     (AnduinOS, Debian, elementary OS, Kali, Mint, Pop!_OS, Ubuntu variants)
│   └── Fedora-family/     (AlmaLinux, CentOS Stream, Fedora KDE/Workstation, Rocky)
├── Rescue/                (Clonezilla, GParted, Memtest86+, Rescatux, SystemRescue)
└── Windows/               (Windows 10, Windows 11)
```

Each leaf file (e.g. `Windows10.iso.md`) documents the project name, the official download URL,
and any notes on the specific build/edition present on the drive.
