# Changelog

## 1.4.1
- Explicitly designate the protocol repository as a read-only instruction source for consumer agents.
- Clarify that bootstrap/workflow commands and public visibility do not grant write authorization.
- Prohibit consumer agents from editing, branching, committing, pushing, opening PRs, or syncing changes to the protocol source unless the maintainer explicitly authorizes a maintenance task.
- Clarify that authorized changes to a separately designated project repository remain permitted.

## 1.4.0
- Provider-independent public Markdown retrieval with fallback across HTTPS/raw, existing GitHub integrations, and browser/search.
- Quiet bootstrap output by default; no unsolicited command catalog, file inventory, or protocol dump.
- Connected repository output limited to plain `owner/repo` identifiers and honest partial-discovery notes.
- Generalized examples and removed private project references from current documentation.
- Publication safety guidance requires current-file and full-history audits before visibility changes.

## 1.3.0
- Added `access:github owner/repo init.md` bootstrap trigger.
- Updated entrypoint, command reference, agent instructions, and quick start.
- Preserved direct GitHub file reference and `#init owner/repo` compatibility.

## 1.2.0
- Added root `init.md` provider-neutral bootstrap pointer.
- Documented exact GitHub file reference and retained `#init owner/repo`.

## 1.1.0
- Added `#init owner/repo`, verified-access guidance, project/source separation, and continuation commands.

## 1.0.0
- Initial provider-agnostic GitHub-first continuity protocol, command workflow, checkpoints, task ownership, handoffs, security rules, and templates.
