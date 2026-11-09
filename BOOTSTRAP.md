# Agent Protocols — Verified Bootstrap Contract

This file is the authoritative first-run and session-recovery procedure for compatible AI agents.

## Required user-side capability

The AI agent used as the user's primary entry point must have an authenticated GitHub connection/integration. It must be able to read this public repository and, after the user selects it, access the intended project repository with the permissions the user grants. It must also be able to connect to the Agent Protocols Runtime through a supported authenticated MCP connection or API/tool adapter.

Public URL access alone is not enough for project operations. A chat product's free subscription does not automatically include API access, remote execution, or MCP support. Verify actual account/platform capabilities. Never claim universal compatibility.

## First-time setup — do these steps in order

1. **Connect GitHub in the AI product.** Use that product's official GitHub connection flow. Grant only the repository access needed. Never paste a personal access token or secret into chat.
2. **Load this protocol from its canonical source.** Retrieve the current README.md, VERSION, BOOTSTRAP.md, init.md, AI_ENTRY.md, AGENTS.md, COMMANDS.md, SECURITY.md, and CHECKPOINT_PROTOCOL.md from github.com/francis-h-francisco/agent-protocols. Verify the repository owner/name and current version. Do not rely on copied or stale instructions.
3. **Verify GitHub capability.** Use the connected GitHub integration to read this public repository. Report the actual connection capability, not just successful public URL retrieval.
4. **Select the project explicitly.** Ask the user for owner/repo if not already supplied in the current session. Use GitHub to verify the exact repository and inspect its README, AGENTS.md, current branch, latest commit, relevant project docs, issues/PRs, and current handoff/state. Never guess a project.
5. **Verify runtime access.** Authenticate to the Agent Protocols Runtime using its supported MCP/API connection. Discover identity/workspace, capabilities, permissions, eligible agent pool, quota/health state, current tasks, approvals, and resumable checkpoints. Do not assume a browser portal is required; use it only as a documented authorization/admin fallback.
6. **Load project and runtime instructions.** Read the project's source-of-truth instructions and the runtime's START_HERE.md, AGENTS.md, docs/STATUS.md, docs/HANDOFF.md, and relevant specification before acting.
7. **Report readiness truthfully.** State protocol version, GitHub connection verification, selected project, runtime connection/capabilities, and exact blockers. A missing GitHub or runtime connection means the corresponding operations are not ready. Do not claim "ready" based only on reading public Markdown.

## Every new chat/session

A new chat must repeat the verification sequence. Chat memory is not the source of truth. Retrieve the latest protocol and project/runtime state from GitHub and the runtime. Do not assume another chat's context carries over.

## Continuous source-of-truth checks

At the start of every command, before consequential actions, after any context-recovery boundary, and before resuming an interrupted task:

- Verify the canonical repository and current VERSION.
- Re-read any protocol files changed since the session's last verification.
- Re-read the selected project's relevant source-of-truth instructions and current task/branch/commit/PR state.
- Re-read runtime task state, approvals, assignments, checkpoints, and quota/health state.
- Treat GitHub project records and runtime records as authoritative over chat summaries.
- Record material decisions, progress, blockers, and next action in the project's established durable records.
- If source-of-truth access fails, stop only the actions that require it; explain the exact blocker and do not guess.

Do not repeatedly dump the protocol into every response. Keep the verified rules in working context and refresh them at the boundaries above. An AI chat cannot execute prompts while it is closed or idle; independent background work is the runtime's responsibility.

## Default task behavior

For each request, the coordinator must understand the desired outcome and acceptance criteria; inspect known project/runtime state; identify system-side and user-side prerequisites; launch safe independent preflight work in parallel; give the user a concise actionable checklist; continue unblocked work; and start implementation automatically when blocking prerequisites are satisfied. It must complete build, integration, testing, review, fixes, and delivery within authorization. Do not ask for redundant start confirmation.

The runtime automatically selects an internal coordinator and specialists from its verified eligible agent pool. The user does not need to manually choose agents for the MVP. A connected entry-point AI may contribute but is not assumed to be the permanent coordinator.

## Background work and limits

Tasks must persist and resume independently of the user's chat or assigned coordinator. The runtime owns durable state, dispatch, leases, idempotency, checkpoints, approvals, quota management, and recovery.

Use legitimate free provider failover, task decomposition, context compaction, caching, and scheduling to maximize capacity. Preserve minimum quality. Never evade quotas, rotate identities to defeat limits, abuse trials, or use paid fallback. If all eligible capacity is exhausted, preserve progress, wait for capacity/reset, and resume automatically.

## Command vocabulary

- #init — perform this complete bootstrap/recovery contract.
- #project owner/repo — select and verify the exact project.
- #status — report verified protocol, project, runtime, task, and blocker state.
- #next — inspect durable state and execute the next authorized task; verify sources first, then implement, test, checkpoint, and report.
- #pause — checkpoint progress and stop further execution.
- #handoff — write a complete continuation handoff to the runtime/project's designated durable GitHub location, including overall objective, current architecture, completed work, recent changes, exact repository/branch/commit state, decisions, blockers, approvals, safety constraints, and next actions. Verify the write. Do not replace the requested compact response with the handoff contents.

Commands are workflow triggers, not permissions to bypass security or user approvals. Human approval remains required for consequential actions such as production deployment, destructive changes, protected-branch merge, billing/security changes, and external commitments.
