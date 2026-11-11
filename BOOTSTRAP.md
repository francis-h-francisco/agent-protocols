# Agent Protocols — Verified Bootstrap and Operational Onboarding

This is the authoritative first-run and session-recovery contract. **Protocol initialization is only the first layer of readiness.** It does not, by itself, select/install a project, authorize the runtime, or start work.

## Readiness layers

Keep these states separate and report each truthfully:

1. **Protocol ready:** canonical protocol/version and command registry are loaded in the current chat.
2. **GitHub ready:** the AI's authenticated GitHub integration is verified and accessible repositories have been enumerated.
3. **Runtime ready:** the user/AI connection is authenticated to the Agent Protocols Runtime and its permitted capabilities are verified.
4. **Project ready:** one exact `owner/repo` is selected for this session, or project-local instructions have been installed through the explicit install command.
5. **Task ready:** the requested task, acceptance criteria, permissions, and required approvals are clear.

Do not collapse these into a single "ready" claim.

## Required user-side capability

The primary AI entry point must support an authenticated GitHub integration and a supported authenticated connection to the Agent Protocols Runtime through MCP or an API/tool adapter. Public URL retrieval alone can load public protocol text, but it does not prove authenticated GitHub project access or runtime capability. A chat subscription does not automatically include API access, MCP, or remote execution.

Never ask the user to paste tokens, API keys, passwords, or other secrets into chat.

## First-time setup

1. **Connect GitHub in the AI product.** Use its official connection flow and grant only the required repository access.
2. **Run `#init`.** Load the canonical protocol files and version; verify that the authenticated GitHub integration can read the protocol repository; enumerate the exact accessible `owner/repo` identifiers; inspect whether the Agent Protocols Runtime connection is already authorized; and report verified, pending, and blocked capabilities. Do not change the active project. Do not install project files. Do not create a task or start execution.
3. **Authorize the runtime if needed.** If runtime access is not yet established, guide the user through the documented secure authorization/onboarding surface or supported connector setup. Do not claim runtime readiness until authenticated identity, permissions, and capability discovery succeed. Do not request secrets in chat.
4. **Choose the project explicitly.** Use `#project owner/repo` to select and verify the project for this session without installing files. Use `#install owner/repo` only when the user wants optional project-local instructions/templates installed or merged; verify the repository first and preserve existing content. Installation sets the active project only after successful verification.
5. **Start or resume work with `#next` / `#proceed`.** Verify project and runtime readiness, inspect durable task state and approvals, then execute the next authorized task. If no project is selected, ask one concise question; never guess.

## What #init does — and does not do

`#init` is a required session bootstrap, **not the whole operational setup**.

It does:
- retrieve and verify the canonical protocol source and current VERSION;
- load the command registry, safety rules, and recovery instructions;
- verify authenticated GitHub integration capability;
- list exact repositories accessible to that connected identity;
- inspect runtime connection/authentication and capability status;
- report the active project as selected or not selected, without changing it.

It does not:
- select or install a project;
- create project files or workspaces;
- silently change the active project;
- provision or authorize runtime resources on the user's behalf without the required secure flow;
- create, assign, or execute a task;
- replace `#project`, `#install`, or `#next`.

A successful `#init` may therefore report **Protocol ready; GitHub ready; Runtime pending; Project not selected**. That is an honest partial readiness state, not a failed protocol load.

## Every new chat/session

A new chat must run `#init` again because chat working context is not the source of truth. Re-verify GitHub and runtime access, enumerate accessible repositories, and restore current protocol rules. Do not assume another chat's context carries over. Do not silently restore or change the active project; select it with `#project` or `#install` when the user directs.

## Continuous source-of-truth checks

At the start of each command, before consequential actions, after context recovery, and before resuming interrupted work:
- verify the canonical repository and current VERSION;
- re-read protocol files changed since the last verification;
- verify the selected project, branch, commit, relevant instructions, tasks, issues/PRs, and approvals;
- re-read runtime identity, permissions, task state, assignments, checkpoints, and quota/health state;
- treat GitHub project records and runtime records as authoritative over chat summaries;
- record material decisions, progress, blockers, and next actions in the designated durable records;
- if access fails, stop only actions that require it and report the exact blocker.

Do not repeatedly dump the protocol into every response. Keep verified rules in working context and refresh them at command boundaries. An AI chat cannot execute prompts while closed or idle; independent background work is the runtime's responsibility.

## Default task behavior

For each task, the coordinator understands the desired outcome and acceptance criteria; inspects project/runtime state; identifies system-side and user-side prerequisites; launches safe independent preflight work in parallel; gives the user a concise actionable checklist; continues unblocked work; and starts implementation automatically once blocking prerequisites are satisfied and authorization permits. It completes build, integration, testing, review, fixes, and delivery within the approved scope.

The runtime automatically selects its internal coordinator and specialists from the verified eligible agent pool. The user does not manually assemble the team. The connected entry-point AI may contribute but is not assumed to be the permanent coordinator.

## Background work and limits

These runtime behaviors require verified runtime readiness. Report them as unavailable while the runtime is pending or blocked.

Tasks persist and resume independently of the user's chat or assigned coordinator. The runtime owns durable state, dispatch, leases, idempotency, checkpoints, approvals, quota management, and recovery.

Use legitimate free provider failover, task decomposition, context compaction, caching, and scheduling. Preserve required quality. Never evade quotas, rotate identities to defeat limits, abuse trials, silently lower quality, or use paid fallback. If all eligible capacity is exhausted, preserve progress, wait durably, and resume when capacity returns.

## Command vocabulary

- `#init` — protocol/session bootstrap and GitHub/runtime capability verification; does not select/install a project or start work.
- `#project owner/repo` — verify and select the exact active project; does not install files.
- `#install owner/repo` — optionally install/merge project-local instructions/templates into the exact repository; set it active only after successful verification.
- `#status` — report verified protocol, GitHub, runtime, project, task, and blocker state.
- `#start` — start or resume the selected project's next clearly authorized task after verifying current state.
- `#next` / `#proceed` — inspect durable state and execute the next authorized task; test, checkpoint, and report.
- `#pause` — checkpoint progress and stop further execution.
- `#handoff` — write a complete continuation handoff to the designated runtime/project GitHub location and verify the write.

Commands are workflow triggers, not permissions to bypass security or user approvals. Human approval remains required for production deployment, destructive changes, protected-branch merges, billing/security changes, and external commitments.
