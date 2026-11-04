# Portable AI Project Continuity Protocol
Version: 1.7.0

A provider-independent, GitHub-first protocol for command handling, project continuity, and human-directed multi-agent coordination across AI assistants, models, and standalone chats.

## Quick start
In any compatible chat, send:

`#init`

The agent retrieves this repository's current protocol and loads the universal command registry into the current chat. Use `#init` again in every new chat because working memory is not guaranteed to carry across chats.

Select a project with `#project owner/repo`, or provide a repository directly to a command.

## Core coordination model
GitHub Issues are the canonical task inbox and asynchronous communication record:
- `#coor` creates a complete task issue directly in the target repository, visible immediately on its default branch.
- `#start` resumes the agent's currently claimed task.
- `#next` discovers and claims the next eligible task.
- Issue comments hold acknowledgments, questions, progress, decisions, blockers, and handoffs.
- Pull requests hold proposed code changes and review.
- A task issue remains open until the coordinator or owner accepts the result.

This removes the unmerged-branch visibility problem for task instructions. A task issue is the single canonical assignment; do not create a duplicate directive branch/PR for ordinary assignments.

## Two communication layers
1. **Durable asynchronous coordination:** GitHub Issues, comments, labels, PRs, and project records. This remains the source of truth.
2. **Optional live messaging:** a transport adapter (for example Telegram) and an event relay can notify humans or connected agent runtimes about GitHub events and route short agent-to-agent messages. Every consequential message must link to and be recorded on its canonical GitHub issue.

A notification transport does not itself run an AI agent. Live agent-to-agent behavior requires each agent to have an active runner or an integration capable of receiving events, authenticating, invoking that agent, and posting its response. Ordinary chat sessions cannot be assumed to listen while idle.

See `docs/LIVE_MESSAGING.md` for the staged, $0-first design and security model.

## Project commands
- `#project owner/repo` — select the active repository for this chat.
- `#install owner/repo` — optionally install project-specific guidance and continuity records.
- `#coor [owner/repo] [task/context]` — inspect the project and create a bounded, ready-to-run GitHub task issue.
- `#start` — resume the task already claimed by this agent; if none, ask whether to claim the next eligible task or follow the project's explicit convention.
- `#next` / `#proceed` — discover and claim the next eligible task, then execute it.
- `#status` — report verified project and task status.

See `COMMANDS.md` for the complete registry.

## Task identity and visibility
Each task issue includes a stable task ID, target repository, base commit, owner-approved scope, expected role, dependencies, acceptance criteria, verification plan, and approval boundaries. The full task instructions are in the issue body and therefore visible to authorized repository collaborators without fetching an unmerged coordinator branch.

The first agent to claim a task posts a structured claim comment and verifies the latest issue state/comments before starting. GitHub issue comments and labels are not a transactional distributed lock; when concurrent claims conflict, stop and ask the coordinator to resolve ownership. Do not assume labels or automation exist—verify them first.

## Session-first design
- Universal command definitions live in this shared repository, not in every project.
- A successful `#init` loads command semantics and safety rules for the current chat session.
- A fresh chat retrieves the latest protocol again; cross-chat memory is not assumed.
- Agents cannot continuously poll while idle unless a separate runtime/event integration is deployed.

## Retrieval fallback
1. Fetch public HTTPS/raw content directly when supported.
2. Otherwise use an already-connected GitHub integration.
3. Otherwise use browser/search access to the exact public file.
4. If none can retrieve it, state the specific limitation. Never claim it was loaded.

## Read-only source policy
Agents consuming this repository are users, not contributors. They must not edit files, create branches, commit, push, open PRs, or synchronize changes here unless the owner explicitly authorizes a specific maintenance task.

## Core principle
GitHub records are durable project truth. Live messaging improves responsiveness but never replaces the canonical task record. Inspect current instructions and state before acting, make reviewable changes, test where feasible, and record outcomes truthfully.
