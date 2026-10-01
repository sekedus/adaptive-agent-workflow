# Harness Portability

## Core rule

Adaptive Agent Workflow is **project-workflow portable**, not tied to one chat client. The canonical project instruction source is:

```text
AGENTS.md
```

A harness adapter is optional and should remain thin.

```text
             project
                │
                ▼
          `AGENTS.md`
       canonical workflow
                │
      ┌─────────┴─────────┐
      ▼                   ▼
 Copilot adapter      Other harness adapter
 (optional)           (only if needed)
```

## OpenCode / OpenChamber

OpenCode v2 uses `AGENTS.md` as its persistent project instruction mechanism. OpenChamber is built around OpenCode and its repository also uses `AGENTS.md` for always-on rules and routing.

For these environments, the AAW core can operate without `.github/copilot-instructions.md`.

## VS Code Copilot

VS Code supports `AGENTS.md` as a cross-agent project instruction format. `.github/copilot-instructions.md` remains a useful Copilot-specific adapter. Keep it short and defer to `AGENTS.md` instead of duplicating workflow rules.

## Other harnesses

Support depends on the harness. Before claiming compatibility, verify its current project-instruction discovery rules.

Use this order:

1. Check whether the harness discovers root `AGENTS.md`.
2. If yes, use AAW directly.
3. If no, identify the harness-native project instruction file.
4. Create a thin adapter that points the agent to `AGENTS.md`.
5. Do not create a second workflow implementation.

## Wiki is optional

`wiki/` is for human documentation. Agents should be able to execute the workflow from the installed core files without it. Keep the wiki in the project only when the user wants local workflow documentation.

## Personal customization is optional

AAW does not require a separate personal customization package. Personal instructions can improve interaction style or environment-specific behavior, but the project workflow must remain self-contained.

## Source of truth hierarchy

```text
AGENTS.md
  = project workflow and agent behavior

CONTEXT.md / dev/* / docs/adr/*
  = project state and durable knowledge

.github/copilot-instructions.md
  = optional Copilot adapter

wiki/
  = human documentation

personal user instructions
  = user-specific interaction/environment preferences
```

## Important distinction

Harness portability does not mean every tool, skill, MCP server, or subagent mechanism is portable. The workflow should detect the harness capabilities and adapt those execution details while preserving the same project state and workflow semantics.
