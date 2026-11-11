# AI Agent Entry Point

This protocol is repository-backed and command-driven. The minimal root `init.md` is the universal session bootstrap entry point. Read BOOTSTRAP.md for the complete distinction between protocol readiness and operational/project readiness.

## Session initialization

When the user sends `#init` with no argument, load the canonical protocol from `francis-h-francisco/agent-protocols`. If an explicit protocol source is supplied, retrieve that exact source and verify it. Read VERSION, this file, AGENTS.md, and COMMANDS.md; read CHECKPOINT_PROTOCOL.md and SECURITY.md before project execution or when relevant.

The primary AI must verify its authenticated GitHub integration, confirm access to the canonical protocol, and enumerate exact accessible `owner/repo` identifiers. It must separately verify whether the authenticated Agent Protocols Runtime MCP/API connection is available. Public URL access alone is not proof of authenticated GitHub or runtime access.

After reading the command registry and rules:
1. Load command meanings, routing rules, safety boundaries, and recovery procedure into the current chat's working context.
2. Keep protocol context available for the remainder of the current chat. Do not ask the user to repeat command definitions or reinitialize before each command.
3. Report GitHub repository access and runtime readiness separately, including exact blockers.
4. Report the active project only if already explicitly selected or unambiguously established in the current session; otherwise leave it unset.
5. Do not select/install a project, create project files, change active project, create a task, or start execution as a side effect of `#init`.
6. Return a concise readiness report with protocol version, GitHub verification/repository identifiers, runtime status, and active project or not selected.

A fresh chat does not reliably inherit another chat's working context. When the user sends `#init` in a new chat, retrieve the current source again. Do not claim cross-chat memory unless the platform explicitly verifies it.

## Command dispatch

Treat COMMANDS.md as the universal command registry. Recognize commands by their leading command token, even when the user adds a repository, task, or natural-language details. Each command defines its own required retrieval and action sequence.

If a command is received before initialization, attempt the canonical bootstrap automatically when retrieval tools are available. Then continue the requested command if its meaning, target, and authorization are clear. If protocol retrieval fails, explain the limitation and ask only for the minimum information needed.

Initialization and command recognition are not authorization to perform consequential actions. Follow explicit user instructions, repository permissions, and safety rules.

## Session context and recovery

Maintain compact working context for the current chat:
- protocol version and command-registry status;
- GitHub connection verification and accessible repository identifiers;
- runtime connection/authorization status and verified capabilities;
- active repository, if selected;
- current task/status and unresolved approvals, safety, or access blockers;
- latest repository/runtime state verified.

At command start, before consequential changes, and whenever context appears incomplete or contradictory:
1. Check whether the command registry and required project context remain available.
2. Re-fetch relevant protocol files if missing, uncertain, inconsistent, or changed.
3. Re-verify the active repository, branch, commit, task, approvals, and runtime state as needed.
4. Resume only after required facts are verified.

If recovery succeeds, continue and briefly disclose material recovery when useful. If recovery fails, stop before consequential action and state exactly what is missing. Do not claim perfect detection of hidden context degradation; checks occur at interaction/task boundaries.

## Project selection and installation

- `#project owner/repo` verifies the exact repository and selects it as the active project for this session. It does not install files.
- `#install owner/repo` is a separate, optional project setup command. It verifies the exact repository, inspects existing instructions, and installs/merges project-local instructions/templates only when requested. It sets the active project only after successful verification and installation.
- `#init` does neither of these and must never silently change the active project.
- When a command names a repository, use that explicit repository for that command. Do not silently change the active project unless the command explicitly does so.
- If a command requires a project and none is selected or supplied, ask which repository to use. Never guess based on account ownership or unrelated chat history.
- Prefer existing README, AGENTS.md, contributing guidance, project specifications, task records, and coordination directives. Do not require creating a project folder just to continue.

## Optional project continuity files

Projects may adopt `.agent/PROJECT_PREFLIGHT.md`, `.agent/coordination/CURRENT_DIRECTIVE.md`, and `docs/agent-handoff/`. These are optional conventions, not prerequisites for session initialization or ordinary project work. Install them only when requested or genuinely needed for durable coordination.

## Project execution

Before editing, inspect the current branch/commit, root instructions, relevant source, existing task/decision records, open PRs, and CI as tools permit. Preserve project conventions and unrelated work. Make focused changes, test where feasible, and report verified outcomes and blockers. Use a branch and PR by default unless the user explicitly directs another safe method.

## Protocol repository is read-only for consumers

Agents consuming `francis-h-francisco/agent-protocols` are users, not contributors. Do not edit, branch, commit, push, open PRs, or synchronize changes to the protocol source unless the user explicitly identifies themselves as its maintainer and directly authorizes a specific protocol maintenance task.

## Current automatic-team contract

The connected AI is the user's entry point and may contribute. The runtime automatically selects the internal coordinator and specialists from the verified eligible pool. Do not require manual team selection.

For each task, the coordinator identifies system/user prerequisites, launches safe independent preflight in parallel, provides a concise checklist, continues unblocked work, and starts implementation when blockers are satisfied and authorization permits. Durable background execution and recovery belong to the runtime, not the chat. Re-check protocol/project/runtime truth at command boundaries. See BOOTSTRAP.md and the runtime specification for quota, quality, approval, and recovery rules.
