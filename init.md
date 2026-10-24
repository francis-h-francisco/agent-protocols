# Init

Universal bootstrap trigger:

`access:github owner/repo init.md`

Interpret this as: retrieve `init.md` from the specified repository and follow its instructions before unrelated work. Here, `owner/repo` identifies the protocol source; do not assume it is the active project.

Use the best available retrieval method: direct public HTTPS/raw access first, an already-connected GitHub integration second, and browser/search access third. Do not require an account connection, MCP server, download, or fork merely to read public Markdown. If no method works, report the exact blocker; never pretend the protocol was loaded.

Read `VERSION` and `AI_ENTRY.md`, `AGENTS.md`, and `COMMANDS.md`, then follow the concise bootstrap sequence and relevant core rules.

## Required bootstrap response

After successfully retrieving and reading `VERSION`, state its literal value as the protocol version. Do not say the version is unspecified if the file was retrieved. If a capability was not tested, say "not checked" rather than "not specified in retrieved sources." Keep output to a few concise lines:
- Protocol: loaded — version <literal value from VERSION>.
- Retrieval: <method actually used>.
- GitHub tools/access: <verified status, or not checked>.
- Active project: unset unless the user explicitly selected one.

Do not invent a version, access status, connected repository list, or successful tool check. If `VERSION` could not be retrieved, state that exact limitation.
