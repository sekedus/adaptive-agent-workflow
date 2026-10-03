# Architecture Map and Engineering Discipline

## Why 0.7.0 adds this

Adaptive Agent Workflow is not only a task-state system. A new session also needs to understand the **shape of the codebase** without reading the entire repository.

`ARCHITECTURE-MAP.md` is the living navigation map for that purpose.

## What belongs in the map

Keep only information that helps an agent find and reason about code:

- domains and module ownership;
- entry points;
- important dependencies;
- execution/data flows;
- sensitive boundaries and hotspots;
- reusable capabilities;
- public or internal contracts worth protecting;
- test surfaces.

**Do not** turn it into a second README, full design document, or file-by-file index.

## When to update it

Update it when a task materially changes:

- module/domain ownership;
- dependency relationships;
- entry points;
- execution/data flow;
- public contracts;
- important hotspots;
- test locations or test boundaries.

**Do not** update it for trivial changes that do not alter the codebase shape.

## Trace before patching

For a bug or non-trivial behavior change, do not assume the first suspicious file is the root cause.

```text
symptom
  -> reproduce
  -> trace real flow
  -> identify shared/root cause
  -> smallest correct fix
  -> regression test
```

This reduces repeated symptom patches and helps low-context agents avoid making the codebase more complex than necessary.

## Reuse ladder

Before adding a helper, abstraction, or dependency:

```text
1. Existing project capability
2. Standard library / platform API
3. Already-installed dependency
4. New abstraction / dependency
```

Move down the list only when the previous level does not satisfy the current requirement.

## Verification contract

Use `dev/verification.md` to define the actual commands and evidence expected for the project.

The separation is intentional:

```text
quality.md
  -> what should be checked

verification.md
  -> how this project proves it
```

This prevents agents from inventing a generic "done" standard.

## Relationship to the other AAW state files

```text
ARCHITECTURE-MAP.md
    = how the codebase is shaped

CONTEXT.md
    = what domain terms mean

dev/tasks/
    = what work must be done

dev/now.md
    = what is happening now

dev/verification.md
    = how completion is proven

git
    = what actually changed
```
