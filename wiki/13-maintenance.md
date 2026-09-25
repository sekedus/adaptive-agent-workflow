# Maintenance

## 1. Keep the workflow small

Do not turn `AGENTS.md` into a giant prompt encyclopedia.

Keep stable orchestration rules in `AGENTS.md`.
Keep domain terms in `CONTEXT.md`.
Keep project constraints in `dev/constraints.md`.
Keep current execution state in `dev/now.md`.
Keep specialized behavior in skills.

## 2. Add a new rule only after a real failure

When an agent makes a mistake, ask:

```text
Is this a missing general rule?
Or is this an isolated mistake?
```

Add a permanent rule only if it prevents a recurring class of errors.

## 3. Prefer skill composition over giant custom prompts

If an existing skill already handles:

- debugging;
- TDD;
- grilling;
- browser automation;
- security;
- frontend design;

route to it rather than reproducing its entire procedure in `AGENTS.md`.

## 4. Review skill selection periodically

Every few months, inspect:

```bash
npx skills list --global
```

Remove skills you never use if they create maintenance or discovery noise.

Use:

```bash
npx skills update
```

or a scoped/global update when you deliberately want newer skill versions.

## 5. Treat experimental skills as optional

Some useful skills are explicitly experimental.

For example, the current `taste-skill` v2 is marked experimental. Do not make an experimental skill a hard project dependency unless you accept that it may change.

## 6. Keep the project artifacts healthy

Periodically check:

```text
Is now.md still short?
Are completed tasks archived/closed?
Are ADRs durable decisions rather than temporary notes?
Is parking-lot full of stale ideas?
Are constraints still accurate?
```

If `now.md` becomes large, compress it. It is supposed to be a checkpoint, not a journal.

## 7. Upgrade the workflow carefully

When changing `AGENTS.md`, prefer:

```text
one rule
-> one project/session
-> observe behavior
-> keep or revert
```

Do not make ten workflow changes at once and then lose track of which one caused a regression.
