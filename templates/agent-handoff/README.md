# Agent Handoff Records

This directory is the durable, project-local record of work across AI assistants, developers, and sessions. It is separate from preflight instructions: `.agent/PROJECT_PREFLIGHT.md` tells agents what to read and how to act; this directory records what happened.

## Standard project layout

Install this template set into the target project as follows:

- `README.md` → `docs/agent-handoff/README.md`
- `CURRENT_STATE.md` → `docs/agent-handoff/CURRENT_STATE.md`
- `ACTIVE_TASK.md` → `docs/agent-handoff/ACTIVE_TASK.md`
- `DECISIONS.md` → `docs/agent-handoff/DECISIONS.md`
- `reports/IMPLEMENTATION_REPORT.md` → `docs/agent-handoff/templates/IMPLEMENTATION_REPORT.md`
- `reviews/REVIEW_REPORT.md` → `docs/agent-handoff/templates/REVIEW_REPORT.md`

Create `docs/agent-handoff/reports/` for task-specific reports and `docs/agent-handoff/reviews/` for independent reviews. These are destinations for future records, not template files.

## Standard files

- `CURRENT_STATE.md`: concise verified project snapshot.
- `ACTIVE_TASK.md`: current task, ownership, scope, dependencies, and acceptance criteria.
- `DECISIONS.md`: durable decisions and rationale.
- `reports/`: audits, implementation reports, verification, and task handoffs.
- `reviews/`: independent reviews and acceptance decisions.
- `templates/`: reusable report templates.

## Required read order

Read current state, active task, decisions, and the latest relevant report/review, then verify the live repository, branch, commit, PR, and CI. Older records are historical and may be stale.

## Report states

- DRAFT — incomplete notes, not a handoff.
- SUBMITTED — author says work is complete; not independently verified.
- IN_REVIEW — independent assessment underway.
- ACCEPTED — explicitly accepted by the authorized owner/reviewer.
- REJECTED — not accepted; reasons recorded.
- SUPERSEDED — replaced by a newer record.

Green CI, a merged PR, or an agent's self-assessment does not alone imply product acceptance unless project policy explicitly defines that result.

## Record workflow

1. Create one task-scoped report per substantial audit or implementation.
2. Record exact repo, base/head commits, branch, PR, changed paths, commands, test results, CI links, limitations, and unverified claims.
3. Link the report in the PR description.
4. Update current state and active task; append durable decisions.
5. Independent reviewers record findings in reviews; do not rewrite the author's report to make claims appear independently verified.
6. Keep chat concise: report link/path, current status, blockers, next action, and owner decision.

## Privacy and integrity

Do not put secrets, credentials, access tokens, private prospect/customer records, or unnecessary personal data in records. Prefer links to commits, PRs, and CI runs over copying large diffs. Correct historical reports with a dated correction or superseding review.
