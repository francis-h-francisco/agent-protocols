# Conversational Commands

Commands express workflow intent, not platform permissions. This file is the universal command registry.

## Initialization and project selection
- `#init` — initialize or restore the current chat from the canonical protocol source.
- `#init owner/repo` — use an explicitly supplied protocol source; do not confuse this with project selection.
- `#project owner/repo` — verify and select the active project.
- `#help` — show command help when asked.

## Project commands
- `#install owner/repo` — optionally install project-specific preflight and continuity guidance.
- `#coor [owner/repo] [task/context]` — inspect the project, define one bounded assignment, and create its canonical GitHub Issue directly in the target repository.
- `#start` — resume this agent's existing claimed task after re-reading its issue, comments, project instructions, and current state. It does not automatically claim a new task.
- `#next` / `#proceed` — discover and claim one eligible task, then execute it.
- `#modify` — modify the selected project within the user's requested scope.
- `#pause` — checkpoint progress and post a factual update to the task issue/project record.
- `#append` — add supplied durable knowledge to the appropriate project record.
- `#status [owner/repo]` — report verified project, task, PR, CI, communication, and blocker status.
- `#sync-protocol owner/repo` — update protocol-managed files in the named project only when authorized.

## Routing rules
1. If not initialized, attempt canonical bootstrap when possible.
2. An explicit repository argument applies to that command; otherwise use the active project.
3. If the repository is unknown, ask; never infer from account ownership or unrelated chat history.
4. Commands retrieve instructions from GitHub; users should not need to paste accessible project instructions.
5. Project-specific preflight and handoff files are optional unless that project makes them mandatory.
6. Commands never override explicit user restrictions, security rules, or approval boundaries.

## #coor execution contract

### 1. Inspect
- Resolve the exact target repository.
- Read root instructions, project specifications, task/state/decision records, current coordinator tasks, open PRs, and relevant CI.
- Verify default branch and latest commit.
- Identify the next useful task, dependencies, risks, and expected role. Separate verified facts from inference.

### 2. Plan and bound
Create one unique stable task ID (for example `COOR-YYYYMMDD-01`) and one complete issue body containing:
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
- Apply task/priority/status labels only if they already exist and are appropriate. Do not silently create labels, milestones, projects, or workflows unless authorized.
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

