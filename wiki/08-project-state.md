# Project State Files

The workflow separates current state, durable knowledge, work definitions, human orientation, and Git history. AAW-managed workflow state belongs under `.aaw/`; human-facing project docs remain under `docs/`.

## Root `README.md`

**Question answered:** How should a new human understand this project?

It is a concise orientation document, not a changelog.

Update it when project understanding changes materially.

## `CONTEXT.md`

**Question answered:** What does the domain mean?

Use it for domain vocabulary, definitions, agreed terminology, and concepts that should remain consistent across sessions.

## `docs/adr/`

**Question answered:** Why did we choose this?

Use ADRs for decisions that are important, durable, and difficult to reverse.

## `.aaw/project.md`

**Question answered:** What is this project?

Keep purpose, scope, stack, and stable project facts here.

## `.aaw/constraints.md`

**Question answered:** What boundaries must the implementation respect?

## `.aaw/roadmap.md`

**Question answered:** Where are we going?

It is the authoritative index of milestones and task IDs. Do not invent tasks during bootstrap.

## `.aaw/tasks/`

**Question answered:** What specific work must be done?

Each task is bounded and executable. New or materially updated tasks use YAML frontmatter as canonical metadata; status is not duplicated in the body. Small tasks should stay concise; a user message is not automatically a new task.

## `.aaw/milestones/`

**Question answered:** What broad bounded outcome groups these tasks?

Use a milestone only for a genuinely large/broad coordinated outcome needing multiple independently tracked task files, usually three or more; two only when real dependencies, phases, or shared exit criteria make coordination valuable. A few small independent tasks do not automatically need a milestone. Keep it as a compact summary/navigation layer and update it whenever a linked task changes state. Do not delete cancelled task entries; strike them through. A milestone whose tasks are all cancelled is `CANCELLED`, not `COMPLETE`.

## `.aaw/bug-fixes/`

**Question answered:** What meaningful standalone bugs were resolved?

Use stable `B-xxxx-<slug>.md` IDs. Bugs found inside an active task stay in that task when they remain in scope. Completed records move to `done/`; cancelled records move to `cancelled/` after a reason is recorded. A task cancellation must remain visible (struck through) in its linked milestone.

## `.aaw/tasks/cancelled/`

**Question answered:** Which task work was explicitly cancelled, and why?

Keep the reason in task frontmatter; do not guess it. This is separate from `done/` because cancelled work is not completed work.

## `.aaw/hdt.md`

**Question answered:** When and how should a human/runtime test be performed?

Use HDT only when automated checks do not fully prove the required behavior.

## `.aaw/parking-lot.md`

**Question answered:** Which project-related ideas are intentionally deferred?

It is an active queue, not an archive. Remove entries when promoted, rejected, or resolved.

## `.aaw/now.md`

**Question answered:** What are we doing right now?

This is the primary resume/checkpoint file and navigation layer.

It is intentionally short and is **not** a chronological diary or absolute source of truth when it conflicts with durable artifacts or Git evidence.

## `.aaw/state-integrity.md`

**Question answered:** How do these state artifacts stay consistent?

Use it for invariants and state-transition rules.

## `.aaw/readme-policy.md`

**Question answered:** When should the user-facing README change?

## `.aaw/security.md`

**Question answered:** Which security surface does this project have, and which security workflows apply?

## `.aaw/changelog-policy.md`

**Question answered:** When should this project keep a human-facing changelog?

Use it when the project has meaningful release-facing history. The file is optional for small/private projects.

## `CHANGELOG.md`

**Question answered:** What meaningful changes should humans know about between releases?

When present, prefer Keep a Changelog 1.1.0. Do not turn it into a task or commit dump.

## Git

**Question answered:** What actually changed?

Git is the physical source of code/worktree history.

## `.aaw/` is workflow state; `docs/` is project documentation

`.aaw/manifest.yml` identifies the installed AAW release. The rest of `.aaw/` contains workflow-managed state and policy: current snapshot, roadmap, tasks, milestones, verification/HDT, quality/security, commit policy, and parking lot. This directory is normally tracked by Git so another session or agent can recover the project.

Use `docs/` for human-facing project documentation such as design docs and ADRs. Do not put AAW runtime state back under `dev/` in a 0.8.x project. During migration from 0.7.x, move only known AAW-owned files, not unrelated application files that happen to live under `dev/`.

## Why these are separate

A common failure is treating one file as the entire project's memory. The workflow instead uses layers:

```text
README          human orientation
CONTEXT         domain memory
project         project identity
constraints     boundaries
roadmap         direction + task index
tasks           bounded work
now             current execution checkpoint
ADRs            durable decisions
Git             actual repository state
```

When these contradict each other, reconcile before continuing.
