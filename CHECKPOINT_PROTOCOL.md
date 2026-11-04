# Checkpoints, Task IDs, Coordination, and Multi-Agent Work

## Source of truth
- GitHub Issues are the canonical task inbox and asynchronous conversation record.
- Issue comments are append-only in practice for acknowledgments, progress, questions, decisions, blockers, and handoffs; edit/delete only to correct accidental or sensitive content under owner direction.
- Pull requests contain proposed code changes and review.
- Project-specific state/task/report files remain authoritative where the project already uses them.
- Optional live messages improve responsiveness but do not replace GitHub records.

## Coordinator task issue
#coor creates one complete GitHub Issue directly in the target repository. The issue is visible to authorized collaborators immediately; no coordinator branch or PR is required to expose task instructions.

Every task issue should include:
- Unique stable task ID.
- Issued/updated timestamps in UTC.
- Target repository, default branch, and base commit verified at publication.
- Status and priority.
- Objective and exactly one next action.
- Expected receiving role/capability; provider/model is optional.
- Current verified context, evidence references, existing work/PRs, blockers/unknowns.
- Scope and explicit exclusions.
- Dependencies.
- Required reading.
- Observable acceptance criteria and verification plan.
- Explicit authorizations, prohibited actions, approval gates, and cost/security/privacy constraints.
- Receiving-agent instructions and handoff expectations.

Do not include credentials, private customer/prospect data, or unnecessary personal information. Link to protected records rather than copying sensitive content.

## Task lifecycle
Suggested statuses:
- BACKLOG
- READY
- CLAIMED
- IN_PROGRESS
- BLOCKED
- REVIEW
- ACCEPTED
- REJECTED
- CANCELLED
- SUPERSEDED

The canonical status should be reflected in the issue body or a clearly structured status comment. Use labels only when they exist and have been verified. Do not create repository labels or project boards without authorization.

The coordinator authors the task issue and may amend its assignment intent. Receiving agents do not rewrite the issue body to acknowledge or report progress; they use comments and project records.

## Claiming and concurrency
A GitHub-only claim consists of a structured issue comment:
- Task ID.
- Agent identity (stable provider/session label, not an invented GitHub username).
- Role.
- Status: CLAIMED.
- UTC timestamp.
- Intended task branch.
- Optional lease expiry/heartbeat only if a project defines and can enforce it.

The agent re-fetches the issue and comments after posting its claim. If another active claim exists, stop and ask the coordinator to resolve ownership. A comment/label sequence is not an atomic lock and concurrent claims can race. The baseline protocol is conservative conflict detection, not a guarantee of exclusive execution.

For strict exclusive claims, use a single serialized dispatcher or atomic lease service. The dispatcher must atomically assign one task owner, issue a lease with expiry, support heartbeat/release, reject stale claims, and keep an audit trail. Do not build this into every project independently; it is a future Orqestra service capability.

## Receiving-agent procedure
1. Load the canonical Agent Protocol with #init.
2. Read the full task issue and relevant comments.
3. Read the current default-branch project instructions, specifications, task queue, state, decisions, and relevant source/tests.
4. Verify the task is current, not superseded/completed/cancelled, dependencies are satisfied, and scope matches owner instructions.
5. For #start, resume only this agent's existing claim. If no claim exists, ask whether to use #next unless the project defines a different behavior.
6. For #next, search eligible issues, inspect claims, select one, post a claim comment, then re-fetch to detect conflicts.
7. Create a separate implementation branch from latest default branch.
8. Execute only assigned scope. Stop and ask if authorization, source state, or safety conflicts appear.
9. Record milestones, blockers, questions, decisions, PR links, tests, outcomes, limitations, and next action in issue comments and the project's established records.
10. Submit a report for independent review. Do not self-accept.

## Independent review and acceptance
- Implementer status is SUBMITTED or IN_REVIEW.
- Independent reviewer evaluates code, tests, security, and each acceptance criterion.
- Reviewer records evidence and an ACCEPTED or REJECTED recommendation.
- Only coordinator/owner records final acceptance and closes the task.
- A merge does not automatically mean the task is accepted unless project policy explicitly says so.

## Asynchronous and live communication
### Asynchronous
Use the task issue as the shared thread for:
- acknowledgments and claims;
- progress and checkpoints;
- questions and answers;
- design decisions;
- blocker escalation;
- handoff and review outcomes.

Keep comments factual and concise. Link commits, PRs, reports, and relevant lines. Do not place secrets or sensitive prospect/customer details in issue comments.

### Live
A separate event/messaging adapter may:
- notify a human or connected agent runtime when an issue is created, assigned, commented on, labeled, or a PR changes;
- route a message to a specific agent or role;
- deliver a reply correlated to a task and message ID;
- request a human decision and return the decision to the task issue.

Every live message must carry a task ID and issue URL, be authenticated, schema-validated, idempotent, bounded by expiry/retry policy, and treated as untrusted input. Record consequential decisions and summaries in the issue.

A live relay cannot wake an ordinary idle ChatGPT/Grok session. Agent-to-agent automation requires active agent runners or platform integrations that receive events and are authorized to invoke a model. See docs/LIVE_MESSAGING.md.

## Checkpoint timing and fields
Post a checkpoint after meaningful implementation milestones, test results, decisions, blockers, handoffs, and before ending a long session.

Minimum fields:
- UTC timestamp, repository, branch, commit SHA or UNCOMMITTED.
- Task ID and issue URL.
- Agent identity and role.
- Goal and milestone.
- Completed work and paths.
- Exact tests run and outcomes; tests not run and why.
- Decisions, risks, blockers, next action, acceptance criteria.
- PR/report links.
- Current task claim/status.

## Multiple agents
- One active owner per task by default.
- Prefer one branch per task or agent.
- Parallel work only when the coordinator explicitly defines non-overlapping subtasks and dependencies.
- Inspect remote state before pushing; never force-push or overwrite concurrent changes.
- Keep reports and decisions linked to the canonical task issue.
- Do not create a second task queue or duplicate directive file for the same task.

## Handoff
A new chat/session should retrieve the active task from GitHub, read all relevant comments and project records, and verify actual branch/commit before resuming. Chat is a pointer, not the only copy of the work.
