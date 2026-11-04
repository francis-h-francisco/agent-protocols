# Installation and Upgrade Guide

## Session use (no project installation required)
1. In any compatible standalone chat, send #init.
2. The agent retrieves the canonical protocol, loads the universal command registry into the current chat context, and reports readiness.
3. Use commands in that chat. The agent should not require repeated command explanations or reinitialization before each command.
4. In a new chat, send #init again. New chats cannot be assumed to inherit another chat's working memory.
5. Select a project with #project owner/repo or supply the repository directly to a command.

No project folder, ChatGPT Project, local preflight file, or per-agent command installation is required for basic protocol use.

## Optional project installation
Use #install owner/repo only when the project benefits from durable local instructions and handoff records. It may add or merge:
- .agent/PROJECT_PREFLIGHT.md — project-specific guidance;
- .agent/coordination/CURRENT_DIRECTIVE.md — coordinator control directive, when coordination is used;
- docs/agent-handoff/ — durable state, tasks, decisions, reports, and reviews.

These are optional project continuity conventions, not the source of universal command definitions. Preserve existing files and customizations.

## Retrieval and source policy
Read public Markdown through HTTPS/raw, an existing GitHub integration, or browser/search. Repository writes require authorization. Consumer agents must not modify francis-h-francisco/agent-protocols unless its maintainer explicitly authorizes a specific maintenance task.

## Before writing to a target project
1. Confirm the intended repository and account.
2. Read README, agent instructions, task queue, project state, and relevant source.
3. Verify branch, latest commit, and working-tree state if exposed.
4. Classify files as protocol-managed, project-owned, or mixed. Never blindly replace customized files.

## Safe installation or upgrade
1. Inspect repository and current branch/commit.
2. Create a working branch unless the user explicitly authorizes a direct push.
3. Merge only protocol-managed guidance; preserve project-specific instructions, decisions, state, logs, and customizations.
4. Initialize unknown project facts as UNKNOWN; never invent state.
5. Review diffs for secrets and unrelated content; run available checks.
6. Commit and open a PR when appropriate. Report exact branch, commit, PR, checks, and blockers.

## Normal task workflow
Retrieve project instructions and current state from GitHub when relevant. Read optional preflight/handoff files when present. Verify live branch, commit, PR, and CI. Test and record meaningful outcomes. Use existing project conventions; do not create folders solely to satisfy this protocol.

## Upgrade
Compare installed version and changelog against the target release. Update only protocol-managed files or explicitly managed sections. Preserve project state and customizations. Describe conflicts rather than overwriting when safe merging is unclear.

## Public release safety
Before changing visibility, audit all current files and reachable history, including old versions, commit messages, metadata, branches, and tags. History rewriting is destructive and requires explicit approval.
