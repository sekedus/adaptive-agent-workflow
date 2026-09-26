# Adaptive Agent Workflow

A reusable, recovery-first workflow template for AI-assisted software development.

Designed for:

- GitHub Copilot Chat in VS Code
- free / low-context models
- natural-language user prompts
- model/session/IDE/device handoff
- selective use of existing skills
- bounded implementation with checkpoints and evidence

The workflow is intentionally conservative: the user does not need to type `MODE:` or repeat workflow instructions for ordinary work.

## Core idea

```text
Natural-language user request
        |
        v
Intent + task-size + risk assessment
        |
        +--> DISCUSS / REVIEW
        |
        +--> GRILL (/grill-with-docs)
        |
        +--> PLAN (/wayfinder when large)
        |
        +--> BUILD
        |
        +--> FIX / diagnose
        |
        v
Selective three-pillar quality gates
        |
        v
Checkpoint -> dev/now.md
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

When the user asks you to install, clone, download, or apply the **Adaptive Agent Workflow** to an existing or new project:

1. Obtain this template repository/archive using the available Git, download, or file tools.
2. Copy the workflow files into the target project.
3. **Do not copy or overwrite the template repository's root `README.md`.** The target project's existing `README.md` belongs to that project and must be preserved unless the user explicitly asks to replace it.
4. Preserve the target project's existing source code and unrelated documentation.
5. Merge carefully when a target file already exists; do not blindly overwrite project-specific `AGENTS.md`, `.github/copilot-instructions.md`, `CONTEXT.md`, or other instruction/state files.
6. Read the target repository first and adapt the template to the existing stack and conventions.
7. Keep `wiki/` only when the user wants the workflow documentation available inside the project; otherwise it may remain only in the template source.
8. After installation, initialize or reconcile `dev/project.md`, `dev/constraints.md`, `dev/now.md`, `dev/roadmap.md`, and `dev/quality.md` for the target project.
9. Run a lightweight validation before claiming installation is complete: confirm the required files exist, check for conflicting instructions, and verify that `dev/now.md` reflects the real project state.

The installation itself is a **configuration task**, not an invitation to refactor the target project.

When the target project already contains similar workflow files, prefer merging compatible rules over replacing them. Preserve existing project-specific requirements unless they conflict with an explicit user request.

## Files

- `AGENTS.md` — project-level operating rules and intent router.
- `.github/copilot-instructions.md` — thin VS Code entry point; keeps Copilot aligned with `AGENTS.md`.
- `CONTEXT.md` — durable domain vocabulary and agreed terminology.
- `dev/project.md` — project purpose, scope, stack, and important constraints.
- `dev/constraints.md` — compatibility/legacy/runtime/resource constraints.
- `dev/now.md` — the primary current-state checkpoint.
- `dev/roadmap.md` — milestones and direction.
- `dev/quality.md` — adaptive quality-gate policy and three-pillar quality model.
- `dev/security.md` — project-specific security profile and security-skill routing.
- `dev/parking-lot.md` — unrelated ideas that should not hijack the active task.
- `dev/tasks/` — bounded executable tasks.
- `docs/adr/` — durable architectural decisions.
- `docs/workflow/adaptive-agent-workflow.md` — full workflow specification.
- `wiki/` — complete English user and maintenance guide for the workflow.

## Install into a new project

The normal user-facing request can be simple, for example:

```text
Install sekedus/adaptive-agent-workflow in this project.
```

The agent should inspect the current repository, obtain the template, preserve the existing project README, and merge the workflow files into the project.

For a new, empty project, the same request can initialize the workflow before implementation begins.

## Start development

Once installed, the user can communicate naturally, for example:

```text
I want to build a bookmark manager.
```

For a non-trivial or ambiguous product idea, the agent should inspect the repository and invoke `/grill-with-docs` before implementation.

For a small, obvious change, it should not create unnecessary ceremony.

## Resume

```text
continue
```

The agent reads `dev/now.md`, the current task, and only relevant files. If the previous session may have been interrupted, it reconciles the recorded state with `git status`, relevant diffs, and verification evidence before continuing.

## Important rule

Chat history is temporary. The repository is the durable memory.

## Documentation

See [the Adaptive Agent Workflow Wiki](wiki/README.md) for the complete English usage guide, setup instructions, recovery procedures, skill routing, and maintenance guidance.
