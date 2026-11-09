# Agent Protocols

**A portable command and continuity layer for AI-assisted projects.**

Agent Protocols gives compatible AI agents a shared way to initialize sessions, select repositories, follow project instructions, execute approved work, and preserve handoffs in GitHub.

One public protocol. A small command set. Each project's own repository remains its source of truth.

## Quick start

### First-time setup

A fresh AI chat does not automatically know what `#init` means. Bootstrap the protocol first by sending:

```text
Read and follow https://raw.githubusercontent.com/francis-h-francisco/agent-protocols/main/init.md
```

If the agent cannot retrieve public URLs, open [init.md](init.md) and provide its contents to the agent.

### Later sessions

Once the agent has been configured with the protocol instructions, start a new session with:

```text
#init
```

This reloads the current protocol and command registry. If the agent does not retain the configured instructions between chats, repeat the first-time bootstrap prompt.

Select a project after initialization:

```text
#project owner/repository
```

Initialization does not select or install a project.

## Core commands

| Command | Purpose |
|---|---|
| `#init` | Load or restore the protocol in a configured agent |
| `#project owner/repo` | Select the active project for this session |
| `#status` | Report verified project state |
| `#next` / `#proceed` | Continue the next authorized task |
| `#coor` | Publish or update the project coordination directive |
| `#install owner/repo` | Optionally add project-local guidance |
| `#pause` | Record progress, decisions, blockers, and next action |
| `#help` | Show command guidance |

Commands describe workflow intent; they do not grant repository, account, deployment, or spending permissions.

## How it works

1. **Initialize** — retrieve the canonical protocol and load its command and safety rules.
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
