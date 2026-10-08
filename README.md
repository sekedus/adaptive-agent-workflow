# Adaptive Agent Workflow

**Workflow version: 0.7.2**

A reusable, recovery-first workflow template for AI-assisted software development.

The workflow core is harness-agnostic at the project level: `AGENTS.md` is the portable source of truth. Harness-specific instruction files are thin adapters only. Installed identity and version metadata live in `.aaw/manifest.yml`. Canonical source: `https://github.com/sekedus/adaptive-agent-workflow`.

Designed for:

- agent harnesses that support `AGENTS.md` (for example OpenCode/OpenChamber and VS Code Copilot)
- free / low-context models
- natural-language user prompts
- model/session/IDE/device handoff
- selective use of existing skills
- bounded implementation with checkpoints and evidence
- project state that remains usable after agent interruptions

The workflow is intentionally conservative: the user does not need to type `MODE:` or repeat workflow instructions for ordinary work.

## Core idea

```text
Natural-language request
        |
        v
Intent + task-size + risk assessment
        |
        +--> DISCUSS / REVIEW
        +--> GRILL (/grill-with-docs)
        +--> PLAN (/wayfinder when large)
        +--> BUILD
        +--> FIX / diagnose
        |
        v
Selective three-pillar quality gates
        |
        v
State transaction
  -> task / roadmap / now / README as affected
        |
        v
Codebase memory + verification contract
  -> ARCHITECTURE-MAP.md / dev/verification.md when affected
        |
        v
Verification
        |
        +--> HDT when human/runtime evidence matters
        |
        v
Commit checkpoint offered when appropriate
        |
        v
Next session/model/device can recover from repository state
```

## Three primary product pillars

```text
1. Solve the Problem — Useful & Usable
2. Unique Design — Desirable & Distinctive
3. Secure by Design
```

The workflow activates the smallest meaningful quality gates for the change instead of running every skill on every task.

## Human-friendly interaction

AAW scales the amount of interaction to the work instead of forcing every change through the deepest workflow. Small local changes can remain lightweight; ambiguous, architectural, security-sensitive, or user-visible changes may use design confirmation, deeper review, and Human Development Testing (HDT).

The `/wait-what` skill is optional. AAW still provides the core behavior: explain what changed, why, how to verify it, what to expect, and what to report if it fails.

`dev/now.md` is a compact snapshot, `dev/parking-lot.md` is an active deferred queue, and task/bug records are bounded durable work records rather than chronological diaries.

## AAW maintenance and migration

AAW maintenance is a control-plane operation. Requests such as `update AAW to v7` or `migrate this project to AAW 0.7.2` enter `MIGRATION` mode before normal product intent routing. While `.aaw/migration.yml` is active, product tasks and roadmap changes are frozen. Migration preserves project state, verifies the target workflow, updates `AGENTS.md` and harness adapters last, records `AAW_VERSION` in `.aaw/manifest.yml`, removes the migration lock, and stops without executing an application task.

See [`docs/workflow/aaw-migration.md`](docs/workflow/aaw-migration.md).

## Harness portability

The workflow has one portable project instruction source:

```text
AGENTS.md
```

`AGENTS.md` contains the workflow rules, intent routing, state integrity rules, recovery protocol, codebase-understanding rules, quality-gate routing, skill dependency handling, README policy, feature/bug records, and commit policy.

The repository may also contain:

```text
.github/copilot-instructions.md
```

This file is an optional **VS Code Copilot adapter**. It must stay thin and point back to `AGENTS.md`; it must not become a second copy of the workflow.

For harnesses that support `AGENTS.md`, the installed core workflow does not require `.github/copilot-instructions.md`. For harnesses that do not support `AGENTS.md`, use that harness's project-instruction mechanism as a thin adapter while keeping `AGENTS.md` as the canonical project workflow documentation.

The `wiki/` directory is human documentation and is not a runtime dependency.

## For agents

This repository is the **template source**, not a project-specific README to copy blindly into another project.

When the user asks you to install, upgrade, downgrade, migrate, repair, clone, download, or apply the **Adaptive Agent Workflow** to a target project:

### Existing project

1. Identify the active agent harness. Prefer its native support for root `AGENTS.md` when available.
2. Obtain this template repository/archive using the available Git, download, or file tools.
3. Read the target project before changing anything.
4. Preserve the target project's existing `README.md`.
5. Copy/merge workflow files without blindly overwriting project-specific instructions or state.
6. Do not copy this template repository's root `README.md` into an existing target project.
7. Keep `wiki/` only when the user wants the workflow documentation available inside the project; otherwise it may remain only in the template source. The installed core workflow does not require `wiki/` at runtime.
8. Do not create product tasks until the target project's real objective is known.
9. Reconcile `dev/project.md`, `dev/constraints.md`, `dev/quality.md`, `dev/security.md`, `dev/roadmap.md`, `dev/now.md`, and `dev/verification.md` with the real project.
10. Initialize or reconcile `ARCHITECTURE-MAP.md` with the real codebase.
11. Validate state before claiming installation is complete.

### Empty / new project

1. Identify the active agent harness. Prefer its native support for root `AGENTS.md` when available.
2. Install the workflow files.
3. Create a **new user-facing root `README.md` for the target project**. Do not copy this template's root README verbatim because it contains agent/template instructions.
4. Keep the README concise and truthful to the project's actual state. It may begin with a project-under-definition/placeholder state.
5. Initialize `dev/project.md`, `dev/constraints.md`, `dev/quality.md`, `dev/security.md`, `dev/roadmap.md`, `dev/now.md`, and `dev/verification.md` without inventing product scope.
6. Initialize `ARCHITECTURE-MAP.md` as a project-specific codebase map (do not leave template placeholders once discovery starts).
7. Set the workflow phase to `DISCOVERY_PENDING`.
8. Do not create `T-0001` merely to represent setup. The first real task ID is created after project discovery/definition.
9. Keep `wiki/` only when the user wants the workflow documentation available inside the project; otherwise it may remain only in the template source. The agent must be able to operate from the installed core files without `wiki/`.
10. Validate the installation. By default, ask the user whether to create an **`Initial commit`**; if `dev/commit-policy.md` sets `initial: auto`, create it automatically after safety checks.

### Root README rule

The template root README is not copied into target projects. In an empty/new project, it is used only as guidance for generating the project's own README.

### After every completed task

1. Verify the task.
2. Synchronize affected state artifacts.
3. Review whether the project's root README needs a meaningful update.
4. Run a state-integrity check.
5. Apply the `task` commit policy: ask by default, or auto-commit when `task: auto` is configured and safety checks pass.
6. Never auto-commit unrelated user changes.

## Commit policy

Commit behavior is persistent per project and is stored in `dev/commit-policy.md`. The two checkpoints are independent:

```yaml
initial: ask
task: ask
```

These are the defaults. The user can change either one to `auto` at installation time or later using natural language. Auto-commit still requires verification, state-integrity checks, and a cleanly attributable commit scope. It never implies `git push`.

## Files

- `.aaw/manifest.yml` — authoritative AAW identity, canonical source, installed version, and schema metadata.
- `.aaw/migration.yml` — temporary durable migration lock/state; absent during normal operation.
- `AGENTS.md` — portable project-level operating rules, intent router, and workflow source of truth.
- `.github/copilot-instructions.md` — optional thin VS Code Copilot adapter; not the workflow source of truth.
- `CONTEXT.md` — durable domain vocabulary and agreed terminology.
- `ARCHITECTURE-MAP.md` — living codebase map: domains, ownership, dependencies, flows, hotspots, contracts, and test surfaces.
- `dev/project.md` — project purpose, scope, stack, and stable facts.
- `dev/constraints.md` — compatibility/legacy/runtime/resource constraints.
- `dev/now.md` — bounded current-state snapshot/checkpoint.
- `dev/hdt.md` — Human Development Test policy for runtime/user verification.
- `dev/milestones/` — compact milestone summaries for work broader than one task.
- `dev/roadmap.md` — milestones and direction.
- `dev/quality.md` — adaptive quality-gate policy and three-pillar quality model.
- `dev/verification.md` — concrete verification contract and evidence expectations.
- `dev/security.md` — project-specific security profile and skill routing.
- `dev/skill-dependencies.md` — known skill dependency closure.
- `dev/state-integrity.md` — state invariants and state transactions.
- `dev/readme-policy.md` — policy for the project's user-facing README.
- `dev/commit-policy.md` — persistent initial/task commit policy.
- `dev/parking-lot.md` — active deferred project ideas; promoted/resolved entries are removed.
- `dev/tasks/` — bounded executable tasks; completed tasks move to `dev/tasks/done/`.
- `dev/bug-fixes/` — standalone meaningful bug records with stable `B-*` IDs; completed records move to `dev/bug-fixes/done/`.
- `dev/milestones/` — compact summaries for broad bounded outcomes.
- `CHANGELOG.md` — release-facing history for AAW itself.
- `dev/changelog-policy.md` — optional target-project changelog guidance based on Keep a Changelog 1.1.0.
- `docs/adr/` — durable architectural decisions.
- `docs/workflow/adaptive-agent-workflow.md` — full workflow specification.
- `docs/workflow/aaw-migration.md` — agent-facing AAW migration procedure.
- `wiki/19-architecture-map-and-engineering-discipline.md` — compact architecture-map and engineering-discipline guidance.
- `wiki/21-human-development-testing.md` — HDT guidance.
- `wiki/` — complete English user and maintenance guide.

## User-facing usage

The normal user prompt can be simple:

```text
I want to build a bookmark manager.
```

or:

```text
continue
```

The workflow handles intent, task sizing, grilling, state reconciliation, skill routing, verification, and checkpointing behind the scenes.

## Installation into an empty project

Use a normal request such as:

```text
Install the Adaptive Agent Workflow in this project.
```

The agent should bootstrap the workflow, create a project README, leave product discovery pending, validate the state, and apply the `initial` commit policy (default: `ask`).

## Installation into an existing project

The agent should preserve the existing README and existing project behavior, merge workflow files carefully, and reconcile the workflow state with the real repository before implementation begins.

## Root README maintenance

The project's root README is a human-facing orientation document, not a changelog.

Update it when a new human needs to know something important about the project, especially after:

- initial project discovery;
- user-visible features;
- major architecture/integration changes;
- setup/install changes;
- important compatibility changes.

**Do not** copy every task, internal refactor, or test result into the README.

## Documentation

See [the Adaptive Agent Workflow Wiki](wiki/README.md) for the complete English usage guide, bootstrap behavior, state integrity, recovery, commit checkpoints, skill routing, and maintenance guidance.
