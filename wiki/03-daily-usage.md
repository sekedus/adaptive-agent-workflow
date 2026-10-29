# Daily Usage

## 1. Start a session with ordinary language

You can simply say:

```text
continue
```

or:

```text
resume
```

The agent reads `.aaw/now.md`, resolves the current task, verifies task/roadmap state, and checks Git when relevant before continuing.

## 2. Asking a question

```text
why does this fail?
```

Expected behavior:

```text
inspect
-> diagnose
-> explain
-> do not modify production code
```

## 3. Asking for a review

```text
check the auth flow for security issues
```

Expected behavior:

```text
inspect
-> route to appropriate security workflow
-> report findings
-> do not silently apply fixes
```

## 4. Asking for a fix

```text
fix the token validation bug
```

Expected behavior:

```text
identify bounded issue
-> apply fix
-> test
-> checkpoint
```

## 5. What happens when a task finishes

A task goes through this sequence:

```text
run applicable automated checks and record results
-> decide HDT: NOT_REQUIRED or REQUIRED
-> if REQUIRED: wait for user HDT PASS while task stays active
-> review README impact, then set AWAITING_USER_REVIEW and keep the task active
-> ask whether the user wants related changes before closing
-> if changes are requested: triage them and re-verify affected checks
-> if no changes are requested: mark COMPLETE and move to done/
-> synchronize task/roadmap/now and check state integrity
-> offer/perform commit according to policy
```

If the agent already ran automated checks successfully, it reports the commands and results; it does not ask the user to repeat them. HDT is separate and asks the user to exercise real UI/runtime behavior only when required. `HDT: NOT_REQUIRED` skips the human test round, not the pre-close user review.

Triage before creating a milestone. If several related small items share one outcome and verification boundary, create one task file and no milestone. Create a milestone only when a genuinely large/broad outcome needs coordinated work across multiple independently trackable task records, usually three or more (two only when real dependencies/phases/shared exit criteria warrant it). If the user requested planning only, leave records `PLANNED`, update the roadmap/current snapshot, apply the `planning` checkpoint, and stop; do not start implementation.

A commit is recommended because it provides a durable review and recovery boundary. By default the agent asks. `planning: ask|auto` controls the checkpoint after milestone/task planning; `task: ask|auto` controls completed task checkpoints. A planning commit never authorizes implementation.

Example when HDT is not required:

> Automated checks run by the agent passed: `npm run lint`, `npm test`, and `npm run compile`. HDT is `NOT_REQUIRED` under this project's verification contract. Task `T-0001` is waiting in `AWAITING_USER_REVIEW` and remains active. Do you want any related revisions or additions before I close it?

Only after the user says there are no further changes should the agent mark the task complete, move it to `done/`, synchronize state, and follow the commit policy (which asks by default). For a task with required HDT, do not use this review prompt until the user reports a sufficient PASS result.

## 6. Initial project commit

For an empty/new project, installation itself creates the first useful recovery boundary.

After the workflow and project README are validated, the agent applies the `initial` commit policy. With the default `initial: ask`, it offers:

```text
Initial commit
```

With `initial: auto`, it creates the checkpoint automatically after the auto-commit safety checks pass.

## 7. Root README updates

The root README is updated periodically, not after every tiny change.

Update it when a task changes what a new human needs to understand, such as:

- a new user-facing feature;
- a major integration;
- setup/install instructions;
- runtime/browser support;
- high-level architecture.

**Do not** turn README into a changelog.

## 8. Introducing a new idea during active work

If the current task is:

```text
Implement OAuth callback
```

and the user says:

```text
What if we also add passkeys?
```

This is not permission to switch tasks.

Discuss or park the idea, then keep the current task unchanged unless the user clearly changes the objective.

## 9. Stopping work

You do not need a long handoff message.

A simple:

```text
I'm stopping here.
```

should cause the agent to checkpoint if the current state is safe to record.

The next session can recover from `.aaw/now.md`, task state, roadmap state, and Git evidence.
