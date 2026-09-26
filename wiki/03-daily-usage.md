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

The agent should read `dev/now.md`, the referenced task, and only the relevant project material.

## 2. Asking a question

Example:

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
-> apply the fix
-> test
-> checkpoint
```

## 5. Continuing after a previous proposal

A short message such as:

```text
yes
```

or:

```text
do that
```

must be interpreted using the immediately preceding actionable proposal, not as permission to execute an entire unrelated roadmap.

Before executing, the agent should know exactly what "that" means.

## 6. Introducing a new idea during active work

Suppose the current task is:

```text
Implement OAuth callback
```

and the user says:

```text
What if we also add passkeys?
```

This is not permission to switch tasks.

The idea should be discussed or recorded in `dev/parking-lot.md` unless the user clearly chooses to change the active objective.

## 7. Stopping work

You do not need to write a long handoff message.

A simple:

```text
I'm stopping here.
```

should cause the agent to checkpoint if the current state is safe to record.

The next session can then recover from `dev/now.md` and the actual repository state.
