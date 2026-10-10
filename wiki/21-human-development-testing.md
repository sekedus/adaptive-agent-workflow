# Human Development Testing (HDT)

HDT is a human-run verification gate for behavior that automated checks cannot fully prove. It is separate from linting, automated tests, type checks, builds, and packaging.

## Decide Whether HDT Is Required

Read the project's `dev/verification.md` and set the effective task decision to `REQUIRED` or `NOT_REQUIRED`, with a short reason. Runtime-dependent user-visible behavior, extension/browser/IDE host behavior, integration/lifecycle/permission flows, and any change the project verification contract marks as required need HDT. If a project's matrix requires EDH for session/runtime changes, that requirement applies even when helper unit tests pass. Unit tests for a helper do not prove an entire integration path. Diff size alone is not decisive, but a large or cross-boundary change should trigger closer scrutiny.

Toolchain-only changes can be `NOT_REQUIRED` when the agent has run the relevant automated checks and the project's verification contract says they provide sufficient evidence. Installing/updating a dependency without error is not sufficient by itself.

## Flow

```text
implementation
  -> agent runs automated checks and reports results
  -> NOT_REQUIRED: mark complete only after automated evidence is recorded
  -> REQUIRED: set AWAITING_HDT; keep task active/in progress; give manual test steps
  -> user reports observations
  -> PASS: record evidence, mark COMPLETE, move to done/, then apply commit policy
  -> FAIL/unclear: keep task active; investigate/fix or request missing evidence; repeat relevant test
```

If required HDT is pending, failed, or declined, the task must not be marked `COMPLETE`, moved to `done/`, or offered the normal completed-task commit checkpoint. A user's refusal does not silently waive the gate. An explicitly requested partial checkpoint commit leaves the task incomplete.

## Do Not Ask Users to Repeat Agent-Run Checks

If the agent already ran `npm test`, lint, compile, type-check, packaging, or equivalent automated checks successfully, report the actual results. Do not ask the user to rerun those same commands as another verification step. Ask the user to execute a command only when the agent could not run it and access to the user's environment is genuinely needed; label this as an unverified automated check, not HDT.

## Human Test Instructions

1. What to open/run.
2. What action to take.
3. What result to expect.
4. What information to report if it differs.

Treat the user's report as evidence, not as an unconditional status command. Clear PASS completes the gate; FAIL requires investigation/fix; ambiguous evidence requires one targeted follow-up.
