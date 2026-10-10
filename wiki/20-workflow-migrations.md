# Workflow Migrations

AAW 0.7.1 introduced a dedicated control plane for upgrading, downgrading, repairing, or migrating the workflow itself.

## Natural-language request

The user does not need a migration command. Examples:

```text
update AAW to v0.7.3
update adaptive-agent-workflow to 0.7.3
upgrade this project to AAW 0.7.3
```

The agent detects workflow maintenance rather than application work.

## Version metadata

The authoritative installed version is `.aaw/manifest.yml`:

```yaml
AAW_ID: adaptive-agent-workflow
AAW_SOURCE: https://github.com/sekedus/adaptive-agent-workflow
AAW_VERSION: 0.7.3
AAW_SCHEMA: 1
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
dev/project.md
dev/constraints.md
dev/roadmap.md
dev/now.md
dev/tasks/
dev/tasks/done/
dev/bug-fixes/
dev/bug-fixes/done/
dev/milestones/
docs/adr/
existing Git changes
```

For 0.7.0+, `ARCHITECTURE-MAP.md` and `dev/verification.md` must describe the real project. They are not template content to copy verbatim.

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

Existing projects should reconcile, rather than blindly replace, the following: compact `dev/now.md`, active-only `dev/parking-lot.md`, adaptive task templates, milestone summaries, standalone `B-*` bug records, done folders, `dev/hdt.md`, and the compact `dev/verification.md` contract.
