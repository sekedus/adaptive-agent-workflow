# Adaptive Agent Workflow Wiki

This wiki is the operational manual for the **Adaptive Agent Workflow**.

It is written for a user who:

- primarily understands HTML, CSS, and JavaScript;
- uses AI agents heavily for other programming languages and frameworks;
- may use free or low-context models;
- may switch models, sessions, IDEs, harnesses, devices, or projects;
- prefers natural-language prompts instead of command-heavy prompts;
- needs durable project state so a new agent can resume without old chat history.

## Read this first

1. [Principles](00-principles.md)
2. [Installation and prerequisites](01-installation.md)
3. [Starting a project](02-project-setup.md)
4. [Daily usage](03-daily-usage.md)
5. [Intent routing](04-intent-routing.md)
6. [Grilling ideas with `/grill-with-docs`](05-grilling-and-requirements.md)
7. [Adaptive quality gates](06-quality-gates.md)
8. [Recovery and context limits](07-recovery-and-handoff.md)
9. [Project state files](08-project-state.md)
10. [Switching projects/devices](09-project-switching.md)
11. [Recommended skills](10-skills.md)
12. [Troubleshooting](11-troubleshooting.md)
13. [End-to-end examples](12-examples.md)
14. [Maintenance](13-maintenance.md)

## The mental model

```text
Natural-language request
        |
        v
Intent + size + risk assessment
        |
        +--> discuss / review
        |
        +--> grill / clarify
        |
        +--> plan
        |
        +--> build / fix
        |
        v
Selective quality gates
        |
        v
Verify + checkpoint
        |
        v
Repository becomes the durable memory
```

The workflow is deliberately **adaptive**. It is not a ritual where every request runs every phase or every skill.
