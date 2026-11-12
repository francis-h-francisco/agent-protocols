# Changelog

## 1.8.0
- RUNTIME.md describes how the team works:
  - plan, do the work, test in a temporary GitHub Codespace with automatic fixes, independent review, approval, draft PR;
  - immediate failover between free providers;
  - the task budget, member limits and the owner's path rules.
- GitHub access spans every GitHub account the owner connects to the runtime.
- New commands:
  - `#export` and `#notify`;
  - owner-only `#pause-all`, `#resume-all`, `#providers` and `#paths`;
  - guidance for giving the team work (files deliverables, context files, test command).
- Corrected the REST mirror path to `/api/v1/tools/<tool_name>`.

## 1.7.0
- The standard first command is `#init github.com/francis-h-francisco/agent-protocols`, which works in any AI agent. The README's first line sends agents to `AI_ENTRY.md`.
- `AI_ENTRY.md` is now an ordered, step-by-step checklist (breadcrumbs): load the protocol, check the runtime, guide the one-time connector setup, list repositories, and reply ending with `#help`.
- New `RUNTIME.md` holds the runtime's endpoint, connection steps per AI product, sign-in, and tools. Users never need to know the URL.
- Sign-in is a per-person access password, entered only in the runtime's sign-in window. Access is by owner invitation.
- The runtime is the GitHub bridge (`repo_list`, `repo_read`), so a separate GitHub integration is optional. `protocol_get` serves the protocol through the runtime.
- `#help` is defined as a short, readiness-aware guide.
- Added the owner access commands `#invite`, `#people`, `#grant` and `#revoke`.
- An unmerged 1.7.0 branch from earlier was superseded and is not this release.

## 1.6.0
- Added BOOTSTRAP.md as the authoritative first-run and session-recovery contract.
- Stated the prerequisite plainly: the primary AI must have an authenticated GitHub integration; public Markdown retrieval alone does not prove project access.
- Separated five readiness layers (protocol, GitHub, runtime, project, task) and required each to be reported truthfully.
- Kept #init as protocol/session bootstrap only: it verifies GitHub access, lists exact accessible owner/repo identifiers, and reports runtime status, but never selects or installs a project or starts work.
- Kept #project owner/repo (select), #install owner/repo (optional project-local setup) and #next/#proceed (execution) as distinct steps.
- Described the automatic-team and durable background execution contract of a connected runtime, applicable only after runtime readiness is verified.
- Reaffirmed no paid fallback, no quota evasion, and no silent quality reduction.

## 1.5.0
- Shifted the protocol to a session-first model: #init loads universal command definitions into the current chat context.
- Added canonical no-argument #init behavior and documented reinitialization in each fresh chat without assuming cross-chat memory.
- Added #project owner/repo for explicit active-project selection.
- Made project-local preflight and handoff folders optional rather than prerequisites for command recognition or ordinary protocol use.
- Added automatic command bootstrap, command routing, and context-recovery requirements.
- Added #coor for coordinator directive publication, distinct from #next/#proceed execution.
- Defined optional coordinator directive location and lifecycle; clarified it is not a duplicate task queue.
- Clarified that agents cannot poll while idle or guarantee detection of silent memory degradation.

## 1.4.2
- Standardized project-specific pre-task instructions at .agent/PROJECT_PREFLIGHT.md.
- Standardized durable project work records at docs/agent-handoff/, separate from agent instructions.
- Added canonical preflight, current-state, active-task, decisions, implementation-report, and independent-review templates.
- Updated agent bootstrap, installation, command, and checkpoint guidance to read and maintain the project preflight and handoff records.
- Clarified report states and that agent-authored submissions are not accepted until independently reviewed/authorized.

## 1.4.1
- Explicitly designate the protocol repository as a read-only instruction source for consumer agents.
- Clarify that bootstrap/workflow commands and public visibility do not grant write authorization.
- Prohibit consumer agents from editing, branching, committing, pushing, opening PRs, or syncing changes to the protocol source unless the maintainer explicitly authorizes a maintenance task.

## 1.4.0
- Provider-independent public Markdown retrieval with fallback across HTTPS/raw, existing GitHub integrations, and browser/search.
- Quiet bootstrap output by default; no unsolicited command catalog, file inventory, or protocol dump.
- Connected repository output limited to plain owner/repo identifiers and honest partial-discovery notes.
- Generalized examples and removed private project references from current documentation.
- Publication safety guidance requires current-file and full-history audits before visibility changes.

## 1.3.0
- Added access:github owner/repo init.md bootstrap trigger.
- Updated entrypoint, command reference, agent instructions, and quick start.
- Preserved direct GitHub file reference and #init owner/repo compatibility.

## 1.2.0
- Added root init.md provider-neutral bootstrap pointer.
- Documented exact GitHub file reference and retained #init owner/repo.

## 1.1.0
- Added #init owner/repo, verified-access guidance, project/source separation, and continuation commands.

## 1.0.0
- Initial provider-agnostic GitHub-first continuity protocol, command workflow, checkpoints, task ownership, handoffs, security rules, and templates.
