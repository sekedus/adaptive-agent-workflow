# Adaptive Agent Workflow

A lightweight, recovery-first workflow for AI-assisted software development.

Designed for:

- GitHub Copilot Chat in VS Code
- free / low-context models
- natural-language user prompts
- model/session/IDE/device handoff
- selective use of existing skills
- bounded implementation with automatic checkpoints

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
Selective quality gates
        |
        v
Checkpoint -> dev/now.md
        |
        v
Next session/model/device can recover from repository state
```

## Files

- `AGENTS.md` — project-level operating rules and intent router.
- `.github/copilot-instructions.md` — thin VS Code entry point; keeps Copilot aligned with `AGENTS.md`.
- `CONTEXT.md` — durable domain vocabulary and agreed terminology.
- `dev/project.md` — project purpose, scope, stack, and important constraints.
- `dev/constraints.md` — compatibility/legacy/runtime/resource constraints.
- `dev/now.md` — the primary current-state checkpoint.
- `dev/roadmap.md` — milestones and direction.
- `dev/quality.md` — adaptive quality-gate policy and skill routing.
- `dev/parking-lot.md` — unrelated ideas that should not hijack the active task.
- `dev/tasks/` — bounded executable tasks.
- `docs/adr/` — durable architectural decisions.
- `docs/workflow/adaptive-agent-workflow.md` — full workflow specification.

## Start a new project

Copy this template into the repository, then ask naturally, for example:

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

See the [Adaptive Agent Workflow Wiki](wiki/README.md) for the complete English usage guide, recovery procedures, and recommended skills.
