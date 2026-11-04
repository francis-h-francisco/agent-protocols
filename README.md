# Portable AI Project Continuity Protocol
Version: 1.4.2

A provider-independent, GitHub-first workflow for preserving project continuity across AI assistants, models, and fresh chats.

## Quick start

Use the short trigger with this repository:

`access:github francis-h-francisco/agent-protocols init.md`

If the agent does not understand the shorthand, ask it to open the root [init.md](init.md) or this public URL:
https://raw.githubusercontent.com/francis-h-francisco/agent-protocols/main/init.md

The bootstrap should quietly read required rules, verify only capabilities it actually has, and return a compact status. It must not dump the protocol, enumerate files, or list commands unless asked.

## Retrieval fallback

1. Fetch public HTTPS/raw content directly when supported.
2. Otherwise use an already-connected GitHub integration.
3. Otherwise use browser/search access to open the exact public file.
4. If none can retrieve it, state the specific limitation. Never claim it was loaded.

No MCP server, account connection, manual download, or fork is required merely to read public Markdown. Writing to a repository still requires authorization.

## Read-only source policy

This repository is a maintained instruction source. Agents consuming it are users, not contributors. They must not edit files, create branches, commit, push, open PRs, or synchronize changes to this repository unless the owner explicitly authorizes a specific maintenance task. Protocol commands are not write authorization. If an agent finds an issue, it should describe the proposed fix to the user without publishing it. This behavioral policy should be backed by repository permission and branch-protection settings.

## Workflow

- `#init owner/repo` — load the protocol and report concise status; do not select an active project.
- `#install owner/repo` — inspect the exact target and safely install/merge protocol guidance.
- `#next` — resume the next appropriate task from durable project state.

Commands are conventions, not platform magic. Agents must use real tools and distinguish verified results from assumptions.

## Project preflight and handoff records

Projects adopting this protocol should keep two separate locations:

- `.agent/PROJECT_PREFLIGHT.md` — project-specific pre-task instructions: required reading, scope, safety, approvals, and how to work.
- `docs/agent-handoff/` — durable work records: current state, active task, decisions, implementation/audit reports, independent reviews, and templates.

The root `AGENTS.md` should point agents to the preflight file. That preflight file tells agents to read the handoff records before starting or resuming work. The handoff directory records what happened; it is not a substitute for agent instructions.

Use the canonical templates in `templates/PROJECT_PREFLIGHT.md`, `templates/PROJECT_AGENTS_SECTION.md`, and `templates/agent-handoff/`. Customize project facts and constraints; never copy another project's private data or assumptions. Reports must distinguish SUBMITTED agent claims from independently verified and ACCEPTED outcomes.

## Core principle

Repository files—not chat history—are the durable source of truth. Inspect current project instructions and state before acting, make reviewable changes, test where feasible, and record outcomes truthfully.

## Repository contents

- `init.md`: minimal bootstrap pointer.
- `AI_ENTRY.md`: bootstrap and execution behavior.
- `AGENTS.md`: agent safety and working rules.
- `COMMANDS.md`: command semantics.
- `INSTALL.md`: safe installation and upgrades.
- `CHECKPOINT_PROTOCOL.md`: durable checkpoints and handoffs.
- `SECURITY.md`: privacy and safety rules.
- `templates/PROJECT_PREFLIGHT.md`: project preflight template to install as `.agent/PROJECT_PREFLIGHT.md`.
- `templates/PROJECT_AGENTS_SECTION.md`: snippet to integrate into a project's root `AGENTS.md`.
- `templates/agent-handoff/`: project state, active task, decisions, and report/review templates.
- `adapters/`: environment adaptation guidance.

## Important limits

Repository discovery may be partial. List connected repositories only as plain `owner/repo` identifiers, with no links, descriptions, visibility labels, or permission details. If discovery is not provably exhaustive, say briefly that the list is partial. Never claim access, edits, tests, pushes, or deployments unless verified.
