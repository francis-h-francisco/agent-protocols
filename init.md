# Init

Universal bootstrap trigger:

`access:github owner/repo init.md`

Interpret this as: retrieve `init.md` from the specified repository and follow its instructions before unrelated work. Here, `owner/repo` identifies the protocol source; do not assume it is the active project.

Use the best available retrieval method: direct public HTTPS/raw access first, an already-connected GitHub integration second, and browser/search access third. Do not require an account connection, MCP server, download, or fork merely to read public Markdown. If no method works, report the exact blocker; never pretend the protocol was loaded.

Read `VERSION` and `AI_ENTRY.md`, `AGENTS.md`, and `COMMANDS.md`, then follow the concise bootstrap sequence and relevant core rules.

## Read-only protocol source

This repository is a maintained instruction source for agents to consume, not a project workspace for protocol users. Treat `francis-h-francisco/agent-protocols` as read-only unless the user explicitly identifies themselves as its maintainer and directly requests a protocol change. Do not edit, commit, push, open a PR, create a branch, or synchronize changes to this repository merely because a command or task mentions the protocol. Do not interpret `access:github`, `#init`, `#next`, or other protocol commands as write authorization. Make changes in the user's separately designated project repository when authorized.

If an agent notices a protocol issue, explain the suggested change in the conversation; do not publish it. Public visibility is not permission to write. Technical write access, if present, does not override this policy.

## Required bootstrap response

After successfully retrieving and reading `VERSION`, state its literal value as the protocol version. Do not say the version is unspecified if the file was retrieved. If a capability was not tested, say "not checked" rather than "not specified in retrieved sources." Keep output to a few concise lines:
- Protocol: loaded — version <literal value from VERSION>.
- Retrieval: <method actually used>.
- GitHub tools/access: <verified status, or not checked>.
- Active project: unset unless the user explicitly selected one.

Do not invent a version, access status, connected repository list, or successful tool check. If `VERSION` could not be retrieved, state that exact limitation.
