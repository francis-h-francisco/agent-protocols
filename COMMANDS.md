# Conversational Commands

Commands express workflow intent, not platform permissions. This file is the universal command registry. After #init, the agent should understand these commands for the rest of the current chat without repeated explanations.

## Initialization and project selection
- #init — initialize or restore the current chat session from the canonical protocol source. Load the command registry and rules into working context, verify retrieval, and respond ready. Does not select a project or install project files.
- #init owner/repo — backward-compatible explicit protocol-source form when the user intends that repository to be the protocol source. Do not confuse it with project selection.
- #project owner/repo — verify and select the active project for this session. Do not install files.
- #help — show command help when asked.

## Project commands
- #install owner/repo — optional installation/merge of project-local preflight and continuity templates into the exact target repository. Set it as the active project only after verification. This is not required to use the protocol or its commands.
- #coor [owner/repo] — central coordination. Identify the explicit or active project; if neither exists, ask which repository. Inspect current project instructions, state, open work, and blockers. Publish/update the coordinator directive in the project's established location, or use .agent/coordination/CURRENT_DIRECTIVE.md when durable coordination is needed and no convention exists. Default to a reviewable branch and PR. Do not implement the directive's application task merely because #coor was invoked.
- #start — start or resume the selected project's next clearly authorized task after verifying its current state.
- #next / #proceed — execute the next appropriate approved task. Read the latest coordinator directive when one exists, then inspect task state, implement, verify, record, and report.
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

## Coordinator directive lifecycle
The coordinator directive is a control-plane instruction, not a duplicate task queue. Keep task details and execution progress in the project's existing task/handoff system. A directive should identify a unique ID, issued/updated time (UTC), target repository, objective, next action, priority, acceptance criteria, constraints/approvals, references, and status.

The coordinator publishes the directive. The executing agent reads it at initialization/resume and before choosing the next task; it records the acknowledged directive ID in its normal task/checkpoint record when available. Do not let the agent overwrite coordinator-authored intent while acknowledging it. If the directive conflicts with explicit user instructions or safety policy, stop and ask.

#coor reports the repository, directive summary, branch/PR or verified publication result, and blockers. It does not authorize external outreach, spending, deployment, destructive changes, or execution of the application task.

## Bootstrap response
Keep #init concise: protocol ready/version, command registry loaded, verified retrieval/access status, active project or not selected, ready. Do not dump this command list unless asked.

## Protocol source write restriction
The public francis-h-francisco/agent-protocols repository is read-only for consumer agents. No edit, branch, commit, push, PR, or sync is allowed unless the user explicitly identifies themselves as its maintainer and directly authorizes that specific protocol change. Command syntax does not grant permissions.
