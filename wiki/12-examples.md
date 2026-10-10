# End-to-End Examples

## Example 1: New small feature

User:

```text
add a clear button to the search box
```

Agent route:

```text
inspect UI
-> existing pattern found
-> small task
-> implement
-> targeted test/check
-> checkpoint
```

No grill. No Wayfinder. No security audit.

## Example 2: Ambiguous feature

User:

```text
I want subscriptions
```

Agent route:

```text
new non-trivial feature
-> inspect codebase
-> /grill-with-docs
-> record context/ADR
-> create bounded task
-> implement
-> verify
```

## Example 3: Hard bug

User:

```text
Sometimes login works and sometimes it immediately logs me out.
```

Agent route:

```text
REVIEW
-> /diagnosing-bugs
-> reproduce/minimize
-> instrument
-> identify cause
-> propose/apply fix according to user intent
-> regression test
-> checkpoint
```

## Example 4: User only asks about security

User:

```text
Can this auth flow be exploited?
```

Agent route:

```text
REVIEW
-> inspect auth code
-> targeted security workflow
-> findings
-> stop before code modification
```

User then says:

```text
fix the first issue
```

Agent route:

```text
FIX
-> apply bounded fix
-> test
-> checkpoint
```

## Example 5: UI design

User:

```text
Make the dashboard feel less generic.
```

Agent route:

```text
inspect existing UI
-> choose appropriate design skill
-> implement distinctive direction
-> frontend-design-review
-> browser verification when useful
```

## Example 6: Large feature

User:

```text
Add multi-device sync, offline mode, conflict resolution, and account recovery.
```

Agent route:

```text
large/cross-cutting
-> /grill-with-docs
-> /wayfinder
-> bounded tasks
-> implementation sessions
-> verification per task
-> periodic architecture/code review
```

**Do not** attempt the entire feature in one chat.

## Example 7: Very long user prompt, tiny actual problem

User provides a long description of an error.

Agent discovers:

```text
missing `await`
```

Route:

```text
small bug
-> fix
-> run targeted test
-> checkpoint
```

Prompt length does not define task size.

## Example 8: Tiny user prompt, huge actual task

User says:

```text
yes, do that
```

The immediately preceding proposal involves migrating the database.

The agent should recognize the referenced action as a large task and route accordingly instead of treating `yes` as a tiny task.

## Example 9: Agent dies halfway through implementation

Before failure:

```text
T-0031 token validation
```

After failure:

```text
dev/now.md says implementation started

git diff shows two modified files

tests were not run
```

Resume:

```text
reconcile
-> inspect diff
-> finish partial implementation
-> test
-> checkpoint
```

**Do not** restart blindly.

## Example 10: Switching projects

You are working on Project A and suddenly want to work on Project B.

Use:

```text
checkpoint A
-> switch to B
```

When returning weeks later:

```text
open A
-> continue
-> reconcile
-> resume the exact recorded task
```

## Example 11: Empty project installation

User:

```text
Install the Adaptive Agent Workflow in this project.
```

Expected route:

```text
bootstrap
-> create project README
-> initialize DISCOVERY_PENDING state
-> validate
-> apply initial commit policy
```

**Do not** invent `T-0001` merely to represent installation.

## Example 12: Create a milestone without starting implementation

User:

```text
Here are seven new tasks. Group them into a milestone.
```

Expected behavior:

```text
inspect and group the requested outcomes
-> create M-xxxx with PLANNED status
-> create bounded child task records, all PLANNED
-> update roadmap and now snapshot
-> ask about related parking-lot ideas if any
-> summarize the plan
-> STOP (no product implementation)
```

**Do not** start the easiest first task. A milestone-creation request is planning authorization, not implementation authorization. Start coding only when the user explicitly asks to implement a task.

## Example 13: Automated verification vs required HDT

For a toolchain-only change such as a TypeScript version upgrade, when the project contract says automated checks are sufficient, the agent runs the relevant type-check/lint/test/build checks and reports their results. Successful package installation alone is not enough, but no manual HDT is needed when the contract confirms there is no relevant runtime behavior to test. The agent does not ask the user to repeat successful commands.

For a session-eviction change in a VS Code extension, if the project's verification matrix requires EDH for session/runtime behavior, HDT is `REQUIRED` even if unit tests pass. The agent reports automated results, sets the task to `AWAITING_HDT`, keeps it in `dev/tasks/`, and gives only the manual EDH steps. It must not say HDT is not required, mark the task complete, move it to `done/`, or offer the completion commit before the user reports PASS.

## Example 14: Completed task and commit checkpoint

User:

```text
finish the task
```

After the implementation and all required verification gates are satisfied, the agent should apply `dev/commit-policy.md`. If HDT is required, the task is not complete until the user reports PASS. With the default `task: ask`, offer the commit only after that gate passes; with `task: auto`, create the checkpoint only after all gates pass.

The agent should:

```text
run automated checks
-> resolve HDT requirement
-> if required, wait for HDT PASS
-> mark COMPLETE and move task to done/
-> update roadmap if status changed
-> update now
-> review README impact
-> state-integrity check
-> offer commit if uncommitted
```

Example offer:

> `T-0003` is complete and verified. The changes are uncommitted. A commit is recommended as a checkpoint for review and recovery. Commit now?

The agent should not auto-commit unless explicitly authorized.

