# Agent Protocols

**A portable protocol, project-onboarding, execution, and continuity layer for GitHub-connected AI agents.**

Agent Protocols gives compatible AI agents a shared command contract for loading protocol rules, verifying connected repositories and runtime access, selecting or installing project context, coordinating authorized work, and preserving progress across sessions.

## Important prerequisite: authenticated GitHub connection

The primary AI agent must support an authenticated GitHub connection/integration. It must be able to verify the canonical protocol and access the project repositories the user authorizes. Public web browsing or reading a raw Markdown URL alone does not prove project access.

The full workflow also requires a supported authenticated connection to the Agent Protocols Runtime through MCP or an API/tool adapter. Compatibility varies by AI product and account plan. A free chat subscription does not automatically include API access, cloud execution, or MCP support.

Connect GitHub using the AI product's official connection flow. Never paste tokens, API keys, passwords, or other secrets into chat.

## First-time setup

1. Connect GitHub to the AI agent using its official connection flow.
2. Send `#init`. The agent loads the current canonical protocol, verifies the authenticated GitHub integration, lists exact accessible `owner/repo` identifiers, and reports runtime connection status. **It must not select a project, install project files, or start a task.**
3. If runtime access is pending, complete the documented secure authorization/connector setup. The agent must verify identity, permissions, and capabilities before claiming runtime readiness.
4. Choose the project:
   - `#project owner/repo` selects and verifies a project for this session without installing files.
   - `#install owner/repo` optionally installs/merges project-local instructions/templates and selects the project after verification.
5. Use `#next` / `#proceed` to inspect durable task state and execute the next authorized task.

**Important:** `#init` alone does not complete project onboarding or start work. Protocol, GitHub, runtime, project, and task readiness are separate states. Follow the readiness report and resolve only the actual blockers.

## Later sessions

Start with `#init` to reload the canonical protocol and re-verify GitHub/runtime access. It does not silently restore or change the active project. Select the intended project with `#project owner/repo`, or use `#install owner/repo` if project-local setup is wanted, then use `#next` to resume work.

## Core commands

| Command | Purpose |
|---|---|
| `#init` | Load protocol; verify GitHub connection, accessible repositories, and runtime status |
| `#project owner/repo` | Select and verify the active project; no file installation |
| `#install owner/repo` | Optional project-local instruction/template installation and project selection |
| `#status` | Report verified protocol, GitHub, runtime, project, task, and blocker state |
| `#coor [owner/repo]` | Inspect and publish/update the project's coordination directive |
| `#next` / `#proceed` | Execute the next authorized task, then test and checkpoint |
| `#pause` | Checkpoint and stop |
| `#handoff` | Write and verify a durable continuation handoff |

Commands express workflow intent. They do not grant repository permissions or approval for consequential actions.

## How the team works

1. The connected AI is the user's protocol-aware entry point and may contribute work.
2. The runtime automatically selects an internal coordinator and specialists from the verified eligible free-agent pool. The user does not manually assemble the team.
3. The coordinator understands the request, identifies system-side and user-side prerequisites, starts safe independent preflight in parallel, and gives the user a concise checklist.
4. Unblocked work continues while missing user prerequisites are resolved. Implementation starts automatically once blockers are satisfied and authorization permits.
5. Tasks and checkpoints persist in the cloud runtime and can continue when the original chat or coordinator is offline, subject to eligible free provider/runner capacity.
6. When quotas or providers are unavailable, the runtime uses another legitimate free path where possible; otherwise it waits durably and resumes when capacity returns.

The runtime is authoritative for identity, permissions, task state, dispatch, quotas, approvals, audit, checkpoints, and recovery. Its internal coordinator is replaceable.

## Authorization surface

The normal interaction is through the user's connected AI and authenticated runtime tools. A minimal browser surface may be used for secure first-time authorization, recovery, approvals, or administration. It is not a duplicate AI chat UI.

## Source of truth and safety

- The public protocol repository is read-only for consumer agents; maintainer-authorized protocol maintenance is separate.
- Project truth lives in the selected project repository and durable runtime records.
- Re-verify protocol, project, and runtime state at command boundaries and before consequential actions.
- Never invent access, tests, quota, agent availability, or completed work.
- Never commit secrets or paste credentials into chat.
- No paid fallback, quota evasion, or silent quality reduction.
- Human approval is required for consequential actions such as production deployment, destructive changes, protected-branch merges, billing/security changes, and external commitments.

## Protocol files

- [BOOTSTRAP.md](BOOTSTRAP.md) — full bootstrap and operational onboarding contract
- [init.md](init.md) — compact session bootstrap entry point
- [AI_ENTRY.md](AI_ENTRY.md) — agent entry and execution rules
- [AGENTS.md](AGENTS.md) — safety and behavior rules
- [COMMANDS.md](COMMANDS.md) — command registry
- [CHECKPOINT_PROTOCOL.md](CHECKPOINT_PROTOCOL.md) — continuity and handoffs
- [SECURITY.md](SECURITY.md) — security requirements
- [INSTALL.md](INSTALL.md) — optional project installation

**Principle:** verified GitHub access, explicit project context, authenticated runtime operations, replaceable agents, and resumable execution.
