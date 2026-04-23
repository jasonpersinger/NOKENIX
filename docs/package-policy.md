# NOKENIX Package Policy

## Purpose

This document sets the initial rules for how packages enter NOKENIX.

The goal is to keep the image useful, offline-capable, and maintainable without turning package selection into an unbounded wishlist.

## Current Baseline

- Debian base: `trixie`
- Archive area: `main` only
- Desktop baseline: `live-task-kde`
- Backports: not enabled by default
- Custom package repository: not yet in use

## Initial Rules

### 1. Prefer Debian Packages As-Is

If Debian `main` already provides the package and it works for the use case, prefer it over custom packaging.

### 2. Avoid Duplicate Applications

Do not ship multiple default apps for the same common task unless there is a clear reason.

Examples:

- One default browser
- One primary office suite
- One primary PDF viewer
- One primary media player

### 3. Offline Utility Matters

Default packages should make the system useful immediately after install without assuming the user will fetch more software right away.

### 4. Packaging Ownership Should Stay Small

If NOKENIX introduces project-owned packages later, they should start with low-risk categories:

- Branding assets
- Desktop defaults
- Thin configuration packages
- Installer-specific settings

### 5. No Backports by Habit

Backports should not become the default answer to every newer-package request. If the project adopts backports later, the policy should name which package categories qualify and why.

## Current Open Questions

- What is the smallest daily-driver app set that still feels complete offline?
- Should NOKENIX ship a software center by default?
- Should the first release include office software by default or leave that to post-install choice?
- Which packages are essential for new users versus just nice to have?

## Near-Term Goal

Turn the current `live-task-kde` baseline into a first explicit default package manifest with a short rationale for each category.
