# Installation and Upgrade Guide

## Command-driven workflow

- `#init owner/repo` loads the protocol, verifies retrieval/GitHub capabilities, and leaves the active project unset unless explicitly targeted.
- `#install owner/repo` selects the exact repository as active project, inspects state, and safely installs or merges protocol guidance.
- `#next` resumes the next appropriate task from the active project's task queue, playbook, and durable state.

Commands are conventions, not platform magic. Use real tools, verify results, and disclose unavailable capabilities.

## Retrieval

For public Markdown, use direct public HTTPS/raw retrieval first, an existing GitHub integration second, and browser/search third. Do not require an account connection, MCP server, download, or fork merely to read public Markdown. Repository writes require authorization.

## Protocol source is read-only for consumers

Agents consuming `francis-h-francisco/agent-protocols` are users, not contributors. Do not edit, branch, commit, push, open PRs, or sync changes to this source repository unless its owner explicitly authorizes a specific maintenance task. This restriction does not prohibit authorized work in a separately designated project repository. If an agent notices a protocol issue, describe the proposed fix without publishing it.

## Before writing to a target project

1. Confirm intended repository and connected account.
2. Read README, agent/contributor guidance, playbook, state, task queue, and relevant source files.
3. Check default/current branch, latest commit, and uncommitted changes if exposed. Never claim local inspection if only remote state is available.
4. Classify files as protocol-managed, project-owned, or mixed. Never blindly replace mixed/project-owned files.

## First installation

1. Create a working branch when supported.
2. Add or merge protocol instructions and missing templates. Preserve project-specific instructions and existing customizations.
3. Install `templates/PROJECT_PREFLIGHT.md` as `.agent/PROJECT_PREFLIGHT.md`. Customize project identity, scope, repositories, approvals, and constraints using verified facts.
4. Create `docs/agent-handoff/` using `templates/agent-handoff/`: README, CURRENT_STATE, ACTIVE_TASK, DECISIONS, reports, reviews, and templates. Initialize unknown facts as `UNKNOWN`; do not invent project state.
5. Ensure root `AGENTS.md` points to `.agent/PROJECT_PREFLIGHT.md`; ensure the preflight points to `docs/agent-handoff/`.
6. Preserve project-specific instructions, source code, decisions, state, logs, and customizations.
7. Review changes for secrets, duplicated rules, and unrelated private content.
8. Run available checks, commit, and open a PR when supported.
9. Report exact branch, commit, PR, checks, and blockers.

## Normal task workflow

1. Read root agent instructions and `.agent/PROJECT_PREFLIGHT.md`.
2. Read `docs/agent-handoff/README.md`, `CURRENT_STATE.md`, `ACTIVE_TASK.md`, `DECISIONS.md`, and the latest relevant report/review.
3. Verify live repository, branch, commit, PR, and CI. Do not treat an old report as current state.
4. Work on the approved task and write a full report under `docs/agent-handoff/reports/`.
5. Record independent review under `docs/agent-handoff/reviews/`; update current state and active task; link reports in PR descriptions.
6. Return a concise chat handoff with the PR/report links, status, blocker, and owner decision. Never self-mark an agent report ACCEPTED.

## Upgrade

Compare installed version/changelog against desired release. Update only protocol-managed files or explicitly managed sections. Preserve project state, logs, and customizations. If safe merging is unclear, describe the conflict rather than overwriting.

## Public release safety

Before changing visibility, audit every current file and complete reachable history, including old versions, commit messages, metadata, branches, and tags. Current-file cleanup does not remove prior commits. History rewriting is destructive and requires explicit approval.

## Empty repositories

Use the existing default branch if one exists. Add the protocol in one logical commit when supported; otherwise use sequential file commits and disclose that choice. Verify final contents.
