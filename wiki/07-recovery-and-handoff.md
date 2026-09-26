# Recovery, Context Limits, and Handoff

## Why recovery is a first-class feature

An agent session can stop unexpectedly because of:

- context-window exhaustion;
- free-model quota/limit;
- network loss;
- tool failure;
- IDE restart;
- agent crash;
- user interruption.

The workflow assumes this will happen.

## 1. Never trust the last attempted operation

If an agent says:

```text
I am implementing token validation now.
```

and then the session dies, do not assume the implementation did not happen.

It may have:

- changed 0 files;
- changed 1 file;
- partially changed several files;
- changed the files successfully but failed before running tests.

## 2. Reconciliation protocol

On resume:

```text
read dev/now.md
        |
        v
read current task
        |
        v
git status
        |
        v
git diff
        |
        v
inspect relevant source
        |
        v
run targeted verification
        |
        v
reconcile actual state
        |
        v
continue
```

Classify the task as:

```text
COMPLETE
PARTIAL
UNCHANGED
INCONSISTENT
```

## 3. Partial work is not failure

If the agent changed half the files and then died, recover the partial work instead of blindly restarting.

Example:

```text
now.md says:
Implement token validation.

Working tree:
reset-token.ts modified
reset-service.ts modified

tests:
not yet run
```

The next agent should inspect the diff, understand what already exists, finish only the missing work, and test it.

## 4. Context danger zone

**Do not** wait for the advertised context window to reach 100%.

For weaker/free models, treat high context utilization as a reason to stop at the next safe boundary.

A practical rule is:

```text
bounded unit complete
-> verify
-> update now.md
-> handoff/checkpoint
-> new session
```

The exact threshold depends on the model and IDE. Do not hard-code one universal token percentage into the repository.

## 5. Use `/handoff` when useful

Use `/handoff` when:

- the current session has become large;
- a task is at a clean boundary;
- the user is changing models;
- the next session needs a concise bridge.

Handoff should not duplicate the whole project. Durable information belongs in project artifacts such as `CONTEXT.md`, ADRs, tasks, and `now.md`.

## 6. Recovery across devices

On the same machine:

```text
git worktree + dev/now.md
```

may be enough.

On another device:

```text
git commit
-> git push
-> clone/pull on next device
```

The workflow cannot synchronize uncommitted code across devices by documentation alone.

## 7. Resume command

The user can simply say:

```text
continue
```

The agent should do the reconciliation work automatically.

## 8. Do not use chat history as a backup

If the project can only be resumed by searching an old conversation, the checkpoint system is incomplete.
