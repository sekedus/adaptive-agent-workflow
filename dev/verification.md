# Verification Contract

> Template file. Initialize this contract after project discovery.
> Keep it compact: define how this project proves a change is correct, not the history of every check ever run.

## Purpose

Define the minimum credible evidence for moving work from `IMPLEMENTED` to `TESTED` or `VERIFIED`.

## Primary Checks

```text
[primary check command]
```

Purpose:

[What this proves.]

## Change -> Verification Matrix

| Change type | Minimum evidence | Extra evidence when applicable |
|---|---|---|
| docs/text | link/render/readability check | user-facing documentation review |
| logic | targeted automated test/check | regression or integration test |
| UI | targeted automated/browser check | HDT when runtime/user interaction matters |
| integration | integration check | real runtime/manual evidence |
| security-sensitive | targeted security test/review | abuse/failure-path verification |
| architecture | affected tests + code review | ADR / broader verification |

Replace the generic rows with the project's actual commands and requirements after discovery.

## Secondary Checks

| Check | Command | When required |
|---|---|---|
| Lint | `[command]` | [condition] |
| Typecheck | `[command]` | [condition] |
| Unit tests | `[command]` | [condition] |
| Integration/E2E | `[command]` | [condition] |
| Build | `[command]` | [condition] |

## Manual / Runtime Verification

[Only scenarios that cannot be credibly proven by automated checks. Link or summarize the expected human action.]

## Human Development Test (HDT)

See `dev/hdt.md`.

HDT is recommended or required only when real human/runtime behavior matters. It is not mandatory for every task.

## Completion Vocabulary

- `IMPLEMENTED` — code or project content exists.
- `TESTED` — at least one relevant check was executed.
- `VERIFIED` — all required checks for the task passed and expected behavior was confirmed with suitable evidence.
- `UNVERIFIED` — evidence is incomplete.

Do not claim `VERIFIED` merely because a command exited successfully when the project's actual behavior still requires human/runtime confirmation. For each task, resolve any project-level `recommended` guidance into an effective task-level `REQUIRED` or `NOT_REQUIRED` HDT decision and record the reason in the task. A `REQUIRED` HDT blocks completion until PASS.

Run available automated checks as the agent and record their real results. Do not ask users to repeat commands that already passed in the current worktree. Ask for user execution only when the agent cannot run a required check and the user's environment/access is genuinely needed; distinguish that from an HDT manual/runtime test.

## Evidence Retention

Keep the contract itself stable. Put task-specific commands/results, HDT reports, and historical evidence in the task record or another appropriate durable record. Git history preserves exact file-level history.
