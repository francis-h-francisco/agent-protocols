# Conversational Commands

Commands express workflow intent, not platform permissions. This file is the universal command registry. After #init, the agent should understand these commands for the rest of the current chat without repeated explanations.

## Initialization and project selection
- #init — initialize or restore the current chat session from the canonical protocol source. Load the command registry and rules into working context, verify retrieval, and respond ready. Does not select a project or install project files.
- #init owner/repo — backward-compatible explicit protocol-source form when the user intends that repository to be the protocol source. Do not confuse it with project selection.
- #project owner/repo — verify and select the active project for this session. Do not install files.
- #help — show command help when asked.

## Project commands
- #install owner/repo — optional installation/merge of project-local preflight and continuity templates into the exact target repository. Set it as the active project only after verification. This is not required to use the protocol or its commands.
- #coor [owner/repo] [task/context] — coordinate work for the explicit or active project. Verify project state, interpret the user's goal, produce a bounded agent-ready directive, and publish it to GitHub using the project's existing coordination convention or the portable fallback described below. Report the exact directive location/ref and handoff instructions. #coor does not execute the implementation task.
- #start — start or resume the selected project's next clearly authorized task after verifying its current state and latest coordinator directive.
- #next / #proceed — execute the next appropriate approved task. Read the latest coordinator directive, inspect task state, implement, verify, record, and report.
- #modify — modify the selected project within the user's requested scope. For shared protocol changes, require explicit maintainer authorization.
- #pause — checkpoint meaningful progress, record blockers and next action where project records exist, then stop execution.
- #append — add newly supplied durable knowledge to the appropriate project record; do not invent facts.
- #status [owner/repo] — report verified repository, task, PR, CI, directive, and blocker status. If no repository is supplied or active, ask which one.
- #sync-protocol owner/repo — update protocol-managed files in the named project only when authorized. Preserve project state and customizations. Never modify the protocol source as a side effect.

## Routing rules
1. If not initialized, attempt canonical bootstrap automatically when possible. Continue the requested command if its meaning, target, and authorization are clear.
2. Use an explicit repository argument for that command. Otherwise use the active project in this chat.
3. If a repository is required but unavailable, ask one concise question. Never infer the target from unrelated context or account ownership.
4. A command may retrieve project files as needed; it must not require the user to paste instructions already accessible through GitHub.
5. If a project lacks .agent/PROJECT_PREFLIGHT.md or docs/agent-handoff/, continue using verified repository guidance. These are optional conventions, not prerequisites.
6. Commands do not override the user's explicit restrictions, security rules, or approval boundaries.

## #coor execution contract

### 1. Resolve and inspect
- Resolve the target repository from the explicit argument or active project. If neither is established, ask which repository; do not guess.
- Read root instructions (AGENTS.md, README, contributing/security guidance), project specifications, current-state and task records, and any existing coordinator directive.
- Verify default branch, latest commit, open task/PR state, relevant CI, and known blockers as tools permit. Inspect the actual files relevant to the proposed task; do not rely only on old chat summaries.
- Identify repository boundaries and the appropriate agent role/capability. Do not assume a particular model/provider or claim that another agent was contacted.

### 2. Plan and bound
- Convert the user's goal into one actionable directive with a unique stable ID (for example COOR-YYYYMMDD-01).
- State the objective, one next action, priority, expected role, scope, out-of-scope items, dependencies, acceptance criteria, verification plan, source references, and known unknowns.
- Separate facts verified from inference and proposed decisions.
- State approvals explicitly. A #coor directive may authorize only work the user has authorized. It does not grant permission for spending, external outreach, deployment, production data changes, destructive actions, secret/permission changes, or merging unless the user separately approves them.
- If the goal is ambiguous in a way that materially changes the task, ask one concise question rather than inventing requirements.

### 3. Publish for the receiving agent
- Prefer the project's existing coordinator/task/handoff location and format when one is established. Do not create a competing task queue.
- Otherwise use `.agent/coordination/CURRENT_DIRECTIVE.md` based on `templates/CURRENT_DIRECTIVE.md`.
- The directive is a control-plane handoff, not a duplicate implementation plan or progress log. Keep detailed task progress in the project's established task/report records.
- Publish the directive to a reviewable branch and open a PR by default. Include the exact repository, branch, file path, PR URL, and base commit in the response. Do not claim the receiving agent can read an unmerged directive from the default branch: tell it to fetch the named branch/PR ref and read the exact file.
- If the project has an established direct-to-main convention or the user explicitly authorizes direct publication, verify that convention/authorization before writing. If GitHub write access is unavailable, provide the complete directive in chat and state that it was not published.
- Never place credentials, private customer/prospect data, or unnecessary personal information in a directive.

### 4. Receiving-agent handoff
The directive must tell the receiving agent to:
1. Initialize the canonical Agent Protocol with #init (or load the same source instructions if its interface cannot execute chat commands).
2. Read the directive from the exact branch/ref supplied by the coordinator, plus the project's current default-branch instructions and relevant task records.
3. Verify current branch/commit and check whether the directive is superseded, blocked, or already completed before acting.
4. Acknowledge the directive ID in its task/checkpoint record without editing the coordinator-authored directive merely to acknowledge it.
5. Create its own task branch from the current project default branch unless the directive explicitly specifies a safe alternative.
6. Execute only the assigned scope; stop and ask if the directive conflicts with owner instructions, current project state, or safety rules.
7. Report results in the project's established report location, with files changed, commit/PR, exact tests and outcomes, limitations, blockers, and next action. Agent-authored reports must not mark themselves ACCEPTED.

### 5. Report and maintain
- Report verified repository identity/default branch/latest commit, directive ID and status, assigned role, objective/next action, acceptance criteria, publication branch/path/PR, and blockers.
- A PR being opened is publication for review, not proof it was merged or that another agent received/read it.
- Do not claim cross-chat persistence, automatic agent dispatch, or a notification unless the platform/tool verifies it.
- #coor prepares and publishes coordination; #start/#next/#proceed perform the implementation task after authorization and fresh verification.

## Coordinator directive lifecycle
The coordinator directive is a control-plane instruction, not a duplicate task queue. Keep task details and execution progress in the project's existing task/handoff system. A directive should identify a unique ID, issued/updated time (UTC), target repository, objective, next action, priority, assigned role, scope, acceptance criteria, constraints/approvals, references, and status.

The coordinator authors/updates the directive. The executing agent reads it at initialization/resume and before selecting the next task; it records the acknowledged directive ID in its normal task/checkpoint record when available. Do not let the agent overwrite coordinator-authored intent while acknowledging it. If the directive conflicts with explicit user instructions or safety policy, stop and ask.

#coor reports the repository, directive summary, branch/PR or verified publication result, and blockers. It does not authorize external outreach, spending, deployment, destructive changes, merging, or execution of the application task.

## Bootstrap response
Keep #init concise: protocol ready/version, command registry loaded, verified retrieval/access status, active project or not selected, ready. Do not dump this command list unless asked.

## Protocol source write restriction
The public francis-h-francisco/agent-protocols repository is read-only for consumer agents. No edit, branch, commit, push, PR, or sync is allowed unless the user explicitly identifies themselves as its maintainer and directly authorizes that specific protocol change. Command syntax does not grant permissions.
