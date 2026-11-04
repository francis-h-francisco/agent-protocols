# Checkpoints, Task IDs, Coordination, and Multi-Agent Work

## Session vs. repository continuity
The protocol command registry is loaded into the current chat by #init; it does not need to be copied into every project. A new chat should retrieve the protocol again. GitHub repository records remain the durable source of project truth.

Project continuity files are optional:
- .agent/PROJECT_PREFLIGHT.md — project-specific instructions.
- .agent/coordination/CURRENT_DIRECTIVE.md — latest coordinator directive.
- docs/agent-handoff/ — state, active task, decisions, reports, reviews, and templates.

Use existing project conventions when these files are absent. Do not create folders merely to make universal commands work.

## Coordinator directive
#coor is the coordination command; #next/#proceed are execution commands.

The coordinator directive is a control-plane instruction, not a duplicate task queue. It should contain:
- Unique directive ID and issued/updated timestamps (UTC).
- Target repository and project objective.
- Next action and priority.
- Acceptance criteria and constraints/approval requirements.
- Relevant source references.
- Status such as NEW, ACKNOWLEDGED, IN_PROGRESS, COMPLETED, or BLOCKED.

The coordinator authors/updates the directive. The executing agent reads it when initializing/resuming project work and before selecting the next task. It records the acknowledged directive ID in its normal checkpoint/task record when available; it must not overwrite coordinator-authored intent merely to acknowledge it. Task-level progress remains in the project's task/handoff system.

If the directive conflicts with explicit user instructions, repository authority, or safety rules, stop and ask. A directive does not authorize external outreach, spending, deployment, destructive changes, or other consequential actions that require separate approval.

## Task identity
Use stable IDs such as T-001. Record objective, owner/agent, status, branch, dependencies, acceptance criteria, files touched, tests, and blockers. Do not assign one task to multiple agents without an explicit collaboration plan.

## Suggested statuses
BACKLOG, READY, IN_PROGRESS, BLOCKED, REVIEW, DONE, CANCELLED.

## Checkpoint timing
Update after a meaningful implementation milestone, test result, decision, blocker, handoff, and before ending a long session. Re-verify context at command boundaries and before consequential actions. Keep checkpoints small and factual.

## Minimum checkpoint fields
- Timestamp (UTC preferred), repository, branch, commit SHA or UNCOMMITTED.
- Goal and milestone.
- Completed work and paths.
- Tests run and exact outcomes; tests not run and why.
- Decisions, risks, blockers, next action, acceptance criteria, task/agent ownership.
- Coordinator directive ID acknowledged, when applicable.

## Multiple agents or sessions
- Prefer one branch per task or agent.
- Inspect remote state before pushing; avoid force pushes.
- If a branch changed concurrently, inspect and reconcile instead of overwriting.
- Use PRs for reviewable integration. Treat the default branch as shared.
- Coordinate overlapping files and keep logs append-only where practical.
- Full reports belong in docs/agent-handoff/reports/; independent reviews belong in reviews/, when the project uses this convention.
- Use explicit report states: DRAFT, SUBMITTED, IN_REVIEW, ACCEPTED, REJECTED, SUPERSEDED. Agent-authored reports must not self-assign ACCEPTED.

## Handoff
A new chat/session should resume from repository files: read available project instructions, current state, active task, decisions, latest relevant report/review, and current coordinator directive when present; then verify actual branch and commit. Chat should contain a concise pointer, not the only copy of the report.
