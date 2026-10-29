# Adaptive Agent Workflow

<picture>![GitHub repo size](https://img.shields.io/github/repo-size/sekedus/adaptive-agent-workflow?label=Size)</picture>
[![GitHub License](https://img.shields.io/github/license/sekedus/adaptive-agent-workflow?label=License)](./LICENSE)
[![Badge DeepWiki]](https://deepwiki.com/sekedus/adaptive-agent-workflow)

**Template version: 0.8.2**

Adaptive Agent Workflow (AAW) is a reusable set of instructions and project records for working with AI coding agents. It helps the agent understand a project, keep work organized, verify changes, and recover after a session or model interruption.

<br>

## Designed for

AAW is designed first for **vibe coders** and **people who know the basics of HTML, CSS, and JavaScript** and use AI to help with the rest.

You can describe what you want in everyday language without remembering special workflow commands or managing a complicated development process yourself.

AAW is also designed for workflows that need:

- **Model, session, IDE, and device handoff:** switch AI models, chat sessions, coding tools (IDEs), or devices without losing project context.
- **Free or low-context models:** keep important project information in files instead of relying only on a long chat history.
- **Agent tools that support `AGENTS.md`:** for example, OpenCode Terminal and VS Code Copilot.
- **Selective use of skills and tools:** use what fits the task rather than running everything every time.
- **Bounded work with checkpoints and evidence:** keep tasks manageable and record what was actually checked.
- **Recovery after interruptions:** let a later session pick up the work from the project's saved state.

<br>

## Install & Upgrade

### Simple: Ask your agent

You do not need to learn special commands. Copy the relevant request below into your coding agent and let it inspect the project before changing files.

**Install AAW in a project that does not already use it:**

```text
Fetch Adaptive Agent Workflow (AAW) from https://github.com/sekedus/adaptive-agent-workflow. Read and follow the source repository's docs/workflow/aaw-installation.md for installing it into this project. Inspect the project first, preserve existing files and instructions, validate the installation, and stop before starting product work.
```

**Upgrade or migrate an existing AAW installation:**

```text
Upgrade the AAW already installed in this project to version 0.8.2. Fetch the matching source from https://github.com/sekedus/adaptive-agent-workflow and read its docs/workflow/aaw-migration.md. Preserve project-specific information and unrelated changes, verify the migration, and stop without doing product work.
```

Use the installation procedure for a new installation. If AAW is already installed, use the migration procedure—even when the upgrade looks small.

### Manual installation with a developer

<details>
<summary>Show the manual steps</summary>

<br>

1. Download or clone the AAW source repository from [GitHub](https://github.com/sekedus/adaptive-agent-workflow). Check `.aaw/manifest.yml` to identify the source version; do not assume a downloaded copy is the version you intended.
2. Decide whether the target project is new or already has AAW. An existing AAW installation must follow the migration procedure, not the fresh-install procedure.
3. Read [`docs/workflow/aaw-installation.md`](docs/workflow/aaw-installation.md) for a new installation, or [`docs/workflow/aaw-migration.md`](docs/workflow/aaw-migration.md) for an upgrade or repair.
4. Merge files carefully. Do not blindly replace existing project instructions, task records, documentation, license, changelog, or other project-specific files with template copies.
5. Verify the required files and project state before continuing. For a new project, do not create a product task just to represent installation.
6. Use the [human installation guide](wiki/01-installation.md) as a checklist if you are doing this manually. The detailed agent procedure is useful for understanding file conflicts and validation requirements.

The `wiki/` directory is optional documentation. The core workflow uses `AGENTS.md` and the installed `.aaw/` files; it does not require the wiki to run. For a human-oriented overview, see [the installation guide](wiki/01-installation.md).

</details>

<br>

## For agents

<details>
<summary>Instructions for agents installing or upgrading AAW</summary>

<br>

This repository is the AAW template source. The root `README.md` introduces the template to people; it is not a procedure to copy into a target project.

- **New installation:** read and follow [`docs/workflow/aaw-installation.md`](docs/workflow/aaw-installation.md).
- **Existing installation, upgrade, downgrade, migration, or repair:** read and follow [`docs/workflow/aaw-migration.md`](docs/workflow/aaw-migration.md).
- **Workflow rules after installation:** use the target project's root `AGENTS.md` as the canonical workflow instruction source. Harness-specific instruction files are thin adapters, not a second workflow definition.
- Inspect the target project and Git state before changing files. Merge instructions and workflow-owned state instead of overwriting them blindly.
- Preserve the target project's README and project-specific data. For a new project, create a README that describes the actual project; do not copy this template README, the template `CHANGELOG.md`, or the template `LICENSE` into the target project.
- Treat installation and migration as workflow maintenance, not product work. Verify the result and stop before starting or resuming an application task from the same request.
- Do not claim a version is current without checking the requested source version and its `.aaw/manifest.yml`.

</details>

<br>

## Quick guide: using AAW

### Describe the outcome you want

Use natural language. Explain what you want to change, why it matters, and what result would satisfy you. You do not need to type labels such as `MODE: BUILD`.

Examples:

- “Explain how login currently works. Do not change any files.”
- “Fix this bug and test the affected behavior.”
- “Help me plan this feature before you start coding.”
- “Continue the unfinished task from the project state.”

### Let the workflow match the work

Small, clear changes can use a lightweight process. Ambiguous, broad, user-visible, architectural, or security-sensitive work may need questions, a plan, or deeper review first. Asking for an explanation or review does not by itself authorize code changes.

### Know when a task is finished

The agent runs suitable automated checks when possible and reports what actually ran. If the change needs Human Development Testing (HDT)—for example, checking behavior in a real browser or runtime—the agent asks you to test the relevant behavior and report what happened.

After the required checks pass, **every task waits for your review** before it is closed. `HDT: NOT_REQUIRED` means no separate human test is needed; it does not mean the agent can silently close the task. Tell the agent whether you want related changes or whether it can close the task. A new session or silence is not approval. When it closes the task, AAW follows the commit policy; a Git commit is a named checkpoint that helps you review and recover changes.

### Park unrelated ideas

If you think of an unrelated feature while a task is unfinished, tell the agent. AAW records the idea in `.aaw/parking-lot.md` instead of silently expanding the current task. If the current task is ready to close, the agent closes it first, then starts a separate task for the new idea when you choose to proceed.

### Return after an interruption

You can switch models, IDEs, or devices, or return after days or weeks. AAW keeps a short current-state summary, task records, a roadmap, and verification notes in the repository so the agent can recover from the files instead of relying on old chat history.

<br>

## How AAW works

AAW is **recovery-first**: it treats interruptions as normal and keeps important work information in the project, not only in a conversation.

```text
Your request in everyday language
            |
            v
Understand intent, size, and risk
            |
            v
Choose the right depth of work
            |
            v
Track a bounded task; add a milestone only for larger coordinated work
            |
            v
Run relevant quality/security checks and automated tests
            |
            v
Human/runtime test only when the project needs it
            |
            v
Wait for your review before closing the task
            |
            v
Update project state and offer a Git commit checkpoint when the policy calls for it
```

### Task first, milestone only when needed

A task is a small, bounded piece of work. Several related changes can share one task when they have the same outcome and verification boundary. A milestone is for a genuinely broad outcome that needs several independently tracked tasks—usually three or more, or two when real dependencies or phases make coordination useful. A single task does not need a milestone.

### Three product-quality pillars

AAW chooses checks based on the change instead of running every tool on every task.

1. **Solve the problem — Useful & Usable.** Make sure the change addresses the real need and can be used as intended.
2. **Unique design — Desirable & Distinctive.** For user-facing experiences, avoid generic design and make deliberate choices that suit the product.
3. **Secure by design.** Consider relevant security risks early, rather than treating security as a final polish step.

### What makes AAW different

- **Natural-language interaction:** the agent routes ordinary requests without requiring users to remember workflow labels.
- **Persistent project state:** `.aaw/now.md`, task records, the roadmap, and verification notes help the next session recover its place.
- **Evidence before completion:** automated checks are run by the agent when possible, and claims are limited to the evidence available.
- **Human checks when needed:** tasks that require runtime or user observation stay active until the required test passes.
- **A review before closure:** completed verification is followed by a user-review checkpoint for every task.
- **Selective tools and skills:** the workflow chooses relevant quality/security checks. Optional third-party skills and personal customization are not bundled into this template and are not required for every task.
- **Portable instructions:** `AGENTS.md` is the canonical project workflow. `.github/copilot-instructions.md` is an optional thin adapter for VS Code Copilot, and other tools can use their supported instruction mechanism.
- **Safe workflow maintenance:** installing or migrating AAW is separate from product development. Migrations preserve project state and stop after verification.

<br>

## Documentation

Start with the [Wiki guide](wiki/README.md) for the full documentation index. The wiki is optional; it is not needed for the core workflow to run.

For a fuller workflow reference, see the [workflow overview](docs/workflow/adaptive-agent-workflow.md). For maintenance procedures, see [installation for agents](docs/workflow/aaw-installation.md) and [migration for agents](docs/workflow/aaw-migration.md). The template's release history is in [`CHANGELOG.md`](CHANGELOG.md).

<br>

## License

MIT – see [LICENSE](LICENSE).


<!-- Badges -->
[Badge DeepWiki]: https://img.shields.io/badge/Ask%20DeepWiki-blue.svg?labelColor=000000&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAACXBIWXMAAAPoAAAD6AG1e1JrAAACIUlEQVRYw+2XP2gUQRTGv7d3JhYWQawkIBaCVWzETos0gmAnVoKNTSoLK0E7EQQrC20sBVFBtLPQRgTBtBaKjYgIQUSxiJq7fT+LvCGPJZdNLt4dQj5Y3u7sznzfzLw/s9IO/icANiniCujEfWdsQgBLxAbsbraPZcmBfcAt4DNwKQsZNfEUsAB8YRV12LfA6ZHuedg7AO7ed/c+UBcbQhbiu+6wXIM6EnZWkszMJe2Ke0n6I2la0v51hFeSMLN6OwIK6jJwEBdUYb2MAxRSz6sY4geiahFgLe1Hwq6YWe3us8AN4FQQU4QM64SPY69Xyr43fADgNjAPXHb3peSsD4FDQ0VLEjAHvIhBPS6AHvA1bBO9JPAXcHFbIRtJ5yzwIQZ9CZwAusDJENIkLqsG8DpNyIZJwSUk9wLHgakcesC1JCCjiHm1kYDNOEjptCxpSVK/8f73OFLxPLAYM3oCzEX7MXf/lJbc/8kWpA4HgQdpYI9IWAbeh83whi84cHXL+58EPBoQhnmm94EzwE3gZ2p/Dhzdbhg+TaRr01x7ftb4/jBwFzjXrCvDpmLW9crVLNeR9CaapoGemb2TdCERW1tNaBNQ8jktwmozqwtpqRNtdWAjARYk39IS12ZWRX7vmJmA71nQZgi36gN7gCvAj5xc3P0jcH7kx7Ik5IC73wsh14GZsZySow5002l4Jr0b6+m4eSyvpAn8lEzsx2QHo8RfUrlN+uPq4ksAAAAASUVORK5CYII=
