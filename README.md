# NOKENIX

NOKENIX is a community Linux distribution project based in Roanoke, Virginia.

The project goal is straightforward: build a Debian-based desktop distro that feels polished and distinct, stays approachable for new Linux users, remains comfortable for intermediate users, and can realistically be maintained by a small volunteer club.

## Current Direction

- Base: Debian `stable`, currently pinned to `trixie`
- Desktop: `KDE Plasma`
- Architecture: `amd64`
- Software policy: free software only for the initial release direction
- Character: beginner-to-intermediate friendly, daily-driver oriented, Debian-first

NOKENIX is intentionally not trying to be a custom kernel distro, an experimental platform, or a large fork of Debian internals. The project’s identity is expected to come from branding, defaults, curation, and out-of-box experience rather than low-level divergence.

## Project Status

The repository is in early build and planning stage, but it is already past the “idea only” phase.

What exists today:

- Core project context and decisions
- A `live-build`-based ISO scaffold
- A documented canonical build environment
- A first bootable live ISO path
- Automated boot smoke testing in QEMU
- Early branding work and visual system drafts

What is not finished yet:

- Installer integration
- Final default application suite
- Final branding assets
- Release cadence and versioning
- CI pipeline

## Build The Current ISO

The canonical build environment is a clean Debian `stable` VM.

From the project root:

```bash
./scripts/build-iso
```

To run the current smoke tests:

```bash
./scripts/test-iso
./scripts/test-boot-smoke
```

If `live-build` is not available locally but Docker is installed, `./scripts/build-iso` can fall back to a privileged Debian `trixie` container. That fallback is for convenience; the documented primary path is still Debian `stable`.

## Repository Layout

- [PROJECT_CONTEXT.md](/home/jason/NOKENIX/PROJECT_CONTEXT.md): foundational project context
- [DECISIONS.md](/home/jason/NOKENIX/DECISIONS.md): accepted, proposed, and open decisions
- [ROADMAP.md](/home/jason/NOKENIX/ROADMAP.md): phased project plan
- [docs/build-environment.md](/home/jason/NOKENIX/docs/build-environment.md): build and test workflow
- [docs/package-policy.md](/home/jason/NOKENIX/docs/package-policy.md): current packaging guardrails
- [docs/release-checklist.md](/home/jason/NOKENIX/docs/release-checklist.md): release gate
- [build/README.md](/home/jason/NOKENIX/build/README.md): build directory notes
- [scripts](/home/jason/NOKENIX/scripts): helper scripts for build and test work

## Principles

The current project direction is guided by a few simple constraints:

- Stay close to Debian unless divergence is clearly worth the maintenance cost
- Prefer simple, reproducible tooling over clever infrastructure
- Aim for a polished desktop experience without building unnecessary custom internals
- Keep the project maintainable by a small volunteer team

## Contributing

Contributions are welcome, especially in these areas:

- build and installer work
- package curation
- testing in VMs and on real hardware
- documentation
- branding, wallpapers, boot assets, and desktop polish

Start with [CONTRIBUTING.md](/home/jason/NOKENIX/CONTRIBUTING.md).

