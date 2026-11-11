> **AI agents: start here.** The user gave you this repository to initialize Agent Protocols. Before replying, open [`AI_ENTRY.md`](https://raw.githubusercontent.com/francis-h-francisco/agent-protocols/main/AI_ENTRY.md) and follow its steps in order.

# Agent Protocols

**A portable protocol, project-onboarding, execution, and continuity layer for GitHub-connected AI agents.**

Agent Protocols gives compatible AI agents a shared command contract for loading protocol rules, verifying connected repositories and runtime access, selecting or installing project context, coordinating authorized work, and preserving progress across sessions.

## Getting started

Send this to any AI agent:

```
#init github.com/francis-h-francisco/agent-protocols
```

The agent reads the protocol and checks whether it is connected to the Agent Protocols Runtime. The first time in each AI product, it walks you through adding the runtime as a connector; it supplies the address, so you have nothing to remember. A sign-in window then asks for your **access password**. Once it accepts, the window closes and returns to the chat.

Then send `#help`.

- **Access is by invitation.** The runtime owner sends you a one-time link that gives you your own password. Never type your password into a chat.
- **One connector is enough.** The runtime also gives the agent GitHub access to the repositories you may use, so a separate GitHub integration is optional.
- **Some AI products or plans** (often free tiers) cannot add custom connectors. The agent will say so.

## Later sessions

Start each new chat with `#init github.com/francis-h-francisco/agent-protocols` (or just `#init` in agents that already know it) to reload the protocol and re-check the runtime. It does not silently restore or change the active project. Select the intended project with `#project owner/repo`, or use `#install owner/repo` if project-local setup is wanted, then use `#next` to resume work.

## Core commands

| Command | Purpose |
|---|---|
| `#init github.com/francis-h-francisco/agent-protocols` | Load the protocol; connect or check the runtime; list your repositories |
| `#help` | What you can do now |
| `#project owner/repo` | Select and verify the active project; no file installation |
| `#install owner/repo` | Optional project-local instruction/template installation and project selection |
| `#status` | Report verified protocol, GitHub, runtime, project, task, and blocker state |
| `#coor [owner/repo]` | Inspect and publish/update the project's coordination directive |
| `#next` / `#proceed` | Execute the next authorized task, then test and checkpoint |
| `#pause` | Checkpoint and stop |
| `#handoff` | Write and verify a durable continuation handoff |

Commands express workflow intent. They do not grant repository permissions or approval for consequential actions.

## How the team works

This is the target behavior of a connected Agent Protocols Runtime. It applies only after runtime readiness has been verified; until then, agents must not claim automatic team selection, background execution, or quota failover.

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
- [RUNTIME.md](RUNTIME.md) — runtime address, connection steps per AI product, and tools
- [AI_ENTRY.md](AI_ENTRY.md) — agent entry and execution rules
- [AGENTS.md](AGENTS.md) — safety and behavior rules
- [COMMANDS.md](COMMANDS.md) — command registry
- [CHECKPOINT_PROTOCOL.md](CHECKPOINT_PROTOCOL.md) — continuity and handoffs
- [SECURITY.md](SECURITY.md) — security requirements
- [INSTALL.md](INSTALL.md) — optional project installation

**Principle:** verified GitHub access, explicit project context, authenticated runtime operations, replaceable agents, and resumable execution.
