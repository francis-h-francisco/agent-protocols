# Agent Protocols

**A portable initialization, execution, and continuity protocol for GitHub-connected AI agents.**

Agent Protocols lets a compatible AI agent read a project's source of truth, follow a shared command contract, coordinate work through a persistent runtime, and preserve verified progress across sessions.

## Important prerequisite: use an AI agent with GitHub connection

For the intended workflow, the AI agent you use must support an **authenticated GitHub connection/integration**. It must be able to read this public protocol repository and access the project repository you authorize. Public web browsing or reading a raw Markdown URL alone is not enough for project operations.

The AI must also support a connection to the Agent Protocols Runtime through a supported authenticated MCP connection or API/tool adapter. Compatibility varies by AI product and account plan; verify the actual GitHub and connector capabilities before starting. A free chat subscription does not automatically include API access, cloud execution, or MCP support.

Connect GitHub using the AI product's official connection flow. Never paste GitHub tokens, API keys, or other secrets into chat.

## First-time setup

1. Connect GitHub to the AI agent you intend to use.
2. Select or authorize the project repository the AI should work on.
3. Send this instruction:

   `Read and follow the verified bootstrap contract at https://github.com/francis-h-francisco/agent-protocols/blob/main/BOOTSTRAP.md. Use your authenticated GitHub connection to verify the canonical repository, load the current protocol version and command rules, verify the selected project repository, and connect to the Agent Protocols Runtime through its supported authenticated MCP/API integration. Do not claim readiness unless each required capability is actually verified.`

4. Follow the agent's readiness report and resolve any missing GitHub, project, or runtime authorization.

If the AI cannot use an authenticated GitHub integration or supported runtime connection, it is not yet ready for the full Agent Protocols workflow. Do not treat public URL access as a substitute.

## Later sessions

Start with `#init`. This is shorthand for the complete verification and recovery process in [BOOTSTRAP.md](BOOTSTRAP.md), not merely fetching one file. The agent must re-read the current protocol and verify project/runtime state before continuing.

## Core commands

| Command | Purpose |
|---|---|
| `#init` | Full protocol, GitHub, project, and runtime bootstrap/recovery |
| `#project owner/repo` | Select and verify the exact project |
| `#status` | Report verified project/runtime/task state |
| `#next` | Continue the next authorized task, then test and checkpoint |
| `#pause` | Checkpoint and stop |
| `#handoff` | Write a complete durable continuation handoff to GitHub |

Commands are portable workflow triggers. They do not grant repository permissions, account access, or approval for consequential actions.

## How the team works

1. The connected AI is the user's protocol-aware entry point and can contribute work.
2. The runtime automatically selects an internal coordinator and specialists from the verified eligible free-agent pool. Manual agent selection is a future feature.
3. The coordinator understands the request, identifies system-side and user-side prerequisites, starts safe independent preflight work in parallel, and gives the user a clear checklist.
4. Work that does not depend on missing user input continues. Once blocking requirements are met, the coordinator starts implementation and proceeds through testing, review, fixes, and delivery.
5. Tasks and checkpoints persist in the cloud runtime. Work can continue when the original chat or coordinator is offline, subject to available free provider and runner capacity.
6. If quotas or providers become unavailable, the runtime uses another legitimately eligible free path where possible. Otherwise it waits durably and resumes when capacity returns.

The runtime is the authority for task state, permissions, dispatch, quotas, approvals, audit, checkpoints, and recovery. The internal coordinator is replaceable.

## Portal is optional

The normal user workflow is through the connected AI and authenticated runtime tools. A browser portal may be used as a fallback for authorization, recovery, approvals, or administration. A separate dashboard or duplicate AI chat UI is not required for the MVP.

## Source of truth and safety

- The public protocol repository is read-only for consumer agents. Its maintainer may authorize specific maintenance changes.
- Project source of truth lives in the user's selected GitHub repository and durable runtime records.
- Re-verify protocol, project, and runtime state at command boundaries and before consequential actions.
- Never invent access, test results, quota, agent availability, or completed work.
- Never commit secrets or paste credentials into chat.
- No paid fallback, quota evasion, or silent quality reduction.
- Human approval is required for consequential actions such as production deployment, destructive changes, protected-branch merges, billing/security changes, and external commitments.

## Protocol files

- [BOOTSTRAP.md](BOOTSTRAP.md) — complete first-run and recovery contract
- [init.md](init.md) — compact command bootstrap
- [AI_ENTRY.md](AI_ENTRY.md) — agent entry and execution rules
- [AGENTS.md](AGENTS.md) — safety and behavior rules
- [COMMANDS.md](COMMANDS.md) — command registry
- [CHECKPOINT_PROTOCOL.md](CHECKPOINT_PROTOCOL.md) — continuity and handoffs
- [SECURITY.md](SECURITY.md) — security requirements
- [INSTALL.md](INSTALL.md) — optional project installation

**Principle:** GitHub-backed project truth, verified runtime state, replaceable agents, and resumable execution.
