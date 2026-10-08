# Architecture Map and Engineering Discipline

## Compact by design

`ARCHITECTURE-MAP.md` is a **navigation map**, not a second architecture document.

The agent should be able to answer:

- where a capability lives;
- who owns the domain/module;
- what important dependencies/relationships exist;
- which execution/data flows cross boundaries;
- where sensitive contracts/hotspots are;
- where the relevant tests live.

It should **not** attempt to document every function, historical investigation, test run, or implementation detail.

The source code remains authoritative for implementation details. The map tells the agent where to inspect next.

## Update only when shape changes

Update the map when a task materially changes ownership, dependencies, entry points, flows, contracts, hotspots, or test boundaries.

**Do not** update it for a trivial change merely to show that the task touched something.

## Trace before patching

For non-trivial bugs or behavior changes:

```text
symptom
  -> reproduce
  -> trace actual flow
  -> identify shared/root cause
  -> smallest correct fix
  -> regression verification
```

## Reuse / YAGNI

```text
existing project capability
    -> standard/platform API
    -> existing dependency
    -> new abstraction/dependency only when justified
```

Avoid creating abstractions solely for hypothetical reuse.

## Verification

`dev/verification.md` is the project's compact verification contract.

Keep historical evidence in the task/bug record or Git history rather than growing the verification contract with old test reports.

## State boundaries

```text
AGENTS.md
  = workflow instructions

dev/* state
  = project data / workflow state

ARCHITECTURE-MAP.md
  = codebase navigation map

docs/
  = human project documentation
```
