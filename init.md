# Init

Universal session bootstrap, in any AI agent:

`#init github.com/francis-h-francisco/agent-protocols`

(or `#init` in an agent that already knows the canonical source.)

Open `AI_ENTRY.md` and follow its steps 1–5 before unrelated work:
1. Load the protocol.
2. Check the runtime connection.
3. Guide the one-time connector setup if needed (`RUNTIME.md`).
4. List accessible repositories, through the runtime's `repo_list` or your own authenticated GitHub integration.
5. Report briefly, ending with "Send `#help` to see what you can do."

Report any unavailable capability honestly.

## Session behavior

A successful initialization loads the universal command registry, operating rules, safety boundaries, and recovery procedure into the current chat's working context. Retain them throughout this conversation. A new chat is a new context: retrieve the latest protocol again.

`#init` does **not** select or install a project, change the active project, create a workspace, authorize runtime resources, create a task, or start execution. It reports the active project as the verified current project or `not selected`. Use `#project owner/repo` to select a project, `#install owner/repo` to optionally install/merge project-local instructions, and `#next` / `#proceed` to execute authorized work.

## Read-only protocol source

This repository is the maintained instruction source. Consumer agents must not edit, commit, push, open a PR, or synchronize changes here unless the user explicitly identifies themselves as its maintainer and directly authorizes a specific protocol maintenance task. A bootstrap or workflow command is not write authorization.

## Required bootstrap response

Keep the response concise but distinguish readiness layers:
- Protocol: loaded, with literal VERSION.
- GitHub: repositories accessible through the runtime (`repo_list`) or the agent's own authenticated integration; exact `owner/repo` identifiers.
- Runtime: authenticated/authorized, pending, or blocked; state what was actually tested.
- Active project: verified `owner/repo` or `not selected`.
- Next required onboarding action, if any.

Do not say the whole system is operationally ready merely because public Markdown loaded. Do not enumerate files or commands unless asked. Never invent a version, access status, active project, or successful tool check.
