# AI Agent Entry Point

This file defines bootstrap and project-execution behavior. The minimal root `init.md` is the portable starting point.

When a user invokes `access:github owner/repo init.md`, `#init owner/repo`, or references this repository's `init.md`, retrieve the exact named repository/file and follow its instructions before unrelated work. Treat `owner/repo` as the protocol source unless the user explicitly targets a project.

## Bootstrap behavior

1. Retrieve the exact public file using the best available method: direct public HTTPS/raw access first; an already-connected GitHub integration second; browser/search access third. Do not require an account connection, MCP server, download, or fork merely to read public Markdown.
2. If one method is unavailable, try the next available method. If all fail, report the concrete blocker. Never pretend the protocol was loaded.
3. Read this file, `AGENTS.md`, `COMMANDS.md`, `CHECKPOINT_PROTOCOL.md`, `SECURITY.md`, `INSTALL.md`, `VERSION`, and relevant changelog/adapter guidance as needed. Verify capabilities through actual tool calls.
4. Keep bootstrap output minimal. Report only protocol version/load status, a brief retrieval capability status, active project (unset unless explicitly selected), and connected repository identifiers if discoverable as plain `owner/repo` names.
5. Repository discovery must use real tool results. Do not show links, descriptions, visibility labels, or permission levels in the bootstrap repository list. Do not claim the list is exhaustive unless the tool explicitly provides a complete listing.
6. Do not enumerate files or commands unless requested. Do not ask the user to paste instructions or perform checks the agent can do itself.
7. Keep the protocol source separate from the active project. Loading the protocol does not select it as the active project; an explicit command such as `#install owner/repo` does.

## Project execution

1. Read the target repository README, agent/contributor instructions, playbook/specifications, state, task queue, logs, checkpoints, and relevant source files.
2. Verify actual branch and latest commit. Inspect local working-tree state only if exposed.
3. Follow the next approved, unblocked task. Preserve decisions and avoid needless micro-batching.
4. Test and verify as far as tools permit.
5. Update durable records with decisions, discoveries, progress, test evidence, blockers, and next action.
6. Report actual changes, verified commits/PRs, tests, risks, and only genuine manual steps.

Repository files—not chat history—are the durable source of truth. Never claim access, edits, tests, commits, pushes, or deployments that were not verified.
