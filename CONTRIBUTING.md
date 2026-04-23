# Contributing To NOKENIX

NOKENIX is a small community distro project. The contribution model should stay simple, explicit, and easy for new volunteers to follow.

## Good First Ways To Help

- Improve documentation
- Test ISO builds and report what worked or failed
- Review package choices and desktop defaults
- Help refine branding assets and visual consistency
- Validate the live session in VMs or on spare hardware
- Triage issues and turn vague ideas into concrete decisions

## Ground Rules

- Keep changes tied to the current project scope
- Prefer Debian-first solutions over custom infrastructure
- Avoid speculative abstractions and large unrelated cleanups
- Document assumptions when a decision is not obvious
- If a change creates a new policy or workflow, write it down

The repo also includes [AGENTS.md](/home/jason/NOKENIX/AGENTS.md), which holds working guidance for coding agents used in the project.

## Before You Start

Read these first:

- [README.md](/home/jason/NOKENIX/README.md)
- [PROJECT_CONTEXT.md](/home/jason/NOKENIX/PROJECT_CONTEXT.md)
- [DECISIONS.md](/home/jason/NOKENIX/DECISIONS.md)
- [ROADMAP.md](/home/jason/NOKENIX/ROADMAP.md)
- [docs/build-environment.md](/home/jason/NOKENIX/docs/build-environment.md)

If you want to work on packaging or release behavior, also read:

- [docs/package-policy.md](/home/jason/NOKENIX/docs/package-policy.md)
- [docs/release-checklist.md](/home/jason/NOKENIX/docs/release-checklist.md)

## Current Technical Baseline

- Debian base: `trixie`
- Desktop target: `KDE Plasma`
- Architecture target: `amd64`
- Build stack: `live-build`
- Installer direction: `Calamares`
- Canonical build host: Debian `stable` VM

This baseline is current as of `2026-04-23`. If you want to change it, update the relevant decision record instead of treating it as an informal assumption.

## Local Build Workflow

From the repo root:

```bash
./scripts/build-iso
```

Useful verification commands:

```bash
./scripts/test-iso
./scripts/test-boot-smoke
```

The smoke test currently verifies:

- `UEFI` ISO handoff in QEMU
- headless live boot through a direct-kernel path
- later-stage boot success through serial output markers such as `sddm` startup

## Contribution Workflow

1. Open an issue if the work changes project direction, policy, or scope.
2. Make a focused branch or focused commit series.
3. Keep the change set narrow and explain the reasoning clearly.
4. Run the most relevant local verification you can.
5. Summarize what changed, how you verified it, and what remains unverified.

If you cannot run a full ISO build or VM test, say that explicitly.

## Pull Request Expectations

A good PR for NOKENIX should answer:

- What problem does this change solve?
- Why is this the right level of complexity?
- What did you verify locally?
- What still needs follow-up testing?

For larger changes, include any relevant impact on:

- build reproducibility
- Debian compatibility
- package policy
- branding consistency
- newcomer usability

## What Not To Do

- Do not add custom low-level distro infrastructure without a documented reason
- Do not silently expand scope beyond the current roadmap
- Do not mix branding work, package-policy changes, and build-system refactors into one PR unless they are tightly coupled
- Do not introduce non-free components by default without an explicit project decision

## Areas Needing Help

The highest-value near-term contribution areas are:

- installer integration
- default package selection
- branding implementation in boot and desktop assets
- VM and hardware testing
- release workflow refinement

## Communication

Use GitHub issues and pull requests as the primary project record.

When in doubt:

- make the assumption explicit
- choose the simpler path
- write down the tradeoff

