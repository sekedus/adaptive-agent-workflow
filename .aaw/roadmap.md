# Roadmap

> Product direction and milestone summary. Do not invent product work during workflow installation.

## Current Milestone

None yet.

## Milestones

No product milestones have been created yet.

## Task Index

No product tasks have been created yet.

## Roadmap Rules

- First triage requests into the smallest coherent work units.
- Related small items with the same outcome/verification boundary belong in one task; do not create a milestone for them.
- Create a milestone only for a genuinely large/broad outcome needing coordinated work across multiple task files (usually three or more; two only when real dependencies/phases/shared exit criteria warrant it). A few small independent tasks do not automatically need a milestone. Never create a one-task milestone.
- A milestone is a summary/navigation layer, not a second task file.
- A task is a bounded work unit with its own acceptance and verification boundary.
- Task IDs are unique and monotonic within the project.
- Do not create a task merely to record workflow installation.
- When a new milestone is planned, review `.aaw/parking-lot.md` for related project ideas and ask the user before promoting any of them.
- Active task state belongs in `.aaw/tasks/`; completed task files move to `.aaw/tasks/done/` only after all required verification gates pass. Cancelled task files move to `.aaw/tasks/cancelled/`, with the reason recorded and the task crossed out—not deleted—in its milestone.
- Creating a milestone and decomposing a multi-item request is planning-only unless the user explicitly authorizes implementation; leave child tasks `PLANNED` and stop.

- When a linked task changes state, reconcile its milestone in the same state transaction. A milestone is `COMPLETE` only when every non-cancelled task is `COMPLETE` and every non-struck exit criterion is satisfied. If all tasks are cancelled, the milestone is `CANCELLED`.
- After a standalone planning-only transaction, apply the `planning` checkpoint from `.aaw/commit-policy.md` to the relevant task/milestone state, then stop unless implementation was explicitly authorized.
