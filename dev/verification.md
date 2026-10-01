# Verification Contract

> **Template file.** Initialize this contract after project discovery. Replace placeholders with commands and evidence that are actually valid for the project.

## Purpose

Define concrete evidence for claiming work is `TESTED` or `VERIFIED`.

## Primary Checks

```text
[primary check command]
```

Purpose:

[What this command proves.]

## Secondary Checks

| Check | Command | When required | Evidence |
|---|---|---|---|
| Lint | `[command]` | [condition] | [result] |
| Typecheck | `[command]` | [condition] | [result] |
| Unit tests | `[command]` | [condition] | [result] |
| Integration/E2E | `[command]` | [condition] | [result] |
| Build | `[command]` | [condition] | [result] |

## Manual / Runtime Verification

- [Scenario that must be checked manually or in a real runtime]

## Task Completion Contract

A task may be marked:

- `IMPLEMENTED` — code exists.
- `TESTED` — at least one relevant check was executed.
- `VERIFIED` — all required checks for the task passed and expected behavior was confirmed.
- `UNVERIFIED` — evidence is incomplete.

**Do not** claim `VERIFIED` when required project checks have not been completed.

## Context-Efficient Verification

Prefer the smallest verification set that proves the changed behavior.
**Do not** rerun unrelated full-suite checks for every tiny change unless the project requires it.
