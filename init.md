# Init

Universal session bootstrap:

`#init`

Canonical protocol source: `francis-h-francisco/agent-protocols`.

When the user sends `#init` without an argument, retrieve this repository's current `init.md`, then read `VERSION`, `AI_ENTRY.md`, `AGENTS.md`, and `COMMANDS.md`. Follow the session bootstrap in `AI_ENTRY.md` before unrelated work. If the user supplies an explicit protocol source, use that source instead and verify it is the intended protocol.

Use public HTTPS/raw access first, an already-connected GitHub integration second, and browser/search third. Do not require an account connection, MCP server, download, or fork merely to read public Markdown. If no method works, report the exact blocker; never pretend the protocol was loaded.

## Session behavior

A successful initialization loads the universal command registry and operating rules into the current chat's working context. Retain and use them throughout this conversation; do not make the user repeat command definitions during the same session. A new chat is a new context: `#init` retrieves the latest protocol again. Never claim that chat memory persists across separate chats unless the platform explicitly verifies that capability.

Initialization does not require installing project instructions, creating project folders, or selecting a project. Project-specific instructions are retrieved from GitHub only when a command needs them.

## Read-only protocol source

This repository is the maintained instruction source. Consumer agents must not edit, commit, push, open a PR, or synchronize changes here unless the user explicitly identifies themselves as its maintainer and directly authorizes a specific protocol maintenance task. A bootstrap or workflow command is not write authorization. Technical write access and public visibility do not override this rule.

## Required bootstrap response

After successful retrieval, return a concise readiness response:
- Agent Protocol ready — version <literal value from VERSION>.
- Session command registry: loaded.
- Retrieval/access: <verified method and capability status>.
- Active project: <verified owner/repo or not selected>.
- Ready.

Do not enumerate files or commands unless asked. Do not invent a version, access status, active project, or successful tool check. If a capability was not tested, say "not checked". If retrieval failed, report the blocker and do not claim readiness.


## Verified bootstrap contract (current)

For first-time setup and session recovery, follow BOOTSTRAP.md completely. A bare #init is shorthand for that full procedure, not permission to claim readiness after merely reading public Markdown. Verify the authenticated GitHub integration, canonical repository/version, explicitly selected project repository, and authenticated Agent Protocols Runtime MCP/API connection. Re-verify source-of-truth state at command boundaries and before consequential actions. If any capability is unavailable, report the exact blocker and do not claim it was verified.
