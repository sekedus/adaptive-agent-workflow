# Installation and Prerequisites

## 1. Repository template

Copy the contents of the Adaptive Agent Workflow template into the root of a new repository.

The template intentionally does **not** contain the global skill library because this workflow assumes skills are installed globally under your agent's user-level skill directory.

For your setup, the existing global location is:

```text
%USERPROFILE%\.agents\skills\
```

## 2. Personal customization

The workflow assumes the global user preferences are installed separately:

```text
%USERPROFILE%\.copilot\instructions\
├── user-preferences.instructions.md
├── environment\
│   └── windows-10-vscode.instructions.md
└── vscode\
    ├── vscode-tools.instructions.md
    └── vscode-subagents.instructions.md
```

**Do not** copy these project-specific workflow files into every repository unless you intentionally want project-local overrides.

## 3. Skill Dependency Closure

**Do not** install only the top-level skill that the workflow names. Some skills explicitly delegate to other skills. For example, `grill-with-docs` currently calls `grilling` and `domain-modeling`; `wayfinder` uses `grilling` and `domain-modeling`, and can additionally use `research` and `prototype`; `improve-codebase-architecture` uses `codebase-design`, `domain-modeling`, and `grilling`; `tdd` uses `codebase-design`.

Install the dependency closure before testing the parent skill. See [`dev/skill-dependencies.md`](../dev/skill-dependencies.md) for the maintained matrix and commands.

## 4. Skill installer

The current `skills` CLI supports global installation with `-g` / `--global` and skill selection with `-s` / `--skill`. It can target agents explicitly or all supported agents.

For a portable global install, prefer installing only the skills you actually use.

Example:

```bash
npx skills@latest add mattpocock/skills --skill grill-with-docs --global
```

Repeat for the other selected skills.

If your current installer or agent integration does not place the skill under `%USERPROFILE%\.agents\skills\`, use the installer target appropriate to your harness or copy the complete skill directory into that location. Do not copy only `SKILL.md` when the skill has sibling `references/`, `scripts/`, or `assets/` directories.

## 5. Do not install everything blindly

Skill libraries can contain many specialized skills. Microsoft's skill documentation explicitly recommends selective loading because loading all skills can cause context dilution and context rot.

The goal is:

```text
install broadly enough to cover your common workflows
activate narrowly enough to preserve context
```

## 6. Verify installation

Use the skills CLI to inspect global skills:

```bash
npx skills list --global
```

The CLI supports `skills list`, `skills update`, and scoped global updates.

## 7. VS Code skill invocation

A skill may be manually invocable even when automatic model invocation is disabled. For this workflow, the project instructions may explicitly invoke a skill such as `/grill-with-docs` when intent routing decides that the specialized workflow is needed.

This distinction is useful:

- automatic skill discovery decides when a skill is naturally relevant;
- explicit invocation lets the workflow deliberately route a request into a specialized skill.

## 8. Optional browser automation prerequisites

For web projects, the Playwright CLI skill can be installed globally through Playwright itself:

```bash
npm install -g @playwright/cli@latest
playwright-cli install --skills --skills=agents -g
```

Playwright documents the `--skills=agents` layout for `.agents/skills` and the `-g` flag for home-directory installation. The skill is supported by GitHub Copilot and other coding agents that support locally installed skills.

If the project already has a local Playwright dependency, prefer the local CLI instead of installing another global copy.
