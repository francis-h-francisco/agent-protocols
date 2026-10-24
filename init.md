# Init

Universal bootstrap trigger:

`access:github owner/repo init.md`

Interpret this as: retrieve `init.md` from the specified repository and follow its instructions before unrelated work. Here, `owner/repo` identifies the protocol source; do not assume it is the active project.

Use the best available retrieval method: direct public HTTPS/raw access first, an already-connected GitHub integration second, and browser/search access third. Do not require an account connection, MCP server, download, or fork merely to read public Markdown. If no method works, report the exact blocker; never pretend the protocol was loaded.

Read `AI_ENTRY.md`, `AGENTS.md`, `COMMANDS.md`, and `VERSION`, then follow the concise bootstrap sequence and relevant core rules. Verify actions with available tools, keep output minimal, and keep the protocol source separate from any active project.
