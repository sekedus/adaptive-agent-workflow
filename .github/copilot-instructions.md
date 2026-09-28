# Project Copilot Instructions

This repository uses the Adaptive Agent Workflow defined in `AGENTS.md`.

Before working on a task:

1. Read `AGENTS.md`.
2. Read `dev/now.md`.
3. If a current task exists, verify it against `dev/roadmap.md` and read its task file.
4. Inspect `git status` and relevant diffs when resuming or when commit state matters.
5. Read only project documents relevant to the task.

Do not require the user to provide workflow labels such as `MODE: BUILD`.

Installation/bootstrap is not product development. Do not invent product tasks during workflow installation. For an empty/new project, create a concise project README, initialize project state, and offer an `Initial commit` checkpoint.

Before `continue`, `resume`, or `what's next?`, perform a lightweight state-integrity check across `now.md`, the current task, roadmap, and Git when relevant.

When a substantial or ambiguous feature/product idea requires requirements discovery, explicitly invoke `/grill-with-docs` when available and resolve its dependency closure first.

When work becomes large or likely to exceed the current context, prefer bounded tasks, checkpoints, and `/wayfinder` or `/handoff` when appropriate.

Do not modify production code for questions, explanations, or review requests unless the user clearly requests implementation/fixing.

After every completed task:

- verify the task;
- synchronize affected state artifacts;
- check whether the root README needs a meaningful update;
- verify the state is consistent;
- offer a commit when relevant changes are uncommitted.

Do not auto-commit unless explicitly authorized.

Three-pillar product quality:

- Solve the Problem — Useful & Usable
- Unique Design — Desirable & Distinctive
- Secure by Design

Use `dev/quality.md` and `dev/security.md` to select only the relevant quality and security skills for the current change. Do not require the user to name the correct security skill manually.
