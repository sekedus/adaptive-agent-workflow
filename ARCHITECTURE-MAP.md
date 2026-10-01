# Architecture Map

> **Template file.** When this workflow is installed into a target project, replace this placeholder map with the actual project's living codebase map during project discovery. Do not leave the template examples as if they describe the target project.

## Status

TEMPLATE

## Purpose

A compact navigation map for the codebase. This is not a full architecture essay and not a duplicate of `dev/project.md`.

Use it to answer quickly:

- Where does a capability live?
- Which module/domain owns it?
- What does it depend on?
- Who depends on it?
- What are the important execution/data flows?
- Which files/modules are hotspots or fragile boundaries?
- What contracts must not regress?
- Where are the relevant tests?

## Map

### Project Domains

| Domain / Area | Primary Path(s) | Responsibility | Key Dependencies | Consumers | Tests |
|---|---|---|---|---|---|
| [Domain] | `src/...` | [Responsibility] | [Dependencies] | [Consumers] | `tests/...` |

### Entry Points

- [Entry point] — [purpose]

### Important Flows

#### [Flow name]

```text
input
  -> [module]
  -> [module]
  -> output
```

### Hotspots / Sensitive Boundaries

| Area | Why sensitive | Contract / Risk | Verification |
|---|---|---|---|
| [Path/module] | [Reason] | [Invariant] | [Test/check] |

### Reusable Capabilities

| Capability | Existing Implementation | How to Reuse |
|---|---|---|
| [Capability] | `src/...` | [Pattern/API] |

### Test Surface

- Unit: `tests/...`
- Integration: `tests/...`
- E2E: `tests/e2e/...`

## Update Rule

Update this map in the same state transaction when a change materially alters:

- module/domain ownership;
- dependencies or boundaries;
- execution/data flows;
- entry points;
- public contracts;
- important hotspots;
- test surfaces.

Do not rewrite the map for trivial implementation changes that do not alter the codebase's shape.
