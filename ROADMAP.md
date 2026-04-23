# NOKENIX Roadmap

## Objective

Turn NOKENIX from a project concept into a reproducible, branded, Debian-based `KDE Plasma` distro that a small community team can build, test, and release.

This roadmap is organized into phases. Each phase has a purpose, key decisions, deliverables, and explicit verification criteria.

## Phase 0: Foundation and Repository Setup

### Purpose

Create the project structure and decision record before technical build work starts.

### Deliverables

- Project repository initialized on `GitHub`
- Core docs committed
- Basic repo structure agreed
- Decision log established
- Contribution model kept simple enough for club members to follow

### Recommended Outputs

- `PROJECT_CONTEXT.md`
- `ROADMAP.md`
- `DECISIONS.md`
- `CONTRIBUTING.md`
- `docs/` directory for deeper technical notes
- `build/` or similarly named directory reserved for ISO configuration

### Verify

- A new contributor can read the repo root and understand the project direction
- Open decisions are clearly separated from decided ones
- There is one obvious place for future build configuration

## Phase 1: Tooling and Build Environment

### Purpose

Choose the build method and make it reproducible.

### Decisions Needed

- `live-build` vs alternatives
- Host-native vs containerized build environment
- Local-only builds vs local plus CI builds
- Artifact naming and output structure

### Provisional Recommendation

Use `live-build` as the primary ISO generation tool and standardize the build environment so contributors can produce the same output with minimal host drift.

### Deliverables

- Build tooling decision recorded
- Build prerequisites documented
- First build script or command path documented
- Reproducible build environment defined

### Verify

- A contributor can prepare the environment from docs
- The build process completes from version-controlled config
- Two clean builds produce equivalent expected outputs at the artifact level

## Phase 2: Base System Decisions

### Purpose

Lock the technical policy for what NOKENIX is inheriting from Debian and what it is changing.

### Decisions Needed

- Debian `stable` exact usage policy
- Whether `backports` are allowed and under what conditions
- `UEFI`-only vs `UEFI` plus `BIOS`
- Free-only package policy implications
- Filesystem and partitioning defaults
- Offline package payload target

### Deliverables

- Base system policy written down
- Boot/install targets defined
- Archive component policy defined
- Release support expectations defined

### Verify

- The team can explain the distro's Debian relationship in one page
- The base install target is clear enough to guide build config
- Hardware compatibility expectations are explicitly documented

## Phase 3: Live ISO and Desktop Baseline

### Purpose

Produce a bootable live environment with the right desktop foundation.

### Decisions Needed

- Display manager choice
- Session defaults
- Networking, printing, and basic device support defaults
- What "daily-driver baseline" means for v1

### Deliverables

- Bootable live ISO
- KDE Plasma session configured sanely
- Desktop defaults documented
- Baseline system services selected

### Verify

- ISO boots in a VM to a live desktop
- Desktop session is stable and understandable for a new user
- Core workflows work: network, display settings, storage browsing, shutdown, reboot

## Phase 4: Default Application Suite and Configuration

### Purpose

Curate the software set so the distro is useful immediately after install.

### Decisions Needed

- Default browser
- Office suite inclusion
- Media player choice
- Archive utility, image viewer, PDF support
- Software installation interface
- Whether to include a welcome app

### Deliverables

- Versioned package manifest
- Default app rationale documented
- KDE defaults tuned for the chosen suite

### Verify

- A new user can browse, edit documents, view PDFs, manage files, and play common local media without extra setup
- The ISO remains within an acceptable size target
- No obvious duplication exists in the default app set

## Phase 5: Branding and Identity

### Purpose

Make NOKENIX feel distinct without creating avoidable maintenance burden.

### Decisions Needed

- Logo or wordmark direction
- Color palette
- Wallpaper direction
- Login, splash, and installer branding depth
- Whether theme customization is project-owned or mostly curated from existing upstream assets

### Deliverables

- Branding guide
- Wallpaper set or initial wallpaper pack
- KDE branding defaults
- Boot and installer branding assets where feasible

### Verify

- The distro is recognizably NOKENIX from boot to desktop
- Branding is cohesive across major touchpoints
- Asset maintenance burden stays reasonable

## Phase 6: Installer and First-Run Experience

### Purpose

Turn the live system into a simple installation experience for newcomers.

### Decisions Needed

- Final installer stack and module selection
- Partitioning defaults and warnings
- Offline install payload content
- Post-install cleanup behavior
- First-run guidance or welcome experience

### Deliverables

- Installer integrated and branded
- Installation flow documented
- First-boot expectations defined

### Verify

- Installation succeeds in at least one VM scenario end to end
- Installed system boots cleanly
- First login experience is polished and comprehensible

## Phase 7: Testing, Release, and Project Operations

### Purpose

Create the minimum viable release process the club can repeat.

### Decisions Needed

- Versioning scheme
- Release cadence
- Manual vs automated test coverage
- Checksums, signatures, and download hosting
- Issue triage and release ownership

### Deliverables

- Release checklist
- Smoke test checklist
- Candidate ISO naming scheme
- Basic CI where practical
- Release notes template

### Verify

- The team can produce a release candidate intentionally rather than ad hoc
- Test results are recorded consistently
- Users can verify they downloaded the correct ISO

## Phase 8: Community Infrastructure and Contributor Paths

### Purpose

Make it easy for club members with different skill levels to contribute.

### Contribution Tracks

- Build and packaging
- Documentation
- QA and installer testing
- Branding and wallpapers
- Website/community operations

### Deliverables

- Contributor onboarding guide
- Simple issue labels and triage workflow
- Clear list of beginner-safe tasks
- Communication norms for the project

### Verify

- A new volunteer can find a first task without private guidance
- Non-packaging contributors have meaningful work they can do
- Build and release ownership is not concentrated in one person

## Suggested Milestones

### Milestone A

Project documents, repo structure, and decision process are in place.

### Milestone B

First reproducible live ISO boots to KDE in a VM.

### Milestone C

Installer works and produces a bootable installed system.

### Milestone D

Default app suite and branding are coherent enough for a public preview.

### Milestone E

Release candidate passes the project checklist and is ready for wider club testing.

## Immediate Next Steps

1. Create `DECISIONS.md` and record the currently locked choices.
2. Choose the build stack, with `live-build` as the default candidate.
3. Define the initial repo layout for build config, docs, and assets.
4. Write the first reproducible build environment notes.
5. Decide the initial default package set at a high level before touching branding details.

## Current Recommendation

The next working session should focus on Phase 1 and produce a concrete technical proposal for:

- Repository layout
- Build tool selection
- Build host requirements
- Reproducible build workflow
- Installer integration strategy

That is the right place to get specific, because it drives nearly every downstream decision.
