# Conversational Commands

Commands express workflow intent, not platform permissions. This file is the universal command registry. After `#init`, the agent should understand these commands for the rest of the current chat without repeated explanations.

## Session initialization and readiness

- `#init github.com/francis-h-francisco/agent-protocols` — **the standard first command, in any AI agent.** Open the repository, then follow `AI_ENTRY.md` steps 1–5. The steps: load the protocol, check or guide the runtime connection (`RUNTIME.md`), list accessible repositories, and report readiness. Does **not** select or install a project, create tasks, or execute work.
- `#init` — the same, for an agent that already knows the canonical source.
- `#init owner/repo` — use another repository as the protocol source, only when the user clearly intends that. Do not confuse it with project selection.
- `#help` — a short, friendly guide to what the user can do **now**, based on verified readiness:
  - Not connected: how to finish connecting.
  - Connected, no project: `#project owner/repo` with their actual repositories as examples.
  - Project selected: `#next`, `#status` and how to give the team a task in plain words.
  - The owner also sees the access commands.
  - Keep it under about 12 lines. Offer the full list only if asked.

## Project selection and setup

- `#project owner/repo` — verify and select the exact active project for this session. Does not install files.
- `#install owner/repo` — optional project-local setup: inspect existing guidance, then install/merge project-specific instructions/templates only when requested. Preserve existing content. Set the project active only after successful verification and installation.
- `#coor [owner/repo]` — inspect project instructions/state/open work/blockers and publish/update its coordination directive in the established location (or `.agent/coordination/CURRENT_DIRECTIVE.md` if genuinely needed). Default to a reviewable branch/PR. Does not execute the directive's application task.

## Access (runtime owner only)

- `#invite name [owner/repo ...]` — create a one-time invite link (`access_invite`) for a new person, optionally granting repositories. Give the link to the owner to send privately. The person's password appears only on that page.
- `#people` — list people, their repositories and open invites (`access_list`).
- `#grant name owner/repo ...` — set the repositories a person may use (`access_grant`).
- `#revoke name` — disable a person and sign them out everywhere (`access_revoke`).
- `#pause-all` / `#resume-all` — pause or resume all background work on the runtime (`dispatch_control`).
- `#providers` — list free providers, their data policy, capacity and capability scores (`agent_pool`). "Enable/disable <provider>" uses `provider_set`, after the owner confirms.
- `#paths owner/repo allow <prefixes> deny <prefixes>` — set where the team's file changes may go in that project (`project_settings`).

Never ask for, accept, display or store anyone's password in chat.

## Work and continuity

- `#start` — start/resume the selected project's next clearly authorized task after verifying current state.
- `#next` / `#proceed` — inspect durable task state and approvals, execute the next authorized task, test, checkpoint, update durable status, and report results/blockers.
- `#modify` — modify the selected project within the user's requested scope. Shared protocol changes require explicit maintainer authorization.
- `#pause` — checkpoint meaningful progress, record blockers and next action, then stop.
- `#append` — add newly supplied durable knowledge to the appropriate project record; do not invent facts.
- `#status [owner/repo]` — report verified protocol/GitHub/runtime/project/task/PR/CI/directive/blocker state. If no repository is supplied or active, report global readiness without guessing a project.
- `#sync-protocol owner/repo` — update protocol-managed files in the named project only when authorized. Never modify the canonical protocol source as a side effect.
- `#handoff` — write a complete durable continuation handoff to the designated runtime/project GitHub record and verify the write.
- `#export <task>` — the full record of one of your tasks (`task_export`), for backup or audit.
- `#notify <https-url | off>` — turn your task notifications on or off (`notify_set`), for example an ntfy.sh topic URL.

### Giving the runtime team work

After `#project owner/repo`, describe the outcome in plain words. The agent calls `task_create` with:
- a title, the outcome and acceptance criteria;
- `deliverable_format: "files"` for code or file changes (`"markdown"` for a document);
- `publish: true` to get a draft PR after approval;
- `context_paths` for existing files to change;
- `test_command` (owner only) to run the project's tests in a temporary Codespace and fix failures before review.

Follow progress with `#status` or `task_events`. Ask the user before every `approval_decide`.

## Routing rules

1. If not initialized, attempt canonical bootstrap automatically when tools are available. Continue the requested command if its meaning, target, and authorization are clear.
2. Use an explicit repository argument for that command; otherwise use the active project in this chat.
3. If a project is required but none is selected/supplied, ask one concise question. Never infer a project from account ownership or unrelated history.
4. Retrieve project instructions/state from GitHub when needed; do not require the user to paste accessible information.
5. Project-local preflight and handoff files are optional conventions; continue using verified existing project guidance when absent.
6. Commands do not override user restrictions, security rules, or approval boundaries.

## Coordinator directive lifecycle

The coordinator directive is a control-plane instruction, not a duplicate task queue. Keep task details and execution progress in the project's established task/handoff system. A directive should identify a unique ID, issue/update time (UTC), target repository, objective, next action, priority, acceptance criteria, constraints/approvals, references, and status.

The coordinator publishes the directive. The executing agent reads it at initialization/resume and before choosing the next task; it records the acknowledged directive ID in its normal task/checkpoint record when available. Do not let the agent overwrite coordinator-authored intent while acknowledging it. If it conflicts with explicit user instructions or safety policy, stop and ask.

`#coor` reports repository, directive summary, branch/PR or verified publication result, and blockers. It does not authorize external outreach, spending, deployment, destructive changes, or execution of the application task.

## Bootstrap response

Keep `#init` concise but truthful. Report the protocol version, runtime status (ready as `<name>`, or the exact pending step), accessible repositories (through the runtime's `repo_list` or the agent's own GitHub integration), and the active project or `not selected`. End with "Send `#help` to see what you can do." Do not dump the command catalog unless asked.

## Protocol source write restriction

The public `francis-h-francisco/agent-protocols` repository is read-only for consumer agents. No edit, branch, commit, push, PR, or sync is allowed unless the user explicitly identifies themselves as its maintainer and directly authorizes that specific protocol change. Command syntax does not grant permissions.

## Automatic team and background execution

The runtime automatically selects the internal coordinator and specialists from the verified eligible pool. The connected AI is the user's entry point and may contribute; it is not assumed to be the permanent coordinator. Background work is runtime-owned and must survive chat closure. Use legitimate free capacity only, preserve required quality, and wait/resume safely when all eligible capacity is exhausted.
