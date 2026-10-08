# Changelog

All notable changes to Adaptive Agent Workflow are documented here.

The format is based on [Keep a Changelog 1.1.0](https://keepachangelog.com/en/1.1.0/),
and this project follows Semantic Versioning.

## [Unreleased]

### Added

### Changed

### Fixed

## [0.7.2] - 2026-10-08

### Added

- Explicit AAW identity and canonical source metadata in `.aaw/manifest.yml`.
- Adaptive interaction/checkpoint guidance for light, normal, and deep work.
- Durable pending-decision guidance so user approval is never inferred from a new session or compaction.
- Human Development Test (HDT) as an optional gate for changes that need real human/runtime evidence.
- Milestone templates for requests that are broader than one bounded task.
- `tasks/done/` and `bug-fixes/done/` lifecycle folders.
- Core `WAIT-WHAT` behavior without making the `/wait-what` skill a dependency.

### Changed

- Task records are adaptive: small tasks stay concise; medium/large tasks may use deeper planning and evidence sections.
- `dev/now.md` is a bounded current-state snapshot, not a chronological diary.
- `dev/parking-lot.md` is an active deferred queue; promoted, rejected, or resolved entries are removed.
- Active work remains in `dev/tasks/`; bugs found inside an active task stay in that task when they remain in scope.
- Standalone bug records use stable `B-xxxx-<slug>.md` IDs rather than date-prefixed filenames.
- Completed task and bug records move to `done/` instead of remaining in active folders.
- `dev/features/` is removed; meaningful feature work is represented by tasks, milestones, ADRs, README/docs, or changelog entries as appropriate.
- README guidance is stricter about human readability and keeping history out of the README.
- `ARCHITECTURE-MAP.md` is explicitly a compact navigation map, not an architecture encyclopedia.
- `dev/verification.md` is a compact project verification contract; historical evidence belongs in task/bug records or Git history.
- State synchronization follows affected-artifact scope instead of updating every project document after every task.
- AAW state files are project data; `AGENTS.md` remains the workflow instruction authority.

### Fixed

- Reduced stale-state patterns caused by append-only `now.md` and `parking-lot.md` histories.
- Clarified task merging: a new small request may join an active task only when scope, domain, acceptance, and verification boundaries genuinely align.
- Clarified that design agreement and implementation authorization are separate decisions when a change warrants an explicit confirmation checkpoint.

## [0.7.1] - 2026-10-03

### Added

- AAW migration control plane, manifest, and durable migration lock.
- State-preserving, resumable, and verifiable migration rules.

[Unreleased]: https://github.com/sekedus/adaptive-agent-workflow/compare/v0.7.2...HEAD
[0.7.2]: https://github.com/sekedus/adaptive-agent-workflow/compare/v0.7.1...v0.7.2
[0.7.1]: https://github.com/sekedus/adaptive-agent-workflow/releases/tag/v0.7.1
