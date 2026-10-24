# Installation and Upgrade Guide

## Command-driven workflow
- `#init owner/repo` loads the protocol, verifies retrieval/GitHub capabilities, and leaves the active project unset unless explicitly targeted.
- `#install owner/repo` selects the exact repository as active project, inspects state, and safely installs or merges protocol guidance.
- `#next` resumes the next appropriate task from the active project's task queue, playbook, and durable state.

Commands are conventions, not platform magic. Use real tools, verify results, and disclose unavailable capabilities.

## Retrieval
For public Markdown, use direct public HTTPS/raw retrieval first, an existing GitHub integration second, and browser/search third. Do not require an account connection, MCP server, download, or fork merely to read public Markdown. Repository writes require authorization.

## Before writing
1. Confirm intended repository and connected account.
2. Read README, agent/contributor guidance, playbook, state, task queue, and relevant source files.
3. Check default/current branch, latest commit, and uncommitted changes if exposed. Never claim local inspection if only remote state is available.
4. Classify files as protocol-managed, project-owned, or mixed. Never blindly replace mixed/project-owned files.

## First installation
1. Create a working branch when supported.
2. Add protocol instructions and missing templates. Merge compatible guidance into existing agent instructions.
3. Create project state files only if missing; initialize from evidence and label unknown values `UNKNOWN`.
4. Preserve project-specific instructions, source code, decisions, state, logs, and customizations.
5. Review changes for secrets, duplicated rules, and unrelated private content.
6. Run available checks, commit, and open a PR when supported.
7. Report exact branch, commit, PR, checks, and blockers.

## Upgrade
Compare installed version/changelog against desired release. Update only protocol-managed files or explicitly managed sections. Preserve project state, logs, and customizations. If safe merging is unclear, describe the conflict rather than overwriting.

## Public release safety
Before changing visibility, audit every current file and complete reachable history, including old versions, commit messages, metadata, branches, and tags. Current-file cleanup does not remove prior commits. History rewriting is destructive and requires explicit approval.

## Empty repositories
Use the existing default branch if one exists. Add the protocol in one logical commit when supported; otherwise use sequential file commits and disclose that choice. Verify final contents.
