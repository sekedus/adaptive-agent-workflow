# Workflow Migrations

AAW 0.7.1 introduced a dedicated control plane for upgrading, downgrading, repairing, or migrating the workflow itself.

## Natural-language request

The user does not need a migration command. Examples:

```text
update AAW to v0.8.0
update adaptive-agent-workflow to 0.8.0
upgrade this project to AAW 0.8.0
```

The agent detects workflow maintenance rather than application work.

## Version metadata

The authoritative installed version is `.aaw/manifest.yml`:

```yaml
AAW_ID: adaptive-agent-workflow
AAW_SOURCE: https://github.com/sekedus/adaptive-agent-workflow
AAW_VERSION: 0.8.0
AAW_SCHEMA: 2
```

Legacy labels normalize as `v6 -> 0.6.0` and `v7 -> 0.7.0`.

Older projects without a manifest must be inspected using concrete repository evidence. If the installed release remains uncertain, stop instead of guessing.

## MIGRATION mode

Migration has higher priority than normal product intents.

```text
AAW maintenance request
        -> MIGRATION
        -> freeze product work
        -> migrate workflow
        -> verify
        -> update control instructions last
        -> update manifest
        -> remove lock
        -> stop
```

While `.aaw/migration.yml` exists with `status: ACTIVE`:

- no product task is created or executed;
- roadmap and active task state are preserved;
- unrelated user changes are preserved;
- a new session resumes migration before normal work.

## Why a lock is necessary

`AGENTS.md` controls agent behavior, but `AGENTS.md` is also one of the files being migrated. Chat history is not durable enough to serve as migration state. The lock gives the repository a durable recovery signal.

## Why migration is not a T-* task

Product tasks describe application work. A workflow migration changes the mechanism that executes future application work. Mixing them creates ambiguity about whether the agent should build the product or maintain the workflow. Migration therefore uses control-plane state and does not consume a product task ID.

## State preservation

Migration should merge workflow-owned files rather than blindly copying the template over the repository. Preserve, unless a target release explicitly requires a workflow-only change:

```text
README.md
CONTEXT.md
.aaw/project.md
.aaw/constraints.md
.aaw/roadmap.md
.aaw/now.md
.aaw/tasks/
.aaw/tasks/done/
.aaw/bug-fixes/
.aaw/bug-fixes/done/
.aaw/milestones/
docs/adr/
existing Git changes
```

For 0.7.0+, `ARCHITECTURE-MAP.md` and `.aaw/verification.md` must describe the real project. They are not template content to copy verbatim.

## Completion

A migration is complete only when:

```text
manifest -> target AAW_VERSION
workflow files -> target release
product state -> preserved
verification -> passed
migration lock -> removed
```

After completion, the agent stops. It must not interpret the same request as permission to start or resume application work.

See [`docs/workflow/aaw-migration.md`](../docs/workflow/aaw-migration.md) for the agent-facing procedure.


## 0.7.2 workflow ergonomics

During 0.7.2 migration, existing projects should reconcile, rather than blindly replace, the following legacy paths: compact `dev/now.md`, active-only `dev/parking-lot.md`, adaptive task templates, milestone summaries, standalone `B-*` bug records, done folders, `dev/hdt.md`, and the compact `dev/verification.md` contract.

## 0.7.4 lifecycle integrity

When migrating to 0.7.4, reconcile record lifecycle without bulk-rewriting historical files: new/materially updated task, milestone, and bug records use YAML frontmatter; create `dev/tasks/cancelled/` and `dev/bug-fixes/cancelled/`; preserve user-supplied cancellation reasons and never infer missing ones; reconcile linked milestones when task state changes; add the `planning` commit checkpoint; and document verification-evidence reuse. If a legacy task is already marked `CANCELLED` but stored in `dev/tasks/done/`, move it to `dev/tasks/cancelled/` and strike through its milestone entry. If its reason is missing, ask the user; never invent one.


## 0.8.0 — State directory migration

AAW 0.8.0 moves workflow-managed state from the legacy `dev/` layout into `.aaw/`. `.aaw/manifest.yml` is authoritative; `AAW_SCHEMA` is `2`. `docs/` remains for human-facing project documentation and ADRs.

During migration from 0.7.x, move only known AAW-owned files and folders, preserving IDs, frontmatter, status, cancellation reasons, HDT evidence, and milestone history. Use `git mv` for tracked records when possible. If both the old and new paths exist, reconcile instead of overwriting. Do not move unrelated source code or user files that happen to reside under `dev/`, and do not delete that directory if unrelated contents remain. Update only references that point to AAW-managed paths.

New task triage is task-first: several related small changes that share a verification boundary become one task. Create a milestone only for a genuinely large/broad coordinated outcome needing multiple task files (usually three or more; two only when real dependencies/phases/shared exit criteria warrant it). Never create or complete a milestone for a single task. Migration itself remains `MIGRATION` control-plane work and must stop after verification.
