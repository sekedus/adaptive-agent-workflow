# Project State Files

The workflow separates current state, durable knowledge, work definitions, and history.

## `CONTEXT.md`

**Question answered:** What does the domain mean?

Use it for:

- domain vocabulary;
- definitions;
- agreed terminology;
- concepts that should remain consistent across sessions.

**Do not** turn it into a task log or implementation diary.

## `docs/adr/`

**Question answered:** Why did we choose this?

Use ADRs for decisions that are important, durable, and difficult to reverse.

Examples:

- database choice;
- authentication model;
- deployment architecture;
- public API strategy.

## `dev/project.md`

**Question answered:** What is this project?

Keep purpose, scope, stack, and stable project facts here.

## `dev/constraints.md`

**Question answered:** What boundaries must the implementation respect?

Examples:

- supported runtime versions;
- browser baseline;
- memory limits;
- deployment limitations;
- licensing constraints.

## `dev/roadmap.md`

**Question answered:** Where are we going?

Keep milestones and broad direction here.

## `dev/tasks/`

**Question answered:** What specific work must be done?

Each task should be bounded and executable.

## `dev/now.md`

**Question answered:** What are we doing right now?

This is the most important resume file.

It should remain small.

A good `now.md` tells a new agent:

```text
current task
current step
last completed
next action
blocker
relevant files
verification state
constraints
```

## `dev/security.md`

**Question answered:** Which security surface does this project actually have, and which security workflows apply?

Use it to record: 

- project security classification;
- trust boundaries;
- sensitive data and external integrations;
- the security domain(s) relevant to the project;
- targeted skills selected for those domains.

**Do not** turn this into a catalog of every security skill available.

## `dev/parking-lot.md`

**Question answered:** What interesting things are intentionally not being done now?

Use it to prevent new ideas from hijacking the active task.

## Git

**Question answered:** What actually changed in the worktree/history?

Git is the physical source of code state. `now.md` explains what the changes mean; Git shows what actually changed.

## Why these are separate

A common failure is keeping all of these concepts in one giant log.

That creates a document that is:

- long;
- stale;
- hard to read;
- expensive to load into a small context window;
- ambiguous about what is current.

The Adaptive Agent Workflow deliberately keeps the active state small and makes history opt-in.
