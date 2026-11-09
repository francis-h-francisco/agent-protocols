# Agent Protocols

**A portable command and continuity layer for AI-assisted projects.**

Agent Protocols gives compatible AI agents a shared way to initialize sessions, select repositories, follow project instructions, execute approved work, and preserve handoffs in GitHub.

It is designed to stay simple: one public protocol, a small command set, and each project's own repository as its source of truth.

## Quick start

In a compatible AI chat, send:

```text
#init
```

The agent retrieves the current protocol, loads its command and safety rules, verifies the version, and confirms readiness. Initialize again in a new chat; session context is not assumed to carry over.

Select a project:

```text
#project owner/repository
```

No project installation is required for ordinary use.

## Core commands

| Command | Purpose |
|---|---|
| `#init` | Load or restore the protocol for this chat |
| `#project owner/repo` | Select the active project |
| `#status` | Report verified project state |
| `#next` / `#proceed` | Continue the next authorized task |
| `#coor` | Publish or update the project coordination directive |
| `#install owner/repo` | Optionally add project-local guidance |
| `#pause` | Record progress, decisions, and the next action |
| `#help` | Show command guidance |

Commands describe workflow intent; they do not grant repository, account, deployment, or spending permissions.

## How it works

1. **Initialize** — retrieve the canonical protocol and load the command registry.
2. **Select** — identify the exact project repository; never guess the target.
3. **Inspect** — read project instructions, current state, and outstanding work.
4. **Act** — make focused, reviewable changes only within the user's authorization.
5. **Record** — verify outcomes and preserve decisions, progress, and handoffs in GitHub.

The protocol is session-first. GitHub project records provide durable continuity between chats. If context or repository state is uncertain, the agent must retrieve and verify it before consequential work.

## Project continuity

Projects can use their existing README, `AGENTS.md`, issues, task records, and handoff documentation. Optional templates in this repository provide conventions for preflight instructions, coordination directives, and durable handoffs. They are not prerequisites.

## Safety and boundaries

- The public protocol repository is read-only for agents using it. Protocol consumers must not change it unless its maintainer explicitly authorizes a specific maintenance task.
- Project changes require the user's authorization and the target repository's permissions.
- Agents must preserve existing project conventions and unrelated work.
- Report only access, edits, tests, and deployments that were actually verified.
- If required instructions or state cannot be retrieved, state the blocker instead of guessing.

## Protocol files

- `init.md` — minimal bootstrap entry point
- `AI_ENTRY.md` — initialization and execution flow
- `AGENTS.md` — behavior and safety rules
- `COMMANDS.md` — command registry
- `CHECKPOINT_PROTOCOL.md` — continuity and handoffs
- `SECURITY.md` — security requirements
- `INSTALL.md` — optional project installation
- `templates/` and `adapters/` — optional project and environment guidance

**The principle:** keep commands portable, project truth in GitHub, and every consequential action verifiable.
