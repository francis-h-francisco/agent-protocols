# Installation and Upgrade Guide

## Session use (no project installation required)
1. In any compatible chat, send #init.
2. The agent retrieves the canonical protocol and loads the command registry into the current chat.
3. Use commands in that chat.
4. In a new chat, send #init again; do not assume another chat's working memory is available.
5. Select a project with #project owner/repo or supply it to a command.

## Optional project installation
Use #install owner/repo only when durable project-specific guidance or handoff records are useful. It may add or merge:
- .agent/PROJECT_PREFLIGHT.md — project-specific preflight.
- docs/agent-handoff/ — project state, tasks, decisions, reports, and reviews.
- A pointer to the canonical Agent Protocol and the project's GitHub Issue coordination convention.

Universal commands and task issues do not require a project-local directive file. Do not install a duplicate task queue or copy the universal command registry into each project.

## Before writing to a target project
1. Confirm exact repository and GitHub account.
2. Read README, agent instructions, current task issues/comments, task queue, project state, and relevant source.
3. Verify default branch, latest commit, open PRs, and CI.
4. Classify files as protocol-managed, project-owned, or mixed. Preserve project-specific state and customizations.

## Safe installation or upgrade
1. Create a working branch unless direct-to-default-branch publication is explicitly authorized.
2. Update only protocol-managed guidance; preserve project-specific instructions and state.
3. Review diffs for secrets and unrelated content.
4. Run available checks.
5. Commit and open a PR when appropriate.
6. Report exact branch, commit, PR, checks, and blockers.

## GitHub Issue coordination
A project adopting this protocol uses GitHub Issues as its canonical agent task inbox. Before creating tasks, inspect existing labels, issue templates, task records, and project conventions. Do not assume labels or automations exist. Add only the minimum issue template/labels needed and only with authorization. Issue comments are the durable asynchronous channel. Keep secrets and sensitive business data out of issues.

## Optional live messaging
See docs/LIVE_MESSAGING.md. A project may start with human notifications only and add agent-runtime adapters later. Do not describe a notification relay as an autonomous agent dispatcher unless it actually invokes a connected agent runtime and verifies the result.

## Upgrade
Compare installed version and release notes. Update only protocol-managed files or managed sections. Preserve project state, customizations, and task history. Describe conflicts rather than overwriting them.

## Public release safety
Before changing repository visibility, audit files and reachable history. History rewriting, permission changes, and destructive operations require explicit owner approval.
