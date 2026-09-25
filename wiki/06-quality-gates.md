# Adaptive Quality Gates

The workflow uses quality gates selectively. The purpose is to increase confidence without wasting context on every task.

## 1. Classification dimensions

Before selecting gates, consider:

- task size;
- security sensitivity;
- user-visible impact;
- UI impact;
- architectural impact;
- regression risk;
- browser/runtime compatibility;
- likelihood of requiring real-world verification.

## 2. Small change

Example:

```text
Fix a typo in a label.
```

Gate:

```text
targeted verification
```

Do not run a full security audit or architecture review.

## 3. Normal feature

Example:

```text
Add bookmark tags.
```

Typical gates:

```text
behavioral tests
-> code review
```

TDD can be used when behavior is important or unclear. Matt's engineering skills currently include TDD, code review, and implementation workflows designed to keep changes bounded.

## 4. Hard bug

Example:

```text
The token occasionally expires immediately.
```

Route to:

```text
/diagnosing-bugs
```

The current skill is designed around an evidence loop: reproduce, minimize, hypothesize, instrument, fix, and regression-test.

## 5. Authentication or sensitive data

Typical gates:

```text
behavioral tests
-> targeted security review
-> relevant E2E/failure tests
-> code review
```

Do not automatically load the entire cybersecurity library.

The current Anthropic Cybersecurity Skills repository contains hundreds of specialized security workflows, including web application security and OAuth-related skills. The repository currently reports 818 skills on `main`, so selective routing is important for context economy.

## 6. UI feature

Typical gates:

```text
frontend design guidance
-> implementation
-> frontend design review
-> browser verification when appropriate
```

Anthropic's `frontend-design` skill is explicitly aimed at distinctive, intentional UI rather than generic template-like output. Microsoft's current `frontend-design-review` skill can review UI for design quality, accessibility, responsiveness, theme behavior, and implementation quality.

## 7. Browser/E2E testing

For web projects, use Playwright when actual browser behavior matters.

The current Playwright CLI skill supports browser automation, snapshots, tracing, video, storage-state workflows, test generation, and running Playwright tests. It is designed to be token-efficient compared with loading a large MCP schema into context.

## 8. Large architectural work

Typical route:

```text
/grill-with-docs (when requirements are unresolved)
        |
        v
/wayfinder
        |
        v
bounded tasks
        |
        v
implementation + verification
        |
        v
/code-review
```

The current Wayfinder guidance recommends it for work genuinely larger than one agent session, while smaller single-session planning can stay with grilling.

## 9. Architecture cleanup

Do not run a full architecture review after every tiny feature.

Use `/improve-codebase-architecture` periodically or when evidence shows architectural friction such as duplicated responsibilities, tangled dependencies, or modules becoming difficult to change.

## 10. Stress testing is layered

"Stress testing" is not one universal operation.

Depending on the feature, it can include:

```text
edge-case tests
integration tests
browser/E2E tests
failure/recovery tests
property-based tests
load/performance tests
security testing
```

Select the smallest meaningful set.

## 11. Quality-gate output

The agent should record:

```text
Gate:
Result:
Evidence:
Remaining uncertainty:
```

Never turn "no obvious issue found" into "secure" or "bug-free".
