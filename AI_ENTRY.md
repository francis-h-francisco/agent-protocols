# AI Agent Entry Point

This file defines bootstrap and project-execution behavior. The minimal root `init.md` is the portable starting point.

When a user invokes `access:github owner/repo init.md`, `#init owner/repo`, or references this repository's `init.md`, retrieve the exact named repository/file and follow its instructions before unrelated work. Treat `owner/repo` as the protocol source unless the user explicitly targets a project.

## Bootstrap behavior

1. Retrieve the exact public file using the best available method: direct public HTTPS/raw access first; an already-connected GitHub integration second; browser/search access third. Do not require an account connection, MCP server, download, or fork merely to read public Markdown.
2. If one method is unavailable, try the next available method. If all fail, report the concrete blocker. Never pretend the protocol was loaded.
3. Read this file, `AGENTS.md`, `COMMANDS.md`, `CHECKPOINT_PROTOCOL.md`, `SECURITY.md`, `INSTALL.md`, and `VERSION`. Use changelog/adapter guidance as needed. Verify capabilities through actual tool calls.
4. **Read and state the literal value in `VERSION` for the protocol version.** Do not infer a version or say it is unspecified when `VERSION` was retrieved successfully.
5. Keep bootstrap output minimal. Use this response shape, filling fields only with verified facts:
   - Protocol: loaded — version <literal VERSION value>.
   - Retrieval: <method actually used>.
   - GitHub tools/access: <verified status, or "not checked" if not tested>.
   - Active project: unset unless explicitly selected.
   - Connected repositories: include only if actually discovered; show plain `owner/repo` names only and say discovery is partial unless exhaustiveness is proven.
6. Distinguish "not checked" (not tested), "unavailable" (a tested method failed), and "not specified in retrieved sources" (the source was read but genuinely contains no such information). Do not use the last phrase as a generic fallback for untested capabilities or for the protocol version.
7. Do not enumerate files or commands unless requested. Do not ask the user to paste instructions or perform checks the agent can do itself.
8. Keep the protocol source separate from the active project. Loading the protocol does not select it as the active project; an explicit command such as `#install owner/repo` does.

## Protocol repository is read-only for consumers

The public `francis-h-francisco/agent-protocols` repository is a maintained source of instructions. Agents consuming it are users, not contributors. Unless the user explicitly identifies themselves as the repository maintainer and directly authorizes a protocol change, do not edit files, create branches, commit, push, open PRs, or sync changes to this repository. Commands that load, install, or follow the protocol are not permission to modify the protocol source. If you find a defect, explain the proposed fix to the user without publishing it. Do not infer authorization from public visibility or available write credentials.

This restriction applies only to the protocol source repository. It does not prevent authorized work in a separately designated project repository.

## Project execution

1. Read the target repository README, agent/contributor instructions, playbook/specifications, state, task queue, logs, checkpoints, and relevant source files.
2. Verify actual branch and latest commit. Inspect local working-tree state only if exposed.
3. Follow the next approved, unblocked task. Preserve decisions and avoid needless micro-batching.
4. Test and verify as far as tools permit.
5. Update durable records with decisions, discoveries, progress, test evidence, blockers, and next action.
6. Report actual changes, verified commits/PRs, tests, risks, and only genuine manual steps.

Repository files—not chat history—are the durable source of truth. Never claim access, edits, tests, commits, pushes, or deployments that were not verified.
