# Checkpoints, Task IDs, Coordination, and Multi-Agent Work

## Session vs. repository continuity
The protocol command registry is loaded into the current chat by #init; it does not need to be copied into every project. A new chat should retrieve the protocol again. GitHub repository records remain the durable source of project truth.

Project continuity files are optional:
- .agent/PROJECT_PREFLIGHT.md — project-specific instructions.
- .agent/coordination/CURRENT_DIRECTIVE.md — latest coordinator directive.
- docs/agent-handoff/ — state, active task, decisions, reports, reviews, and templates.

Use existing project conventions when these files are absent. Do not create folders merely to make universal commands work.

## Coordinator directive: purpose and ownership
#coor is the protocol's portable coordination command. It creates a bounded, durable control-plane handoff for another AI agent or a later session. It is not an agent-dispatch service and does not itself contact, launch, or notify another AI agent unless a connected platform explicitly provides and confirms that capability.

The coordinator (the current assistant acting under the owner's request) authors and publishes the directive. The receiving agent consumes it. The receiving agent must not rewrite coordinator-authored intent merely to acknowledge it. Acknowledgment and execution progress belong in the project's task/checkpoint/report records.

The directive is not a second task queue. It identifies the current objective and next approved action; detailed task progress remains in the project's established task/handoff system.

## Directive content contract
Every directive should include:
- Unique stable ID (for example COOR-YYYYMMDD-01).
- Issued and updated timestamps in UTC.
- Target repository and default branch/base commit verified at publication.
- Project objective and current milestone/task context.
- Status: DRAFT, READY_FOR_AGENT, ACKNOWLEDGED, IN_PROGRESS, BLOCKED, REVIEW, COMPLETED, or SUPERSEDED.
- Expected receiving role/capability; provider/model is optional and must not be invented.
- One clearly stated next action and priority.
- Scope, explicit exclusions, dependencies, and relevant paths.
- Acceptance criteria and verification plan.
- Required project/protocol documents and source references.
- Approval boundary: what is authorized and what is not.
- Publication location/ref and receiving-agent read instructions.

Do not include credentials, tokens, private prospect/customer data, or unnecessary personal information. Prefer references to protected project records over copying sensitive details.

## Publication and branch visibility
Use the project's established coordination location if one exists. Otherwise use .agent/coordination/CURRENT_DIRECTIVE.md based on the shared template.

Default publication:
1. Verify the target repository and current default branch/commit.
2. Create a dedicated coordinator branch from that base.
3. Add or update the directive and open a PR to the default branch.
4. Put the exact coordinator branch, path, PR URL, and base commit in the handoff response.
5. The receiving agent must fetch the directive from that exact branch/ref (or PR head), because an unmerged file is not present on the default branch.
6. The receiving agent creates a separate implementation branch from the current default branch, unless the owner explicitly directs otherwise. It must not merge the coordinator branch simply to obtain instructions.
7. If the coordinator PR has been merged, the receiver may read the directive from the default branch after verifying the merge.

A direct commit to the default branch is allowed only when the owner explicitly authorizes it or a verified project convention permits coordinator-only control-plane updates. Never assume permission from repository write access.

If GitHub write/PR capability is unavailable, return the full directive in the chat and label it NOT PUBLISHED. Do not imply a receiving agent has access to a chat-only directive.

## Receiving-agent procedure
At initialization/resumption, the receiving agent must:
1. Load the canonical Agent Protocol (normally #init).
2. Fetch the directive using the exact repository, branch/ref, and path supplied by the coordinator.
3. Read current default-branch project instructions, specifications, task queue, state, and relevant code/tests. The directive is not a substitute for project source-of-truth files.
4. Verify that the directive is current, not superseded, not already completed, and consistent with current owner instructions.
5. Acknowledge the directive ID in its existing task/checkpoint record when available; do not edit the coordinator-authored directive to acknowledge it.
6. Create a separate implementation branch from the latest default branch and execute only the assigned scope.
7. Stop and ask if scope, authorization, source state, or safety conflicts are discovered.
8. Record results in the established project report/task location, including exact files, commit/PR, tests and outcomes, limitations, blockers, and next action.
9. Use report status SUBMITTED or IN_REVIEW; only the coordinator/owner may accept a report. Never self-mark ACCEPTED.

If the project has no report convention, use docs/agent-handoff/reports/ when that location is appropriate; otherwise provide a concise report in the agent's response and ask before creating a new permanent structure.

## Task identity
Use stable task IDs such as T-001. Record objective, owner/agent, status, branch, dependencies, acceptance criteria, files touched, tests, and blockers. Do not assign one task to multiple agents without an explicit collaboration plan.

## Suggested task statuses
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
