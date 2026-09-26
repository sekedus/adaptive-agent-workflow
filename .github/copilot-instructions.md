# Project Copilot Instructions

This repository uses the Adaptive Agent Workflow defined in `AGENTS.md`.

Before working on a task:

1. Read `AGENTS.md`.
2. Read `dev/now.md`.
3. Read the current task referenced by `dev/now.md` when one exists.
4. Read only the project documents relevant to the task.

Follow the natural-language intent, scope-control, recovery, checkpoint, and adaptive-quality rules in `AGENTS.md`.

Do not require the user to provide workflow labels such as `MODE: BUILD`.

When a substantial or ambiguous feature/product idea requires requirements discovery, explicitly invoke `/grill-with-docs` when available.

When work becomes large or likely to exceed the current context, prefer bounded tasks, checkpoints, and `/wayfinder` or `/handoff` when appropriate.

Do not modify production code for questions, explanations, or review requests unless the user clearly requests implementation/fixing.


Product-quality routing:

- Solve the Problem — Useful & Usable
- Distinctive Design — Desirable & Distinctive
- Secure by Design

Use `dev/quality.md` and `dev/security.md` to select only the relevant quality and security skills for the current change. Do not require the user to name the correct security skill manually.
