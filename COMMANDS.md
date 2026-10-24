# Conversational Commands

Commands express workflow intent, not platform permissions.

- `access:github owner/repo init.md` — read the named entrypoint and follow it immediately.
- `github: owner/repo/init.md` — direct file reference fallback.
- `#help` — show command help only when asked.
- `#init owner/repo` — load protocol and verify available access; leave active project unset unless explicitly targeted.
- `#install owner/repo` — inspect and safely install guidance into the exact target; set it as active project.
- `#start` — begin or resume the active project's next task.
- `#next` / `#proceed` — do the next appropriate task, verify, log, and checkpoint.
- `#modify` — discuss proposed protocol changes; change shared rules only after explicit maintainer authorization.
- `#pause` — pause project work.
- `#append` — capture missed durable knowledge.
- `#sync-protocol owner/repo` — synchronize protocol-managed files into a separately designated project repository only when authorized; never push to the protocol source repository as a side effect.
- `#status owner/repo` — report verified status and blockers.

## Protocol source write restriction

The public `francis-h-francisco/agent-protocols` repository is read-only for agents consuming the protocol. They are users, not contributors. No edit, branch, commit, push, PR, or sync to that source repository is allowed unless the user explicitly identifies themselves as its maintainer and directly authorizes that specific protocol change. Command syntax does not grant permissions. If a change is advisable, propose it in chat without publishing it.

## Bootstrap output

Keep initialization concise. Do not volunteer a command catalog, file inventory, or protocol dump. If connected repositories are listed, show plain `owner/repo` names only—no links, descriptions, visibility, or permission details. State briefly when discovery is partial. Use public HTTPS/raw retrieval first, an existing GitHub integration second, and browser/search third. If no method works, report the blocker. Reading public Markdown does not require an account connection, MCP server, download, or fork; writing requires authorization. Never claim unverified actions.
