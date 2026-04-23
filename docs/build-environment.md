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

The current package manifest is intentionally minimal and starts from Debian's `live-task-kde` metapackage rather than a large custom application suite.

## Smoke Test Workflow

Boot the newest ISO in QEMU:

```bash
./scripts/test-iso
```

The test wrapper prefers `UEFI` with `OVMF` when available because that is the current primary boot target.

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
