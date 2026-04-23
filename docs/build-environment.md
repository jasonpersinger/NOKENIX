# NOKENIX Build Environment

## Purpose

This document defines the first supported way to build NOKENIX locally.

The goal is reproducibility with minimum complexity, not maximum cleverness.

## Canonical Build Host

- Host OS: Debian `stable`
- Current pinned release target: `trixie`
- Host form: virtual machine
- Host architecture: `amd64`

As of `2026-04-23`, Debian `stable` is `trixie`. The build config pins the codename instead of using the moving `stable` alias so the project does not silently change base releases later.

## Why a VM First

NOKENIX is using `live-build`, which performs privileged chroot, mount, and image-generation work. A clean Debian VM is the simplest environment to explain, reproduce, and debug for a small volunteer team.

Containerized builds can be revisited later, but they are not the first supported path.

## Minimum Requirements

- Root or `sudo` access
- A filesystem mounted with `dev` and `exec` permissions
- Enough free disk for package downloads and an ISO build
- Hardware virtualization support if you want fast VM smoke tests

## Base Packages

Install the initial toolchain on the Debian build VM:

```bash
sudo apt update
sudo apt install live-build git qemu-system-x86 ovmf
```

This is intentionally small. Add more packages only when the build or test workflow proves they are needed.

## Non-Canonical Host Fallback

If you are not on Debian but do have Docker available, `./scripts/build-iso` will fall back to a privileged Debian `trixie` container and run the same `live-build` workflow there.

That fallback is for convenience. The canonical documented environment is still a clean Debian `stable` VM.

## Repository Workflow

Clone the repo and enter it:

```bash
git clone <your-repo-url> NOKENIX
cd NOKENIX
```

## Build Workflow

Run the ISO build wrapper from the project root:

```bash
./scripts/build-iso
```

What this does:

1. Enters the `build/` directory
2. Cleans prior live-build output
3. Regenerates the live-build configuration through `build/auto/config`
4. Runs `lb build`
5. Stores a build log at `build/build.log`

The current package manifest is intentionally minimal and uses an explicit Plasma desktop package set so the first ISO target stays controlled.

## Smoke Test Workflow

Boot the newest ISO in QEMU:

```bash
./scripts/test-iso
```

The test wrapper prefers `UEFI` with `OVMF` when available because that is the current primary boot target.

Run the automated boot smoke test:

```bash
./scripts/test-boot-smoke
```

This test does two things:

1. Confirms the ISO reaches the `UEFI` DVD handoff path.
2. Boots the live environment headlessly through a direct-kernel path, captures serial output, and passes when it sees either the explicit `NOKENIX_BOOT_SMOKE_OK` marker or later-stage evidence such as `sddm` startup or the serial login prompt.

If host `qemu-system-x86_64` is unavailable but Docker is present, the smoke test falls back to a Debian `trixie` container with QEMU and `OVMF`.

## Current Scope

This first scaffold is intentionally narrow:

- One architecture: `amd64`
- One desktop target: `KDE Plasma`
- One base release target: Debian `trixie`
- One official local build path: Debian `stable` VM

## Not Yet Included

- CI builds
- `BIOS` boot as a committed target
- Installer integration
- Custom package repository setup
- Branding assets beyond placeholders

Those are later phases, not blockers for establishing the build base.
