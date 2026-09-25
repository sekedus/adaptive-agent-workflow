# Adaptive Quality Gates

The goal is not to run every review/skill on every change.

Select only the gates that match the change's size, risk, and affected domain.

## Gate Selection

### Simple / Local Change

Use when the change is small, obvious, and low-risk.

Minimum:

- targeted verification/test when applicable;
- inspect the final diff for accidental changes.

Avoid heavyweight skill invocation.

### Normal Feature

Use when the change affects multiple files or user-visible behavior but remains bounded.

Minimum:

- targeted tests;
- appropriate code review;
- compatibility check when relevant.

### Large / Cross-Cutting Feature

Use when the change spans modules, architecture, migrations, or likely exceeds one context window.

Use:

- `/grill-with-docs` when requirements are ambiguous;
- `/wayfinder` for large work when available;
- bounded tasks;
- checkpoint after meaningful units;
- `/code-review` before considering the implementation complete.

### Bug / Unknown Failure

Use:

- `/diagnosing-bugs` when available;
- reproduce or establish an observable failure;
- apply the smallest fix;
- regression test;
- verify.

### Security-Sensitive Change

Examples:

- authentication;
- authorization;
- sessions/tokens;
- file uploads;
- payments;
- untrusted input;
- secrets;
- externally reachable services.

Use targeted security skills relevant to the changed attack surface. Do not invoke an entire cybersecurity catalog unnecessarily.

A useful source is `mukul975/Anthropic-Cybersecurity-Skills` when installed and appropriate.

Security review is not the same as a security guarantee. Prefer actual tests/tool evidence where possible.

### UI / Frontend Change

For a new or substantially redesigned UI:

- use an appropriate frontend-design/taste skill when distinctive design is required;
- use frontend-design review when available;
- use Playwright/browser verification when behavior or responsive layout matters.

Do not run large design workflows for a one-line CSS correction.

### Behavior / Regression Work

Use `/tdd` when test-first development materially improves confidence.

Prefer tests around public behavior rather than implementation details.

### Stress / Failure Testing

Do not interpret "stress testing" as one universal test.

Select relevant categories:

- edge cases;
- invalid input;
- repeated actions;
- concurrency/race conditions;
- network failure;
- timeout/retry behavior;
- browser/E2E behavior;
- load/performance tests when the system needs them.

For web applications, Playwright/browser tooling can provide valuable real-browser verification.

### Codebase-Wide Architecture Review

Do not perform architecture refactoring after every task.

Use `/improve-codebase-architecture` or an equivalent architecture review periodically or when repeated changes reveal structural friction.

## Review Sequence

Prefer this sequence:

```text
implement
  -> targeted verification
  -> selective quality gates
  -> code review
  -> checkpoint
```

For higher-risk work:

```text
implement
  -> tests
  -> security / UI / E2E / failure checks as appropriate
  -> code review
  -> checkpoint
```

## Evidence Levels

Use these labels in task notes when useful:

- `IMPLEMENTED` — code exists.
- `TESTED` — a relevant automated/manual test was executed.
- `VERIFIED` — expected behavior was confirmed with appropriate evidence.
- `UNVERIFIED` — work exists but evidence is incomplete.
