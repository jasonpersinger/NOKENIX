# NOKENIX Project Context

## Purpose

NOKENIX is a community Linux distribution project based in Roanoke, Virginia and driven by the local Linux club. The goal is to build a Debian-based desktop distribution that is approachable for new users, still comfortable for intermediate users, and realistic for a small volunteer team to maintain.

This document is the foundational context for the project. It records what has already been decided, what assumptions are currently in force, what remains open, and the principles that should guide future decisions.

## Core Intent

NOKENIX should be:

- Easy for a new Linux user to install and use as a daily driver
- Pleasant and polished enough to feel distinct, not like a generic Debian repackage
- Simple enough for a small community team to understand and maintain
- Reproducible enough that contributors can build the same ISO from the same source
- Rooted in regional identity without becoming gimmicky

NOKENIX should not try to be:

- A deeply custom low-level distro
- A kernel- or toolchain-heavy engineering project
- A fast-moving experimental platform with high maintenance cost

## Decisions Already Made

- Name: `NOKENIX`
- Origin: Roanoke, Virginia
- Base distribution: Debian, preferably `stable`
- Primary desktop environment: `KDE Plasma`
- Audience: beginner-to-intermediate desktop users
- Complexity target: conservative and maintainable
- Architecture target for v1: `amd64`
- Collaboration platform: `GitHub`
- First-release installer priority: maximum simplicity
- First-release software policy: free software only
- First-release target: closer to "daily-driver ready with branded polish" than a bare technical proof of concept

## Working Assumptions

These are not permanently locked, but they are the assumptions future planning should use unless changed explicitly.

- Primary boot target is `UEFI`
- Legacy `BIOS` support is desirable if it does not create disproportionate complexity
- The first release should be usable mostly offline after download
- The first release is a single flagship `KDE Plasma` edition
- Future desktop variants may exist later, but they are out of scope for v1 planning
- NOKENIX should feel visually distinct mainly through branding, defaults, curation, and user experience rather than deep system divergence from Debian
- Any custom package repository should start very small and only exist to support branding, defaults, installer polish, or essential project-owned packages

## Design Principles

### 1. Debian First

Prefer inheriting from Debian stable over creating custom low-level infrastructure. Any divergence from Debian should need a clear user-facing reason and a realistic maintenance story.

### 2. Simple Wins

When two approaches would both work, choose the one the club can explain, document, rebuild, and maintain with the least volunteer strain.

### 3. Polish Matters

NOKENIX should not depend on internal complexity to feel unique. Distinction should come from branding, sensible defaults, package curation, documentation, and a coherent out-of-box experience.

### 4. Reproducibility Is Required

The project should be buildable from version-controlled configuration with documented steps. A contributor should be able to reproduce the ISO from a known environment rather than relying on one maintainer's workstation state.

### 5. New Users Are First-Class

The distro should be installable and usable by someone who is new to Linux, but without stripping away normal desktop capabilities that intermediate users expect.

### 6. Free Software by Default

The initial project direction is free software only. This improves clarity of mission, but it also increases hardware compatibility risk. That tradeoff should be acknowledged explicitly in documentation and testing.

## Likely Technical Direction

This is a provisional direction, not a final implementation spec.

- ISO build system: likely `live-build`
- Installer: likely `Calamares`
- Base package source: Debian `stable`
- Release model: curated point releases on top of Debian stable
- Custom packaging scope: minimal at first
- Build environment: documented and reproducible, ideally containerized or otherwise standardized

This direction is favored because it keeps the project close to Debian, reduces bespoke infrastructure, and gives the project a realistic path to reproducible ISO generation and installer branding.

## Major Open Decisions

The following areas still need explicit decisions before implementation hardens.

### Build and Tooling

- Final choice of ISO build stack
- Whether the build environment is containerized, VM-based, or host-native
- Whether builds are local-only at first or also produced by CI

### Base System Policy

- Exact Debian branch policy and whether any use of `backports` is allowed
- Whether `BIOS` support makes the cut for v1
- Default filesystem and partitioning posture
- Update policy and support window per release

### Package and UX Defaults

- Default application suite
- Whether to include a welcome app or first-run guidance
- Software installation path for users
- Media and productivity baseline

### Branding

- Visual identity system
- Color palette
- Wallpaper direction
- Logo/wordmark
- KDE theme choices and how much project-owned theming is worth maintaining

### Installer

- Final Calamares flow
- Offline payload size target
- Partitioning defaults
- User-facing copy and branding

### Infrastructure

- Repo layout
- Documentation structure
- Issue triage model
- Website and community communications stack
- How contributors with varying skill levels can help

## Known Constraints and Risks

### Free Software Only vs Hardware Friendliness

This is the clearest tension in the current direction. A free-only policy is clean and principled, but many new users will expect Wi-Fi, graphics, and peripherals to work with minimal effort. If this policy stays, the project should document hardware expectations clearly and test accordingly.

### Offline Usability vs ISO Size

An offline-capable distro is more convenient for users but increases ISO size and curation work. This is acceptable if the package set stays disciplined.

### Distinct Branding vs Maintenance Load

Strong identity is a goal, but custom themes and heavily forked assets can become maintenance traps. Branding should focus on durable, low-overhead elements first.

### Volunteer Maintenance Capacity

Every technical choice should be evaluated against a small volunteer club's ability to document, debug, and release it repeatedly.

## Success Definition for v1

Version 1 should meet all of the following:

- Boots reliably as a live `amd64` desktop ISO
- Installs with a simple, newcomer-friendly flow
- Lands the user in a polished `KDE Plasma` desktop with coherent branding
- Includes a curated, daily-driver-ready default software set
- Can be rebuilt from version-controlled project files by another contributor following the docs
- Has a release checklist, test workflow, and basic project infrastructure in place

## Near-Term Recommendation

The project should settle the following in order before implementation expands:

1. Build stack and reproducible environment
2. Debian policy and boot/install targets
3. Package manifest and desktop defaults
4. Branding system
5. Installer customization
6. Testing and release flow

That order minimizes rework and keeps branding attached to a stable technical base rather than the other way around.
