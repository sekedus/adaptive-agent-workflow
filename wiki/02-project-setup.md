# Starting a Project

## 1. Create the project skeleton

Start with the template structure before writing a large amount of code.

The important files are:

```text
AGENTS.md
CONTEXT.md
dev/project.md
dev/constraints.md
dev/roadmap.md
dev/now.md
dev/quality.md
dev/parking-lot.md
dev/tasks/
docs/adr/
```

## 2. Give the agent a natural request

For example:

```text
I want to build a bookmark manager.
```

Do not write a long specification unless you already have one.

The agent should inspect the repository and decide whether the idea is already sufficiently defined.

## 3. Greenfield project: grill first when needed

A substantial idea normally goes through `/grill-with-docs`.

The skill should:

1. inspect the codebase and existing docs;
2. ask one useful question at a time;
3. recommend an answer when appropriate;
4. record durable domain language in `CONTEXT.md`;
5. record difficult-to-reverse decisions as ADRs;
6. leave implementation requirements clear enough to become a bounded task.

Matt Pocock's current skill set distinguishes `/grill-with-docs` for work that can be settled in one sitting from `/wayfinder` for work whose route genuinely spans multiple sessions.

## 4. Establish project constraints early

Before implementation, fill in `dev/constraints.md` with what is actually known.

Typical constraints:

```text
Runtime:
Node.js >= 20

Browser support:
Baseline / explicit browser versions

Database:
SQLite

Deployment:
Vercel

Resource constraints:
CPU-first; no GPU requirement
```

Do not invent legacy support that the project never requested.

## 5. Create the first bounded task

A task should answer:

- what must be achieved;
- why it matters;
- what is in scope;
- what is out of scope;
- acceptance criteria;
- relevant files or modules;
- how to verify it.

The first task should be small enough that a weak model can complete or checkpoint it without trying to understand the entire future product.

## 6. Establish the initial checkpoint

`dev/now.md` should identify:

```text
current task
current step
last completed action
next action
blockers
relevant files
verification state
important constraints
```

`now.md` is a current-state file. Do not turn it into a diary.
