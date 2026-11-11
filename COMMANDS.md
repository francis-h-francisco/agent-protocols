# Conversational Commands

Commands express workflow intent, not platform permissions. This file is the universal command registry. After `#init`, the agent should understand these commands for the rest of the current chat without repeated explanations.

## Session initialization and readiness

- `#init` — load/restore the canonical protocol in this chat; verify authenticated GitHub access; enumerate exact accessible `owner/repo` identifiers; inspect authenticated runtime connection status; report readiness layers. Does **not** select/install a project, change active project, create tasks, or execute work.
- `#init owner/repo` — backward-compatible explicit protocol-source form only when the user intends that repository to be the protocol source. Do not confuse it with project selection.
- `#help` — show command help when asked.

## Project selection and setup

- `#project owner/repo` — verify and select the exact active project for this session. Does not install files.
- `#install owner/repo` — optional project-local setup: inspect existing guidance, then install/merge project-specific instructions/templates only when requested. Preserve existing content. Set the project active only after successful verification and installation.
- `#coor [owner/repo]` — inspect project instructions/state/open work/blockers and publish/update its coordination directive in the established location (or `.agent/coordination/CURRENT_DIRECTIVE.md` if genuinely needed). Default to a reviewable branch/PR. Does not execute the directive's application task.

## Work and continuity

- `#start` — start/resume the selected project's next clearly authorized task after verifying current state.
- `#next` / `#proceed` — inspect durable task state and approvals, execute the next authorized task, test, checkpoint, update durable status, and report results/blockers.
- `#modify` — modify the selected project within the user's requested scope. Shared protocol changes require explicit maintainer authorization.
- `#pause` — checkpoint meaningful progress, record blockers and next action, then stop.
- `#append` — add newly supplied durable knowledge to the appropriate project record; do not invent facts.
- `#status [owner/repo]` — report verified protocol/GitHub/runtime/project/task/PR/CI/directive/blocker state. If no repository is supplied or active, report global readiness without guessing a project.
- `#sync-protocol owner/repo` — update protocol-managed files in the named project only when authorized. Never modify the canonical protocol source as a side effect.
- `#handoff` — write a complete durable continuation handoff to the designated runtime/project GitHub record and verify the write.

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

Keep `#init` concise but truthful. Report protocol/version, authenticated GitHub verification and exact accessible repository identifiers, runtime connection status, and active project or not selected. Do not dump the command catalog unless asked.

## Protocol source write restriction

The public `francis-h-francisco/agent-protocols` repository is read-only for consumer agents. No edit, branch, commit, push, PR, or sync is allowed unless the user explicitly identifies themselves as its maintainer and directly authorizes that specific protocol change. Command syntax does not grant permissions.

## Automatic team and background execution

The runtime automatically selects the internal coordinator and specialists from the verified eligible pool. The connected AI is the user's entry point and may contribute; it is not assumed to be the permanent coordinator. Background work is runtime-owned and must survive chat closure. Use legitimate free capacity only, preserve required quality, and wait/resume safely when all eligible capacity is exhausted.
