# Installation and Upgrade Guide

## Command-driven workflow

- `#init owner/repo` loads the protocol and verifies retrieval/access.
- `#install owner/repo` inspects the exact target and safely installs or merges guidance.
- `#next` resumes the next appropriate task from durable project state.

Commands are conventions, not platform magic. Verify actual results.

## Retrieval and source policy

Read public Markdown through HTTPS/raw, an existing GitHub integration, or browser/search. Repository writes require authorization. Consumer agents must not modify `francis-h-francisco/agent-protocols` unless its maintainer explicitly authorizes a specific maintenance task.

## Before writing to a target project

1. Confirm the intended repository and account.
2. Read README, agent instructions, task queue, project state, and relevant source.
3. Verify branch, latest commit, and working-tree state if exposed.
4. Classify files as protocol-managed, project-owned, or mixed. Never blindly replace customized files.

## First installation

1. Create a working branch when supported.
2. Install `templates/PROJECT_PREFLIGHT.md` as `.agent/PROJECT_PREFLIGHT.md`; customize only with verified project facts.
3. Integrate `templates/PROJECT_AGENTS_SECTION.md` into root `AGENTS.md`, preserving existing rules.
4. Install the handoff templates into `docs/agent-handoff/` using this mapping:
   - `README.md`, `CURRENT_STATE.md`, `ACTIVE_TASK.md`, and `DECISIONS.md` go at the directory root.
   - `reports/IMPLEMENTATION_REPORT.md` goes to `templates/IMPLEMENTATION_REPORT.md`.
   - `reviews/REVIEW_REPORT.md` goes to `templates/REVIEW_REPORT.md`.
   - Create `reports/` and `reviews/` as destinations for task records.
5. Ensure root `AGENTS.md` points to `.agent/PROJECT_PREFLIGHT.md`, and the preflight points to `docs/agent-handoff/`.
6. Initialize unknown facts as `UNKNOWN`; never invent project state.
7. Preserve project-specific instructions, decisions, state, logs, and customizations.
8. Review for secrets and unrelated content; run available checks.
9. Commit and open a PR when supported. Report exact branch, commit, PR, checks, and blockers.

## Normal task workflow

1. Read root agent instructions and `.agent/PROJECT_PREFLIGHT.md`.
2. Read handoff README, current state, active task, decisions, and latest relevant report/review.
3. Verify live branch, commit, PR, and CI.
4. Write full task reports in `docs/agent-handoff/reports/` and independent reviews in `docs/agent-handoff/reviews/`.
5. Update current state and active task; link reports from PR descriptions.
6. In chat, provide concise links, status, blockers, and required owner decisions. Agent-authored reports are SUBMITTED or IN_REVIEW, never self-ACCEPTED.

## Upgrade

Compare installed version and changelog against the target release. Update only protocol-managed files or explicitly managed sections. Preserve project state, logs, and customizations. Describe conflicts rather than overwriting when safe merging is unclear.

## Public release safety

Before changing visibility, audit all current files and reachable history, including old versions, commit messages, metadata, branches, and tags. History rewriting is destructive and requires explicit approval.

## Empty repositories

Use the existing default branch. Prefer one logical commit when supported; otherwise disclose sequential commits. Verify final contents.