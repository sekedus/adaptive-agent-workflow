# Adaptive Agent Workflow — Project Rules

## 1. Source of Truth

The repository is the durable project memory.

When resuming work, read in this order:

1. `dev/now.md`
2. the current task referenced by `dev/now.md`
3. only the project documents relevant to the task
4. the relevant source/tests

Do not reconstruct project state from old chat history when the repository already contains the state.

---

## 2. Natural-Language Intent

The user normally communicates in natural language. Do not require explicit workflow labels such as `MODE: BUILD`.

Infer intent from:

- the user's request;
- the current project state;
- the current task;
- repository evidence;
- available tools and skills.

Use these internal intent categories when useful:

- `DISCUSS` — explain, compare, brainstorm, or answer questions.
- `REVIEW` — inspect behavior, code, security, performance, design, or correctness.
- `PLAN` — define scope, acceptance criteria, or implementation steps.
- `BUILD` — implement a clearly requested change.
- `FIX` — apply a requested or approved fix.
- `RESUME` — recover and continue the recorded task.
- `HANDOFF` — checkpoint without starting new work.

The user does not need to name these modes.

---

## 3. Clarification vs. Grilling

Do not ask a question merely because something is technically ambiguous.

Before asking:

1. inspect the relevant code;
2. inspect existing project documentation;
3. inspect existing patterns;
4. use appropriate tools.

Ask only when unresolved ambiguity materially affects correctness, security, architecture, irreversible decisions, important user-visible behavior, or scope.

For low-risk, reversible decisions consistent with existing project patterns, make the smallest reasonable assumption and state it briefly.

For a new product/feature idea with multiple meaningful unresolved decisions, explicitly invoke `/grill-with-docs` when available.

Do not grill trivial or already-defined changes.

---

## 4. Execution Boundary

Questions, explanations, and review requests do not grant production-code modification permission.

Examples that normally do **not** permit editing:

- "Why does this fail?"
- "Can you check this?"
- "Could this be a security issue?"
- "How would you fix this?"
- "What do you think?"

Clear action-oriented requests normally permit implementation within scope:

- "Fix this."
- "Add this."
- "Implement this."
- "Change this."
- "Remove this."

When intent is uncertain, prefer the least destructive interpretation.

---

## 5. Scope Control

Do not expand the active task merely because related improvements are visible.

Do not silently:

- refactor unrelated code;
- upgrade unrelated dependencies;
- rename unrelated files;
- redesign adjacent modules;
- add nice-to-have features;
- rewrite working code without evidence.

Unrelated ideas go to `dev/parking-lot.md` or become a separate task.

A bare confirmation such as `yes`, `do that`, or `go ahead` refers only to the immediately preceding actionable proposal. Before executing, resolve what that proposal actually includes and keep it bounded.

---

## 6. Task Size Triage

Do not infer task size from prompt length.

Estimate size from actual repository impact after inspection.

### Small

Direct, local, low-risk change with clear scope.

Action: implement, verify, checkpoint.

### Medium

Multiple files or behavioral decisions, but still bounded.

Action: plan as needed, implement in bounded units, verify each meaningful unit.

### Large / Cross-cutting

Many modules, architectural changes, major product features, migration work, or work likely to exceed one context window.

Action: clarify/grill when needed, use `/wayfinder` when available, create bounded tasks, and do not attempt the whole change in one conversation.

---

## 7. Context Discipline

Context is a limited resource.

Prefer:

- current task;
- relevant files;
- focused tool calls;
- existing project artifacts;
- incremental verification;
- durable checkpoints.

Avoid reading the entire repository or all historical logs without a reason.

When the session is becoming large enough that continued work risks compaction, failure, or loss of focus:

1. finish only the smallest safe bounded unit;
2. verify it;
3. update `dev/now.md`;
4. use `/handoff` when useful;
5. stop the current execution rather than consuming the remaining context blindly.

A new session must be able to continue from repository state without the previous chat.

---

## 8. Interruption / Recovery Protocol

A session may stop because of context limits, free-model limits, connection errors, tool failures, IDE crashes, or other interruptions.

Never assume the last attempted operation completed.

On resume:

1. read `dev/now.md`;
2. read the current task;
3. inspect `git status`;
4. inspect relevant diffs;
5. compare the repository with the checkpoint;
6. run targeted verification when needed;
7. classify the state as complete, partially complete, unchanged, or inconsistent;
8. reconcile the checkpoint before continuing.

Repository state and verification evidence are stronger than unverified chat claims.

Do not blindly repeat an interrupted operation.

---

## 9. Checkpoint Rule

A checkpoint is required after a meaningful bounded unit of implementation, verification, decision-making, or a significant interruption.

The checkpoint lives in `dev/now.md`.

At minimum it records:

- current status;
- current task;
- current step;
- last completed action;
- exact next action;
- blockers;
- relevant files;
- verification state;
- important assumptions/constraints;
- whether the current work is verified.

`dev/now.md` is a current-state document, not a chronological diary.

---

## 10. Skills, Quality Gates, and the Three Pillars

Evaluate meaningful product work through three pillars:

1. **Solve the Problem** — Useful & Usable
2. **Distinctive Design** — Desirable & Distinctive
3. **Secure by Design** — Security is part of the design and verification process

Use specialized skills when they provide a materially better workflow than ad-hoc reasoning.
Do not invoke expensive or large skills for trivial tasks.
Route selectively using `dev/quality.md` and `dev/security.md`.

Examples:

- ambiguous/new feature → `/grill-with-docs`
- large/cross-cutting change → `/wayfinder`
- unclear previous explanation → `/wait-what`
- debugging/root cause → `/diagnosing-bugs`
- test-first behavioral work → `/tdd`
- implementation review → `/code-review`
- codebase-wide architecture friction → `/improve-codebase-architecture`
- UI creation or redesign → `/impeccable` and/or a suitable frontend-design skill
- UI validation → `frontend-design-review` / Playwright when appropriate
- security-sensitive change → classify the attack surface in `dev/security.md`, then invoke targeted cybersecurity skill(s)
- handoff/context pressure → `/handoff`

Do not require the user to know the name of a security skill. Infer the security domain from the project attack surface and use `dev/security.md` to route it.

Explicitly invoke a skill when the workflow requires it, even if the skill is configured as manually invoked.

---

## 11. Quality Claims

Do not claim that something is fixed, secure, compatible, complete, or tested without evidence appropriate to the claim.

Distinguish clearly between:

- implemented;
- tested;
- verified;
- assumed;
- not tested.

---

## 12. Style and Existing Patterns

Before introducing a new pattern, abstraction, dependency, naming convention, or file organization:

1. inspect nearby existing code;
2. prefer the established project pattern when it is sound;
3. document a meaningful deliberate deviation.

Do not make code "more optimal" by adding speculative abstractions.

Prefer the smallest simple solution that fits current requirements and project conventions.

---

## 13. Compatibility / Legacy

Never silently invent a legacy-support target.

Read `dev/constraints.md` before making runtime/browser/platform compatibility decisions.

If a baseline is missing and the decision materially affects implementation, establish the baseline before proceeding.

---

## 14. New Ideas During Work

A new idea is not automatically a task switch.

When an unrelated idea appears:

1. capture it in `dev/parking-lot.md` when useful;
2. keep the active task unchanged;
3. switch projects/tasks only when the user explicitly changes direction.

---

## 15. Natural-Language Resume

When the user says things such as:

- `continue`
- `resume`
- `lanjutkan`
- `what's next?`
- `continue where we stopped`

interpret this as `RESUME`.

Read `dev/now.md` first and reconcile the workspace if necessary.

Do not require the user to repeat workflow instructions.

---

## 16. Output Style

Keep technical explanations concise and readable.

When the user is likely unfamiliar with a programming language or framework:

- say what changed;
- say why it matters;
- explain unfamiliar terms briefly;
- use small concrete examples when useful.

Do not add motivational filler.
