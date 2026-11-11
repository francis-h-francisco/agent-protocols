# Init

Universal session bootstrap:

`#init`

Canonical protocol source: `francis-h-francisco/agent-protocols`.

When the user sends `#init` without an argument, retrieve the canonical repository's current `init.md`, then read `VERSION`, `AI_ENTRY.md`, `AGENTS.md`, and `COMMANDS.md`. Follow the session bootstrap in `AI_ENTRY.md` before unrelated work. If the user supplies an explicit protocol source, use that source instead and verify it is intended.

Use the authenticated GitHub integration to verify access to the canonical protocol and enumerate the exact accessible `owner/repo` identifiers. Public HTTPS retrieval may load protocol text, but it does not prove authenticated GitHub project access. Verify the runtime connection status separately through its supported authenticated MCP/API path. Report any unavailable capability honestly.

## Session behavior

A successful initialization loads the universal command registry, operating rules, safety boundaries, and recovery procedure into the current chat's working context. Retain them throughout this conversation. A new chat is a new context: retrieve the latest protocol again.

`#init` does **not** select or install a project, change the active project, create a workspace, authorize runtime resources, create a task, or start execution. It reports the active project as the verified current project or `not selected`. Use `#project owner/repo` to select a project, `#install owner/repo` to optionally install/merge project-local instructions, and `#next` / `#proceed` to execute authorized work.

## Read-only protocol source

This repository is the maintained instruction source. Consumer agents must not edit, commit, push, open a PR, or synchronize changes here unless the user explicitly identifies themselves as its maintainer and directly authorizes a specific protocol maintenance task. A bootstrap or workflow command is not write authorization.

## Required bootstrap response

Keep the response concise but distinguish readiness layers:
- Protocol: loaded, with literal VERSION.
- GitHub: authenticated integration verified/not verified; exact accessible `owner/repo` identifiers.
- Runtime: authenticated/authorized, pending, or blocked; state what was actually tested.
- Active project: verified `owner/repo` or `not selected`.
- Next required onboarding action, if any.

Do not say the whole system is operationally ready merely because public Markdown loaded. Do not enumerate files or commands unless asked. Never invent a version, access status, active project, or successful tool check.
