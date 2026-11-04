# Checkpoints, Task IDs, and Multi-Agent Work

## Project preflight and durable records

For projects adopting this protocol, keep instructions separate from work records:
- `.agent/PROJECT_PREFLIGHT.md` — project-specific pre-task reading, scope, constraints, approval boundaries, and workflow.
- `docs/agent-handoff/` — current state, active task, decisions, reports, reviews, and templates.

The root `AGENTS.md` should point to the preflight file. The preflight file should direct agents to the handoff records. Before resuming, read `CURRENT_STATE.md`, `ACTIVE_TASK.md`, `DECISIONS.md`, and the latest relevant report/review, then verify live repository state. Use the canonical templates in this protocol when installing the convention.

## Task identity

Use stable IDs such as `T-001`. Record objective, owner/agent, status, branch, dependencies, acceptance criteria, files touched, tests, and blockers. Do not assign one task to multiple agents without an explicit collaboration plan.

## Suggested statuses

`BACKLOG`, `READY`, `IN_PROGRESS`, `BLOCKED`, `REVIEW`, `DONE`, `CANCELLED`.

## Checkpoint timing

Update after a meaningful implementation milestone, test result, decision, blocker, handoff, and before ending a long session. Keep checkpoints small and factual.

## Minimum checkpoint fields

- Timestamp (UTC preferred), repository, branch, commit SHA or `UNCOMMITTED`.
- Goal and milestone.
- Completed work and paths.
- Tests run and exact outcomes; tests not run and why.
- Decisions, risks, blockers, next action, acceptance criteria, task/agent ownership.

## Multiple agents or sessions

- Prefer one branch per task or agent.
- Inspect remote state before pushing; avoid force pushes.
- If a branch changed concurrently, inspect and reconcile instead of overwriting.
- Use PRs for reviewable integration. Treat the default branch as shared.
- Coordinate overlapping files and keep logs append-only where practical.
- Full reports belong in `docs/agent-handoff/reports/`; independent reviews belong in `reviews/`. Link them in PR descriptions.
- Use explicit report states: DRAFT, SUBMITTED, IN_REVIEW, ACCEPTED, REJECTED, SUPERSEDED. Agent-authored reports must not self-assign ACCEPTED.

## Handoff

A new session should resume from repository files: read project preflight, current state, active task, decisions, task queue, latest relevant report/review, and recent task logs; then verify actual branch and commit. Chat should contain a concise pointer, not the only copy of the report.
