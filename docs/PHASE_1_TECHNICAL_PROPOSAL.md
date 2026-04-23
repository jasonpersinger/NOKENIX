# NOKENIX Phase 1 Technical Proposal

## Purpose

This document proposes the first practical build path for NOKENIX. The goal is not to solve every later design question now. The goal is to choose a build stack and repository structure that are simple, reproducible, Debian-aligned, and realistic for a small volunteer team.

## Recommendation Summary

For version 1, NOKENIX should use:

- `live-build` to generate the live ISO
- `Calamares` as the graphical installer
- A clean Debian `stable` VM as the canonical build environment
- `GitHub` as the source of truth for config, docs, and issue tracking
- Local builds as the first supported workflow
- CI only after the local build path is stable
- An explicit Debian codename pin instead of the moving `stable` alias

## Why This Stack

### `live-build`

`live-build` is the Debian Live project's build tool and is designed around a configuration directory. That matches the project's need for a Debian-first, reproducible ISO process.

It also gives NOKENIX a straightforward way to manage:

- Package lists
- Chroot includes
- Hooks
- Bootloader behavior
- ISO creation
- Optional installer-stage integration

This is a better fit than GUI remastering tools because the build definition lives in version-controlled files rather than in one maintainer's machine state.

### `Calamares`

NOKENIX wants a simple, polished installer experience. Calamares is a distribution-agnostic installer framework with strong branding support and a modular flow that fits that goal well.

It is also already packaged in Debian, including Debian-specific Calamares settings packages, which lowers the integration cost.

### Debian `stable` VM as Canonical Build Host

A containerized build environment is appealing in theory, but it is not the simplest first step here. `live-build` performs privileged work with chroots, mounts, and image generation, and those workflows often become more awkward inside partially isolated containers.

For this project's first supported workflow, the simplest reproducible approach is:

1. Start from a clean Debian `stable` VM
2. Install the documented build dependencies
3. Clone the repo
4. Run the documented build commands

That keeps the environment standardized without forcing the team to solve container edge cases before the distro even boots.

## Alternatives Considered

### `Cubic`

Rejected as the primary workflow.

Reason: Cubic is useful for interactive remastering, but it is not the best foundation for a small team that needs rebuildable, reviewable, version-controlled distro configuration. It is better as a one-off experimentation tool than as the official build system.

### Debian Installer as the Primary User Installer

Not recommended for the first NOKENIX user experience.

Reason: It is powerful and battle-tested, but NOKENIX is aiming for a more newcomer-friendly and visually branded live-to-install flow.

### Mandatory Containerized Builds on Day One

Rejected for the first supported workflow.

Reason: It adds complexity too early. Once the local VM-based process is stable, containerization can be revisited as an optimization.

## Proposed Repository Layout

This layout keeps the project understandable without overengineering it.

```text
NOKENIX/
├── README.md
├── PROJECT_CONTEXT.md
├── ROADMAP.md
├── DECISIONS.md
├── docs/
│   ├── PHASE_1_TECHNICAL_PROPOSAL.md
│   ├── build-environment.md
│   ├── package-policy.md
│   └── release-checklist.md
├── build/
│   ├── auto/
│   ├── config/
│   │   ├── package-lists/
│   │   ├── includes.chroot/
│   │   ├── includes.binary/
│   │   └── hooks/
├── assets/
│   ├── branding/
│   └── wallpapers/
└── scripts/
    ├── build-iso
    └── test-iso
```

## Layout Notes

- `build/` holds the actual distro build inputs.
- `build/auto/` stores the canonical `lb config` and cleanup entrypoints.
- `build/config/` is the live-build configuration tree.
- `build/config/package-lists/` should remain plain and readable.
- `build/config/includes.chroot/` is for files that belong inside the live filesystem.
- `build/config/includes.binary/` is for files copied into the ISO outside the chroot.
- `build/config/hooks/` is for the few steps that cannot be expressed cleanly as package lists or static file includes.
- `assets/` keeps branding materials separate from technical config.
- `scripts/` should stay thin wrappers around documented commands, not become a second build system.

## Proposed Build Workflow

### Supported Workflow for Early Development

1. Provision a clean Debian `stable` VM
2. Install build dependencies
3. Clone the NOKENIX repository
4. Run the documented `live-build` configuration and build steps
5. Boot the produced ISO in a VM for smoke testing

### Early Verification Standard

Phase 1 is successful when:

- A second contributor can follow the docs and prepare the same build environment
- The ISO build completes from version-controlled config
- The ISO boots in a VM
- Build steps do not depend on undocumented machine-local tweaks

## Build Environment Proposal

### Canonical Host

- OS: Debian `stable`
- Form: virtual machine
- Architecture: `amd64`
- Current pinned target release: `trixie`

### Why This Is the Right Starting Point

- It aligns with the target distro family
- It reduces support variance across contributors
- It avoids container privilege and mount surprises
- It is simple to document for club members

## Installer Strategy

NOKENIX should separate live ISO creation from installer customization.

That means:

- First, get a bootable live ISO with the right desktop and package baseline
- Then integrate Calamares into that environment
- Then brand and tune the installer flow

This keeps the team from debugging ISO generation, installer integration, and branding all at once.

## Recommended Phase Order

1. Produce a minimal live ISO with `live-build`
2. Confirm boot in a VM
3. Add NOKENIX package lists and desktop defaults
4. Integrate `Calamares`
5. Tune installer behavior and branding
6. Add CI checks after the local workflow is dependable

## Risks to Watch Early

### Free Software Only

This may conflict with the newcomer-friendly goal on real hardware. The project should not forget this just because VM testing looks good.

### Offline ISO Growth

An offline-capable system can become bloated quickly. Package curation discipline will matter from the start.

### Hook Sprawl

If too much logic ends up in ad hoc shell hooks, the build becomes harder to reason about. Prefer package lists and static includes first.

## Immediate Follow-Up Work

With the initial scaffold in place, the next session should focus on:

- Deciding whether to keep `UEFI`-only for the first bootable target or add `BIOS`
- Expanding the package manifest beyond the base `live-task-kde` starting point
- Integrating `Calamares` after the live ISO boots reliably
- Defining a first VM smoke-test checklist

## Source Basis

This recommendation is based on current official Debian Live and Calamares documentation, plus current Debian package availability as checked on `2026-04-23`.
