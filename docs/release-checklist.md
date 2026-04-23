# NOKENIX Release Checklist

## Purpose

This is the future release gate for NOKENIX. It starts simple on purpose.

## Pre-Release

- Build completes from a clean documented environment
- ISO filename, version, and target release are correct
- Checksums are generated
- Release notes draft exists

## VM Smoke Test

- ISO boots to the live environment
- Automated boot smoke test passes with either the explicit serial marker or the documented fallback success indicators
- Desktop session reaches `KDE Plasma`
- User can open system settings and file manager
- Shutdown and reboot work

## Installer

- Installer launches from the live session
- Install completes without manual recovery steps
- Installed system boots successfully
- First login succeeds

## Packaging and Policy

- Default package set matches the documented manifest
- No unreviewed extra archive areas are enabled
- No accidental backports or project-local package sources are present

## Release Artifacts

- ISO is uploaded
- Checksums are uploaded
- Any signature workflow is completed
- Release notes are published

## Post-Release

- Known issues are recorded
- Immediate regressions are triaged
- The next milestone is updated in project docs
