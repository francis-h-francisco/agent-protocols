# Portable AI Project Continuity Protocol
Version: 1.6.0

A provider-independent, GitHub-first protocol for consistent command handling, project continuity, and human-directed multi-agent coordination across AI assistants, models, and standalone chats.

## Quick start
In any compatible chat, send:

#init

The agent retrieves this repository's current protocol, loads the universal command registry into the current chat context, and returns a concise ready status. Use #init again in every new chat because working memory is not guaranteed to carry across chats.

Select a project with #project owner/repo, or provide a repository directly to a command. No project-local installation is needed for basic command use.

## Session-first design
- Universal command definitions live in this shared repository, not in every project.
- A successful #init loads command semantics and safety rules for the current chat session.
- The agent should not ask the user to repeat command definitions during that session.
- A fresh chat retrieves the latest protocol again; cross-chat memory is not assumed.
- If context is missing or uncertain, the agent re-fetches relevant protocol and project records before consequential action.
- The agent cannot continuously poll while idle and must not claim perfect detection of silent context degradation.

## Project commands
- #project owner/repo — select the active repository for this chat.
- #install owner/repo — optionally install project-specific guidance and durable continuity records.
- #coor [owner/repo] [task/context] — create and publish a bounded, agent-ready coordinator directive for the target project.
- #start — resume the next authorized task after reading the latest directive.
- #next / #proceed — execute the next approved task after checking the latest directive and project state.
- #status — report verified project and directive status.

See COMMANDS.md for the full command registry and #coor execution contract.

## Portable coordination
#coor is part of the universal protocol. It can be used with any accessible project repository; it is not tied to a Pivory repository, a particular agent provider, or project-local installation.

The coordinator inspects project instructions and current state, prepares a bounded directive, and publishes it using the project's existing convention or the portable fallback `.agent/coordination/CURRENT_DIRECTIVE.md`. Publication defaults to a reviewable branch and PR. The handoff must include the exact branch/ref, file path, and PR URL so another agent can retrieve the directive before it is merged.

The receiving agent reads the directive from the exact ref, verifies it against current project state, acknowledges its ID in its own task/checkpoint record, and creates a separate implementation branch from the latest default branch. It reports results in the project's established handoff system.

#coor prepares and publishes instructions; it does not automatically launch or notify another agent. Actual agent dispatch requires a separate platform integration and verified action.

## Optional project continuity files
Projects may adopt .agent/PROJECT_PREFLIGHT.md for project-specific instructions; .agent/coordination/CURRENT_DIRECTIVE.md for the latest coordinator directive; and docs/agent-handoff/ for durable state, active task, decisions, reports, and reviews.

These are optional. Their absence does not prevent an agent from initializing, recognizing commands, or working from existing repository documentation. Create them only when requested or when durable coordination/handoff genuinely requires them.

The coordinator directive is not a second task queue. It states the coordinator's current objective and next approved action; execution details remain in the project's established task records.

## Retrieval fallback
1. Fetch public HTTPS/raw content directly when supported.
2. Otherwise use an already-connected GitHub integration.
3. Otherwise use browser/search access to open the exact public file.
4. If none can retrieve it, state the specific limitation. Never claim it was loaded.

No MCP server, account connection, manual download, or fork is required merely to read public Markdown. Writing to a repository requires authorization.

## Read-only source policy
Agents consuming this repository are users, not contributors. They must not edit files, create branches, commit, push, open PRs, or synchronize changes here unless the owner explicitly authorizes a specific maintenance task. Protocol commands are not write authorization.

## Core principle
Repository files—not chat history—are the durable source of project truth. Session context makes commands convenient; GitHub records make work recoverable. Inspect current project instructions and state before acting, make reviewable changes, test where feasible, and record outcomes truthfully.

## Repository contents
- init.md: universal session bootstrap.
- AI_ENTRY.md: session initialization, routing, context recovery, and project execution.
- AGENTS.md: universal agent behavior and safety.
- COMMANDS.md: command registry and routing.
- INSTALL.md: optional project installation and upgrades.
- CHECKPOINT_PROTOCOL.md: durable checkpoints, coordination, and handoffs.
- SECURITY.md: privacy and safety rules.
- templates/: optional project instruction and continuity templates.
- adapters/: environment adaptation guidance.

Never claim access, edits, tests, pushes, or deployments unless verified.
