# State Integrity, README Updates, and Commit Checkpoints

## Why this exists

The most dangerous workflow failure is not a model forgetting a chat message. It is a repository where multiple durable artifacts disagree.

Example:

```text
now.md      -> T-0002
roadmap.md  -> T-0001
Git         -> code already implements T-0002
README      -> describes an older architecture
```

The workflow therefore treats meaningful changes as state transactions.

## Bootstrap transaction

For an empty/new project:

```text
install workflow
-> create project README
-> initialize project state
-> DISCOVERY_PENDING
-> validate
-> offer Initial commit
```

**Do not** create fake product tasks during bootstrap.

## Task creation transaction

```text
discovery complete
-> create T-0001
-> add to roadmap
-> point now.md to T-0001
-> update README if project identity changed
```

## Task completion transaction

```text
implementation
-> verification
-> task evidence
-> roadmap status
-> now next-state
-> README review
-> state-integrity check
-> commit offer
```

## Commit policy

Commit behavior is persistent in `dev/commit-policy.md` and has three independent checkpoints:

```yaml
initial: ask
planning: ask
task: ask
```

The default is to ask the user. The user may set each checkpoint to `auto`.

### `initial`

- `ask` — offer `Initial commit` after bootstrap validation.
- `auto` — create the initial checkpoint automatically after bootstrap validation and README/state creation.

### `planning`

- `ask` — offer a commit after creating/replanning a milestone and its planned task records.
- `auto` — commit the validated planning-only changes, only when no implementation or unrelated work is included.

Planning ends without starting a task unless implementation was explicitly authorized. For a combined plan-and-named-task request, skip the separate planning checkpoint and apply the task checkpoint after the bounded transaction.

### `task`

- `ask` — offer a commit after each completed and verified task.
- `auto` — automatically commit each completed and verified task.

### Auto-commit safety

Auto-commit is never blind. Before an automatic commit, the agent must:

1. verify the relevant work;
2. synchronize affected state;
3. review README impact;
4. pass state-integrity checks;
5. inspect Git status/diff;
6. confirm that unrelated user changes will not be committed.

If unrelated or ambiguous changes are present, do not auto-commit. Preserve the work and ask the user. Automatic commit never implies `git push`.

Suggested wording when the policy is `ask`:

> `T-0004` is complete and verified. A commit is recommended as a checkpoint for review and recovery. Commit now?

## README update policy

Update the root README when a new human needs to know something that changed.

Good triggers:

- project purpose established;
- user-facing capability added;
- architecture/integration changed materially;
- setup/install instructions changed;
- supported versions changed;
- operational workflow changed.

**Do not** add:

- every task;
- every test result;
- internal implementation details;
- temporary debugging notes.

The README is not a changelog.

## Cancellation and milestone reconciliation

If a task cancellation has no user-supplied reason, ask before changing the record; do not guess. Record `status: CANCELLED` and the reason in task frontmatter, move the record to `dev/tasks/cancelled/`, and strike through the task entry in its milestone. Strike through an exit criterion only if the cancelled task was the sole work needed for it. Do not delete these entries. A milestone is `COMPLETE` when every non-cancelled task is complete and every remaining exit criterion passes. If every task in a non-empty milestone is cancelled, the milestone is `CANCELLED`.

## Verification evidence reuse

Do not rerun application tests just because status metadata, Markdown paths, roadmap, milestone, or `now.md` changed. Reuse successful evidence while relevant source/test/config/dependency inputs remain unchanged; run only invalidated application checks and any necessary Markdown/state-integrity checks.
