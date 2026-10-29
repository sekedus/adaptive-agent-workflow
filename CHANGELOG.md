# Changelog

All notable changes to Adaptive Agent Workflow are documented here.

The format is based on [Keep a Changelog 1.1.0](https://keepachangelog.com/en/1.1.0/),
and this project follows Semantic Versioning.

## [Unreleased]

### Added

### Changed

### Fixed

## [0.8.2] - 2026-10-29

### Added

- Added a dedicated agent-facing installation procedure at `docs/workflow/aaw-installation.md`.

### Changed

- Reworked the root README into a beginner-friendly guide with separate agent installation and migration routing.
- Clarified the difference between fresh installation and migration of an existing AAW installation.
- Updated migration guidance to distinguish routine 0.8.x upgrades from the historical 0.7.x-to-0.8.0 state-layout migration.
- Aligned workflow overview, wiki, agent rules, and Copilot adapter with the 0.8.1 `AWAITING_USER_REVIEW` lifecycle and milestone threshold.

### Fixed

- Corrected workflow specification, daily-usage guidance, quality checklist, and example wording that could incorrectly close `HDT: NOT_REQUIRED` tasks without waiting for user review.

## [0.8.1] - 2026-10-28

### Added

- Added `AWAITING_USER_REVIEW` as a pre-close state for tasks after verification, regardless of whether HDT is required.
- Added guidance for missing referenced attachments and for parking unrelated requests while an active task remains unfinished.

### Changed

- Clarified that `HDT: NOT_REQUIRED` skips human testing, not the pre-close user review.
- Strengthened README writing rules with beginner-focused paragraph and information-preservation guidance.
- Updated task lifecycle, state-integrity, and workflow documentation to keep tasks active until the user review is answered.


## [0.8.0] - 2026-10-20

### Added

- Moved AAW-managed workflow state and policy files from the legacy `dev/` layout into `.aaw/` while keeping human-facing project documentation in `docs/` and the root orientation files.
- Added an explicit compatibility migration procedure for 0.7.x projects, including collision-safe file moves and path-reference reconciliation.
- Added a task-first milestone rule: related small requests sharing one acceptance/verification boundary use a single task without a milestone.

### Changed

- Bumped `AAW_SCHEMA` to `2` to identify the 0.8.0 workflow-state layout.
- Made `.aaw/` the canonical location for project workflow state, task records, milestones, bug-fix records, and verification/quality policies.
- Tightened milestone criteria: create one only for a genuinely large/broad coordinated outcome needing multiple independently trackable child tasks, usually three or more (two only with real dependencies/phases/shared exit criteria); do not create or complete a one-task milestone.
- Preserved 0.7.4 task lifecycle, cancellation, HDT gates, verification-evidence reuse, and planning commit policy in the new layout.

### Fixed

- Prevented multiple related but small user requests from being wrapped in a redundant milestone when one task record is sufficient.
- Prevented task completion from automatically implying milestone completion when no genuine milestone exists.

## [0.7.4] - 2026-10-12

### Added

- Explicit task/milestone/bug-record metadata using YAML frontmatter for new and updated records.
- A `CANCELLED` task lifecycle with a dedicated `dev/tasks/cancelled/` folder and reason-preserving milestone updates.
- A `planning` commit checkpoint for completed milestone/task planning, configurable as `ask` or `auto`.
- MIT license for the AAW template repository.

### Changed

- Milestone state is reconciled whenever a linked task changes state; cancelled tasks and solely dependent exit criteria are struck through rather than removed.
- Milestones become `COMPLETE` only when all non-cancelled tasks are complete and all remaining exit criteria are satisfied; milestones whose tasks are all cancelled become `CANCELLED`.
- Verification evidence may be reused when relevant implementation/test inputs have not changed; metadata-only changes do not trigger redundant application test runs.
- Tracked records are moved with `git mv` when appropriate, and rename detection is checked without creating extra commits merely to force rename presentation.

### Fixed

- Prevented cancelled tasks from being archived as completed tasks.
- Clarified cancellation-reason handling: ask when absent and never invent a reason.
- Reduced stale milestone status/exit criteria after task completion or cancellation.
- Avoided rerunning successful product tests solely because task metadata, file paths, roadmap, milestone, or `now.md` changed.

## [0.7.3] - 2026-10-10

### Changed

- Creating a milestone from a multi-item request is planning-only unless the user explicitly authorizes implementation; child tasks remain `PLANNED`.
- Required HDT is now a hard completion gate: tasks remain active and outside `done/` until a PASS result is recorded.
- Automated checks are agent-owned when tool/environment access allows; users are not asked to repeat successful `lint`, `test`, type-check, compile, or packaging commands.
- Task templates now separate the effective HDT requirement from the HDT result/status.

### Fixed

- Prevented the first/easiest task from being implemented automatically just because a milestone was requested.
- Prevented task completion, folder movement, and normal commit prompts from happening while required HDT is still pending or failed.
- Clarified that a dependency/toolchain update is not verified by successful installation alone; applicable automated checks must run, while HDT is unnecessary when the project contract confirms no human/runtime evidence is needed.
- Clarified that unit tests for a helper do not replace a required end-to-end/runtime check for the behavior that consumes it.

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

[Unreleased]: https://github.com/sekedus/adaptive-agent-workflow/compare/v0.8.2...HEAD
[0.8.2]: https://github.com/sekedus/adaptive-agent-workflow/compare/v0.8.1...v0.8.2
[0.8.1]: https://github.com/sekedus/adaptive-agent-workflow/compare/v0.8.0...v0.8.1
[0.8.0]: https://github.com/sekedus/adaptive-agent-workflow/compare/v0.7.4...v0.8.0
[0.7.4]: https://github.com/sekedus/adaptive-agent-workflow/compare/v0.7.3...v0.7.4
[0.7.3]: https://github.com/sekedus/adaptive-agent-workflow/compare/v0.7.2...v0.7.3
[0.7.2]: https://github.com/sekedus/adaptive-agent-workflow/compare/v0.7.1...v0.7.2
[0.7.1]: https://github.com/sekedus/adaptive-agent-workflow/releases/tag/v0.7.1
