# Feature and Bug-Fix Records

Adaptive Agent Workflow uses `dev/tasks/` for active work and two historical record areas for completed work:

```text
 dev/tasks/        active executable work
       │
       ├── completed feature ──> dev/features/
       │
       └── resolved bug ───────> dev/bug-fixes/
```

These records exist to make a project recoverable and understandable without forcing a future agent to reconstruct old chat sessions.

## Feature Records

Create `dev/features/YYYYMMDD-<feature-slug>.md` for meaningful user-facing capabilities.

A feature record should capture:

- product problem / user need;
- user-visible behavior;
- scope;
- important requirements;
- design/UX considerations;
- concise technical summary;
- relevant security considerations;
- verification evidence;
- documentation impact;
- related task, ADR, and commit;
- useful follow-up work.

**Do not** copy the entire task plan, source code, or chat transcript into the record.

### Example

A task such as:

```text
T-0012 — Add WhatsApp OTP login
```

may produce:

```text
dev/features/20260930-whatsapp-otp-login.md
```

The task contains the execution details. The feature record explains the finished capability to a future human or agent.

## Bug-Fix Records

Create `dev/bug-fixes/YYYYMMDD-<bug-slug>.md` when a bug has been investigated, fixed, and appropriately verified and the incident is worth preserving.

Capture:

- observed behavior;
- expected behavior;
- reproduction;
- impact;
- evidence-based root cause;
- fix;
- security impact;
- verification;
- regression risk;
- prevention / reusable lesson;
- related task, feature, ADR, and commit.

**Do not** create a bug record merely because an issue was reported. A report can remain in the active task while its cause and resolution are being determined.

## YAML Frontmatter

Both record types use a small, lowercase YAML frontmatter block so files are easy to search and process consistently.

## When Not to Create a Record

Avoid documentation noise for:

- typo-only fixes;
- trivial formatting changes;
- internal cleanup with no meaningful behavior change;
- changes already fully explained by an existing record.

## State Integration

Creating a feature or bug-fix record is a **state transaction**, not a replacement for the active task.

For feature completion:

```text
verify task
  → create/update feature record if warranted
  → update roadmap/now
  → review README impact
  → state-integrity check
  → commit checkpoint according to policy
```

For a resolved bug:

```text
verify fix
  → create/update bug-fix record if warranted
  → update task/now
  → update security/ADR when appropriate
  → state-integrity check
  → commit checkpoint according to policy
```

The record should reference the task and commit so the historical record can be traced back to the exact implementation.
