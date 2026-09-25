# Recommended Skills

This workflow does not require every available skill. It is designed around **selective activation**.

## Tier 1: Core skills

These are the most useful for the workflow itself.

| Skill | Why install it | Typical trigger |
|---|---|---|
| `grill-with-docs` | Codebase-aware requirement grilling and shared understanding | New/ambiguous feature |
| `wayfinder` | Multi-session planning for large or foggy work | Large/cross-cutting task |
| `tdd` | Behavior-first testing and tight implementation loops | Important behavior |
| `diagnosing-bugs` | Evidence-driven debugging loop | Hard bug/performance regression |
| `code-review` | Review implementation against standards/spec | After meaningful implementation |
| `handoff` | Bridge between large sessions/models | Context pressure / session boundary |
| `wait-what` | Re-explain a confusing prior answer | User does not understand |
| `improve-codebase-architecture` | Architecture-level cleanup and design review | Repeated structural friction |

Matt Pocock's current engineering skill collection includes these workflows and describes it as a composable set intended to work with different models.

### Install

The current installer supports global installation and individual skill selection. Use the space-separated `--skill <name>` form when selecting a skill.

```bash
npx skills@latest add mattpocock/skills --skill grill-with-docs --global
npx skills@latest add mattpocock/skills --skill wayfinder --global
npx skills@latest add mattpocock/skills --skill tdd --global
npx skills@latest add mattpocock/skills --skill diagnosing-bugs --global
npx skills@latest add mattpocock/skills --skill code-review --global
npx skills@latest add mattpocock/skills --skill handoff --global
npx skills@latest add mattpocock/skills --skill wait-what --global
npx skills@latest add mattpocock/skills --skill improve-codebase-architecture --global
```

If your environment already exposes the global skills under `%USERPROFILE%\.agents\skills\`, verify the resulting path after installation.

## Tier 2: Optional productivity/engineering skills

Install when your projects need them:

- `prototype` — explore a design/interaction question without committing to the final architecture.
- `research` — investigate questions against primary sources and capture cited findings.
- `implement` — structured implementation workflow after a clear spec/ticket set.

Matt's current engineering catalog distinguishes implementation, Wayfinder planning, prototype work, debugging, and research rather than treating them as one universal process.

## Tier 3: Frontend design

### Anthropic `frontend-design`

Use when creating or reshaping UI that should have deliberate visual identity instead of generic defaults.

Depending on how your skills CLI discovers the Anthropic repository, install the specific skill rather than blindly loading the entire repository.

A direct skill source can be used with the skills CLI when supported:

```bash
npx skills@latest add https://github.com/anthropics/skills --skill frontend-design --global
```

### Leonxlnx `taste-skill`

The current default install name is `design-taste-frontend` and v2 is experimental. It is specifically aimed at anti-slop frontend direction and uses variance/motion/density controls. Treat it as an optional experimental design layer rather than a universal requirement.

```bash
npx skills@latest add https://github.com/Leonxlnx/taste-skill --skill design-taste-frontend --global
```

For projects that need stable old behavior, the repository also preserves `design-taste-frontend-v1`.

### Microsoft `frontend-design-review`

Use after UI implementation when you need design-system, accessibility, responsive, theme, and UI quality review. The current skill explicitly supports design reviews and creative frontend work and is not intended for backend-only work.

```bash
npx skills@latest add microsoft/skills --skill frontend-design-review --global
```

## Tier 4: Browser testing

### Playwright CLI skill

For web projects, this is strongly recommended when browser behavior matters.

Install the CLI:

```bash
npm install -g @playwright/cli@latest
```

Install the skill into the vendor-neutral agent skills directory:

```bash
playwright-cli install --skills=agents -g
```

Playwright documents this exact `.agents/skills` global layout, and the skill covers browser automation, snapshots, tracing, storage state, test generation, and test execution.

## Tier 5: Security

### Anthropic Cybersecurity Skills

This is a very large library. The current repository reports 818 skills across many cybersecurity domains and explicitly supports GitHub Copilot among other agents.

Do **not** treat the entire library as a mandatory daily dependency.

Install targeted skills as needed.

For example, the repository currently contains:

```text
performing-web-application-penetration-test
performing-web-application-vulnerability-triage
configuring-oauth2-authorization-flow
```

The OAuth skill covers Authorization Code + PKCE, token lifecycle, scope design, state validation, redirect URI restrictions, and related controls. The web application pentest skill follows OWASP WSTG-style testing.

Install a specific skill rather than the whole security collection when possible:

```bash
npx skills@latest add mukul975/Anthropic-Cybersecurity-Skills --skill configuring-oauth2-authorization-flow --global
npx skills@latest add mukul975/Anthropic-Cybersecurity-Skills --skill performing-web-application-vulnerability-triage --global
```

For a full authorized web application security assessment, install/use the dedicated web application penetration-testing skill only when the project actually calls for it.

## Tier 6: Find more skills

The skills CLI can search the ecosystem:

```bash
npx skills find security
npx skills find typescript
npx skills find playwright
```

Use discovery when a task requires a specialized domain that is not already covered by your installed core skills.

## Recommended minimum set for this workflow

If you want the smallest useful starting point:

```text
mattpocock:
- grill-with-docs
- wayfinder
- diagnosing-bugs
- tdd
- code-review
- handoff
- wait-what

web projects:
- playwright-cli
- frontend-design-review

optional UI:
- design-taste-frontend
- frontend-design

security projects:
- install targeted Anthropic Cybersecurity skills only
```

## Update policy

Do not blindly update every skill in the middle of a project.

Prefer:

```text
finish/verify current work
-> update a skill
-> check for behavior changes
-> continue
```

The skills CLI supports scoped `skills update` operations.
