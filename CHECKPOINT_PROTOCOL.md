# Checkpoints, Task IDs, and Multi-Agent Work

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

## Handoff
A new session should resume from repository files: read state, task queue, latest checkpoint, recent task logs, then verify actual branch and commit.
