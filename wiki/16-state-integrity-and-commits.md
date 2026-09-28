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

## Commit offer

The workflow does not auto-commit by default.

The agent should offer a commit when:

- the initial project bootstrap is validated;
- a task is completed and verified;
- a meaningful checkpoint is reached and the user is likely to benefit from a durable snapshot.

Suggested language:

> `T-0004` is complete and verified. The changes are uncommitted. A commit is recommended as a checkpoint for review and recovery. Commit now?

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
