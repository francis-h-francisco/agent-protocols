# Current Coordinator Directive

> Optional project control-plane instruction. The coordinator owns this file. Executing agents acknowledge its ID in their normal task/checkpoint record; they do not rewrite coordinator intent merely to acknowledge it.

- Directive ID: UNKNOWN
- Status: NEW
- Issued at (UTC): YYYY-MM-DDTHH:MM:SSZ
- Updated at (UTC): YYYY-MM-DDTHH:MM:SSZ
- Target repository: owner/repo
- Project objective: UNKNOWN
- Priority: NORMAL

## Next action
Describe one clear next action. Keep implementation detail in the project's task record rather than duplicating its task queue.

## Acceptance criteria
- [ ] Criterion 1
- [ ] Criterion 2

## Constraints and approvals
- Explicit approvals required: UNKNOWN
- Safety, scope, and dependency constraints: UNKNOWN
- Do not infer permission for spending, external communication, deployment, production changes, or destructive actions.

## References
- Link relevant project instructions, task records, decisions, issues, or pull requests.

## Acknowledgement and progress
- Acknowledged by / session or agent: record in the project's normal checkpoint/task record.
- Execution status and evidence: record in the project's normal task/handoff system.
- Coordinator update required: yes/no, with reason.

## Lifecycle
Use status values such as NEW, ACKNOWLEDGED, IN_PROGRESS, COMPLETED, or BLOCKED. The coordinator updates the directive when priorities or instructions change. The executing agent reads it at initialization/resume and before selecting a task. If it conflicts with explicit user instructions or safety rules, stop and ask.
