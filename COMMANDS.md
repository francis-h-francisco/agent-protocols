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
- `#coor [owner/repo] [task/context]` — inspect the project, define one bounded assignment, and create its canonical GitHub Issue directly in the target repository.

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

- `#start` — resume this agent's existing claimed task after re-reading its issue, comments, project instructions, and current state. It does not automatically claim a new task.
- `#next` / `#proceed` — discover and claim one eligible task, then execute it.
- `#modify` — modify the selected project within the user's requested scope. Shared protocol changes require explicit maintainer authorization.
- `#pause` — checkpoint meaningful progress, record blockers and next action, then stop.
- `#append` — add newly supplied durable knowledge to the appropriate project record; do not invent facts.
- `#status [owner/repo]` — report verified protocol/GitHub/runtime/project/task/PR/CI/directive/blocker state. If no repository is supplied or active, report global readiness without guessing a project.
- `#sync-protocol owner/repo` — update protocol-managed files in the named project only when authorized. Never modify the canonical protocol source as a side effect.
- `#handoff` — write a complete durable continuation handoff to the designated runtime/project GitHub record and verify the write.
- `#export <task>` — the full record of one of your tasks (`task_export`), for backup or audit.
- `#notify <https-url | off>` — turn your task notifications on or off (`notify_set`), for example an ntfy.sh topic URL.

### Giving the runtime team work

After `#project owner/repo`, describe the outcome in plain words.

**Estimate first (runtime 0.11.0 and later).** Before creating the task, the agent calls `task_estimate` with the same fields. It then shows the user, in two or three lines:
- the **tier** and its reasons;
- the expected model calls;
- the options.

| Tier | Meaning | What the agent does |
|---|---|---|
| **T0 Free** | Routine: documents, summaries, small bounded fixes. | Create the task. |
| **T1 Free + verify** | Code changes with a test command. | Create the task; tests run and failures are fixed automatically. |
| **T2 Boost suggested** | Security-sensitive, cross-module or large changes, or a project where recent tasks failed. | Say that free models may struggle. Offer: run it free anyway, split it into smaller tasks, or have the Lead (this AI app) do the hard part. A paid boost is not available yet. |
| **T3 Lead-led** | Open decisions, architecture, or code changes with no acceptance criteria. | Settle the questions with the user first, then estimate again. |

The user chooses. Never upgrade or spend silently. Free is always a complete option.

Then the agent calls `task_create` with:
- a title, the outcome and acceptance criteria;
- `deliverable_format: "files"` for code or file changes (`"markdown"` for a document);
- `publish: true` to get a draft PR after approval;
- `context_paths` for existing files to change;
- `test_command` (owner only) to run the project's tests in a temporary Codespace and fix failures before review;
- `max_model_calls` set to the estimate's `suggested_max_model_calls` when it is above the default.

Follow progress with `#status` or `task_events`. Ask the user before every `approval_decide`.

## Routing rules

1. If not initialized, attempt canonical bootstrap automatically when tools are available. Continue the requested command if its meaning, target, and authorization are clear.
2. Use an explicit repository argument for that command; otherwise use the active project in this chat.
3. If a project is required but none is selected/supplied, ask one concise question. Never infer a project from account ownership or unrelated history.
4. Retrieve project instructions/state from GitHub when needed; do not require the user to paste accessible information.
5. Project-local preflight and handoff files are optional conventions; continue using verified existing project guidance when absent.
6. Commands do not override user restrictions, security rules, or approval boundaries.

## #coor execution contract

### 1. Inspect
- Resolve the exact target repository.
- Read root instructions, project specifications, task/state/decision records, current coordinator tasks, open PRs, and relevant CI.
- Verify default branch and latest commit.
- Identify the next useful task, dependencies, risks, and expected role. Separate verified facts from inference.

### 2. Plan and bound
Use [the portable assignment template](templates/AGENT_TASK_ISSUE.md). Create one unique stable task ID (for example `COOR-YYYYMMDD-01`) and one complete issue body containing:
- status, priority, expected receiving role, objective, and one next action;
- target repository, default branch, base commit, relevant paths and evidence refs;
- in-scope and out-of-scope work;
- dependencies and existing task/PR relationships;
- observable acceptance criteria and verification plan;
- explicit approvals, exclusions, security/privacy/cost constraints;
- required reading and receiving-agent procedure.

Do not create duplicate task issues for the same assignment. Search existing open issues and project task records first. Do not include secrets or unnecessary personal/prospect data.

### 3. Publish the canonical task
- Create the GitHub Issue directly in the target repository so authorized collaborators can read it immediately without a coordinator branch or PR.
- Use a clear title with the task ID and concise objective.
- Reserve the runtime intake label `agent-task` for an explicitly requested runtime submission (see [runtime intake](RUNTIME.md)). Keep runtime-owned tasks out of manual claim discovery. Apply other task/priority/status labels only if they already exist and are appropriate. Do not silently create labels, milestones, projects, or workflows unless authorized.
- Verify the created issue URL, number, body, and state by reading it back.
- The issue body is coordinator-authored assignment intent. Progress, questions, decisions, acknowledgments, and handoffs are appended as comments.
- If issue creation is unavailable, provide the complete directive in chat and state NOT PUBLISHED. Never imply an agent can see chat-only instructions.

### 4. Receiving-agent handoff
The receiving agent must:
1. Load the canonical protocol using #init or retrieve its public source.
2. Read the complete task issue and all relevant comments from the target repository.
3. Read current project instructions, task/state records, and relevant source.
4. Verify the task is current, not superseded/completed/cancelled, dependencies are satisfied, and authorization is adequate.
5. Claim/acknowledge the task with agent identity, role, UTC timestamp, and intended implementation branch; re-fetch comments to detect conflicting claims.
6. Create a separate implementation branch from the latest default branch.
7. Execute only the approved scope and stop on conflicts or missing approvals.
8. Post meaningful progress, blockers, questions, decisions, PR link, exact tests/results, limitations, and next action as issue comments and project records.
9. Mark its report SUBMITTED or IN_REVIEW; never self-mark ACCEPTED.

### 5. Claim and concurrency rules
- Search for an existing valid claim before taking a task.
- Use a stable agent identity string, task ID, UTC timestamp, and intended branch in claim comments.
- A claim is advisory in the GitHub-only baseline. Re-fetch the issue and comments after claiming.
- If claims conflict, ownership is unclear, or another agent has an active claim, stop and ask the coordinator to resolve it.
- Do not assume GitHub labels/comments provide atomic locking. A strict single-owner lease requires a serialized dispatcher or atomic lease service.
- Do not claim multiple tasks concurrently unless the coordinator explicitly authorizes parallel work and scopes do not overlap.

### 6. Completion and acceptance
- Implementer posts a completion summary and opens/links a PR.
- Independent reviewer checks acceptance criteria, code, tests, and evidence; records ACCEPTED or REJECTED recommendation.
- Only coordinator/owner records final acceptance and closes the issue.
- Keep issue open while in review or blocked. A PR merge is not by itself proof of task acceptance unless project policy says so.

## Asynchronous and live communication
- GitHub Issue comments are the durable asynchronous communication record.
- Optional live transport may notify or route short messages, but it must link back to the canonical issue and record consequential decisions there.
- No command may claim a notification, live delivery, or agent dispatch unless a connected integration confirms it.
- An idle chat session cannot be assumed to receive events. Live execution requires an active agent runner or event-capable platform integration.

## Coordinator authority and safety
#coor creates and publishes an assignment; it does not itself execute the implementation task. It cannot authorize spending, external outreach, deployment, production data changes, destructive actions, secret/permission changes, or merge unless the owner explicitly approves them.


## Bootstrap response

Keep `#init` concise but truthful. Report the protocol version, runtime status (ready as `<name>`, or the exact pending step), accessible repositories (through the runtime's `repo_list` or the agent's own GitHub integration), and the active project or `not selected`. End with "Send `#help` to see what you can do." Do not dump the command catalog unless asked.

## Protocol source write restriction

The public `francis-h-francisco/agent-protocols` repository is read-only for consumer agents. No edit, branch, commit, push, PR, or sync is allowed unless the user explicitly identifies themselves as its maintainer and directly authorizes that specific protocol change. Command syntax does not grant permissions.

## Automatic team and background execution

The runtime automatically selects the internal coordinator and specialists from the verified eligible pool. The connected AI is the user's entry point and may contribute; it is not assumed to be the permanent coordinator. Background work is runtime-owned and must survive chat closure. Use legitimate free capacity only, preserve required quality, and wait/resume safely when all eligible capacity is exhausted.
