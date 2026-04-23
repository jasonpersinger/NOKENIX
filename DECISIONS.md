# NOKENIX Decisions

This file records decisions that are either accepted or currently proposed for review. It is meant to be short, explicit, and easy to update.

## Status Key

- `Accepted`: decided and active
- `Proposed`: recommended, but not fully locked
- `Open`: still unresolved

## Accepted Decisions

### NXD-001: Base Distribution

- Status: `Accepted`
- Date: `2026-04-23`
- Decision: NOKENIX will be based on Debian `stable`.
- Rationale: This keeps the distro on a conservative, well-supported base with lower maintenance burden for a volunteer team.

### NXD-002: Primary Desktop

- Status: `Accepted`
- Date: `2026-04-23`
- Decision: The first release will ship with `KDE Plasma` as the flagship desktop environment.
- Rationale: KDE Plasma is a full-featured desktop with strong newcomer usability and room for intermediate users.

### NXD-003: Architecture Scope

- Status: `Accepted`
- Date: `2026-04-23`
- Decision: Version 1 targets `amd64` only.
- Rationale: Restricting architecture scope reduces complexity and speeds up the first usable release.

### NXD-004: Distribution Character

- Status: `Accepted`
- Date: `2026-04-23`
- Decision: NOKENIX should be beginner-to-intermediate friendly, daily-driver capable, and maintainable by a small club without custom kernel work or exotic build systems.
- Rationale: This is the core project constraint and should filter out choices that create unnecessary maintenance debt.

### NXD-005: Software Freedom Policy

- Status: `Accepted`
- Date: `2026-04-23`
- Decision: The initial release direction is free software only.
- Rationale: This gives the project a clear policy boundary, even though it creates hardware compatibility tradeoffs that must be documented and tested.

### NXD-006: Offline Goal

- Status: `Accepted`
- Date: `2026-04-23`
- Decision: The first release should aim to be usable mostly offline after download.
- Rationale: This improves the install and first-use experience, especially for users with unreliable connectivity.

### NXD-007: Branding Direction

- Status: `Accepted`
- Date: `2026-04-23`
- Decision: NOKENIX should feel distinctly branded, with most of that distinction coming from visual identity, defaults, curation, and out-of-box experience rather than deep low-level divergence from Debian.
- Rationale: This creates a visible identity without forcing the project into a large custom engineering surface.

### NXD-008: Collaboration Platform

- Status: `Accepted`
- Date: `2026-04-23`
- Decision: Project collaboration will start on `GitHub`.
- Rationale: It is familiar, easy for volunteers to join, and sufficient for source control, issues, releases, and basic project documentation.

### NXD-009: ISO Build Stack

- Status: `Accepted`
- Date: `2026-04-23`
- Decision: Use `live-build` as the primary ISO build system.
- Rationale: It is Debian's live image build tool, is driven by a configuration directory, and fits the project's reproducibility and Debian-first goals.

### NXD-010: Installer Stack

- Status: `Accepted`
- Date: `2026-04-23`
- Decision: Use `Calamares` as the graphical installer direction for the first release.
- Rationale: It is a distribution-agnostic installer framework with branding support, automated and manual partitioning, and Debian packaging already exists for live-media use.

### NXD-011: Canonical Build Environment

- Status: `Accepted`
- Date: `2026-04-23`
- Decision: Standardize first on a clean Debian `stable` VM as the canonical build environment instead of making containerized builds mandatory on day one.
- Rationale: This is the simpler path for a small team. `live-build` performs privileged chroot and image-building work, and a VM is easier to document and debug consistently than a partially isolated container setup.

### NXD-012: Initial CI Scope

- Status: `Accepted`
- Date: `2026-04-23`
- Decision: Treat local reproducible builds as the source of truth first, then add CI validation after the local build path is stable.
- Rationale: This prevents the team from debugging GitHub Actions and the distro build at the same time.

### NXD-013: Release Pinning

- Status: `Accepted`
- Date: `2026-04-23`
- Decision: Pin the live-build configuration to a Debian codename, not the moving `stable` alias. The current pinned target is `trixie`.
- Rationale: Reproducibility is weaker if the base release changes implicitly. Pinning the codename keeps the build definition stable until the project intentionally rebases.

## Proposed Decisions

### NXD-014: Custom Packaging Scope

- Status: `Proposed`
- Date: `2026-04-23`
- Decision: Avoid a large custom package repository at the start. If project-owned packages are needed, keep them limited to branding, defaults, or thin configuration packages.
- Rationale: This keeps maintenance realistic while still allowing NOKENIX to own the parts that must be distinctly its own.

## Open Decisions

### NXD-015: Boot Support

- Status: `Open`
- Date: `2026-04-23`
- Question: Should version 1 officially support both `UEFI` and legacy `BIOS`, or should `UEFI` be the only guaranteed target?
- Current leaning: Require `UEFI`; include `BIOS` only if the configuration and testing burden stays low.

### NXD-016: Debian Backports Policy

- Status: `Open`
- Date: `2026-04-23`
- Question: Will NOKENIX use `backports`, and if so, for what categories of packages?
- Current leaning: Avoid broad use; allow only narrowly justified exceptions.

### NXD-017: Default Application Suite

- Status: `Open`
- Date: `2026-04-23`
- Question: What is the smallest daily-driver package set that still feels complete offline?

### NXD-018: Versioning and Release Cadence

- Status: `Open`
- Date: `2026-04-23`
- Question: Will releases track Debian stable point releases, use a date-based scheme, or use NOKENIX-specific version numbers?

## Immediate Recommendation

The next review should focus on `NXD-014` through `NXD-018`. The initial build stack is now scaffolded, so the next meaningful decisions are boot support, backports policy, app selection, and release model.
