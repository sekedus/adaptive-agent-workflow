# Adaptive Agent Workflow

**Workflow version: v5**

A reusable, recovery-first workflow template for AI-assisted software development.

Designed for:

- GitHub Copilot Chat in VS Code
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
Verification
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

## For agents

This repository is the **template source**, not a project-specific README to copy blindly into another project.

When the user asks you to install, clone, download, or apply the **Adaptive Agent Workflow** to a target project:

### Existing project

1. Obtain this template repository/archive using the available Git, download, or file tools.
2. Read the target project before changing anything.
3. Preserve the target project's existing `README.md`.
4. Copy/merge workflow files without blindly overwriting project-specific instructions or state.
5. Do not copy this template repository's root `README.md` into an existing target project.
6. Keep `wiki/` only when the user wants the workflow documentation available inside the project; otherwise it may remain only in the template source. The installed core workflow does not require `wiki/` at runtime.
7. Do not create product tasks until the target project's real objective is known.
8. Reconcile `dev/project.md`, `dev/constraints.md`, `dev/quality.md`, `dev/security.md`, `dev/roadmap.md`, and `dev/now.md` with the real project.
9. Validate state before claiming installation is complete.

### Empty / new project

1. Install the workflow files.
2. Create a **new user-facing root `README.md` for the target project**. Do not copy this template's root README verbatim because it contains agent/template instructions.
3. Keep the README concise and truthful to the project's actual state. It may begin with a project-under-definition/placeholder state.
4. Initialize `dev/project.md`, `dev/constraints.md`, `dev/quality.md`, `dev/security.md`, `dev/roadmap.md`, and `dev/now.md` without inventing product scope.
5. Set the workflow phase to `DISCOVERY_PENDING`.
6. Do not create `T-0001` merely to represent setup. The first real task ID is created after project discovery/definition.
7. Keep `wiki/` only when the user wants the workflow documentation available inside the project; otherwise it may remain only in the template source. The agent must be able to operate from the installed core files without `wiki/`.
8. Validate the installation. By default, ask the user whether to create an **`Initial commit`**; if `dev/commit-policy.md` sets `initial: auto`, create it automatically after safety checks.

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

- `AGENTS.md` — project-level operating rules and intent router.
- `.github/copilot-instructions.md` — thin VS Code entry point.
- `CONTEXT.md` — durable domain vocabulary and agreed terminology.
- `dev/project.md` — project purpose, scope, stack, and stable facts.
- `dev/constraints.md` — compatibility/legacy/runtime/resource constraints.
- `dev/now.md` — primary current-state checkpoint.
- `dev/roadmap.md` — milestones and direction.
- `dev/quality.md` — adaptive quality-gate policy and three-pillar quality model.
- `dev/security.md` — project-specific security profile and skill routing.
- `dev/skill-dependencies.md` — known skill dependency closure.
- `dev/state-integrity.md` — state invariants and state transactions.
- `dev/readme-policy.md` — policy for the project's user-facing README.
- `dev/commit-policy.md` — persistent initial/task commit policy.
- `dev/parking-lot.md` — unrelated ideas that should not hijack active work.
- `dev/tasks/` — bounded executable tasks; `.task-template.md` is a template only.
- `docs/adr/` — durable architectural decisions.
- `docs/workflow/adaptive-agent-workflow.md` — full workflow specification.
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
Install sekedus/adaptive-agent-workflow in this project.
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
