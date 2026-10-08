# Task, Milestone, and Bug Records

AAW keeps active work in `dev/tasks/`, broad bounded outcomes in `dev/milestones/`, and meaningful standalone bug records in `dev/bug-fixes/`.

## Tasks

A task is a bounded work unit, not one user message.

A new request may be merged into an active task when these align:

- same domain/area;
- same or compatible acceptance criteria;
- same verification boundary;
- small enough that the combined task remains understandable.

Otherwise, create a separate task or park the idea.

Keep small task files concise. Use deeper planning/evidence sections only when the work needs them.

## Milestones

A milestone groups several related tasks when one task is too narrow for the request but a second roadmap system is unnecessary.

A milestone should contain:

- objective;
- scope/out-of-scope;
- exit criteria;
- task index;
- important constraints/decisions;
- related parking-lot candidates that the user explicitly promoted.

The milestone is a summary/navigation layer, not a copy of task execution details.

## Bugs

If a bug is discovered while working on the current task and is still inside that task's scope, keep it in the task.

For a standalone meaningful bug, use a stable ID:

```text
B-0001-<bug-slug>.md
```

**Do not** create a standalone bug record merely because an issue was reported. The active investigation belongs in a task until the outcome is known.

## Done Folders

Keep active folders easy to scan:

```text
dev/tasks/
  T-xxxx-*.md
  done/
    T-xxxx-*.md

dev/bug-fixes/
  B-xxxx-*.md
  done/
    B-xxxx-*.md
```

Git preserves historical movement, so active folders do not need to retain resolved records.
