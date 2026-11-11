# AI Agent Entry Point — follow these steps in order

You are here because the user sent `#init github.com/francis-h-francisco/agent-protocols`, or `#init`. Complete steps 1–5 **before replying** and before doing anything else. If a step is impossible in your environment, say exactly which one and why, then continue with the next.

**Step 1: load the protocol.** Read these files from `francis-h-francisco/agent-protocols` (branch `main`):
- `VERSION`: https://raw.githubusercontent.com/francis-h-francisco/agent-protocols/main/VERSION
- `AGENTS.md`: https://raw.githubusercontent.com/francis-h-francisco/agent-protocols/main/AGENTS.md
- `COMMANDS.md`: https://raw.githubusercontent.com/francis-h-francisco/agent-protocols/main/COMMANDS.md
- `RUNTIME.md`: https://raw.githubusercontent.com/francis-h-francisco/agent-protocols/main/RUNTIME.md

If you can reach none of them but the runtime is connected, call its `protocol_get` tool instead. Keep the command registry and rules in mind for the rest of this chat. Never claim a version you did not read.

**Step 2: check the runtime connection.** Look among your available tools for the Agent Protocols Runtime (tools such as `runtime_status` and `protocol_get`).
- If present, call `runtime_status`. Success means **Runtime ready**; note the person's name, role and repositories.
- If the tools are missing, or the call needs sign-in, go to step 3.

**Step 3: if not connected, guide the one-time connection.** Using `RUNTIME.md`:
- Give the user the steps for **your own product**, with the MCP endpoint ready to copy. They should never have to find it themselves.
- Tell them the sign-in window will ask for their **access password**, and that the password goes only in that window, never in chat.
- If your product or plan cannot add custom connectors, say so plainly.
- Stop and wait. When they say they are done, repeat step 2.

**Step 4: GitHub readiness.** If the runtime is connected, call `repo_list`: the runtime is the GitHub bridge, and that list is the person's accessible repositories. Otherwise, use your own authenticated GitHub integration if you have one. Public web reading alone is not authenticated access.

**Step 5: reply briefly.**
- Protocol version.
- Runtime: ready as `<name>`, or exactly what is pending.
- Repositories: the exact `owner/repo` list, or how many and how to see them.
- Active project: `not selected` unless it was already selected in this chat.
- End with: **"Send `#help` to see what you can do."**

Do not select or install a project, create a task, or start work as part of initialization. A new chat is a new context: when the user sends `#init` again in a new chat, repeat these steps.

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

This contract applies once an authenticated runtime with these capabilities is connected and verified. If runtime readiness is pending or blocked, say so and do not claim automatic team selection, background execution, or quota failover.

The connected AI is the user's entry point and may contribute. The runtime automatically selects the internal coordinator and specialists from the verified eligible pool. Do not require manual team selection.

For each task, the coordinator identifies system/user prerequisites, launches safe independent preflight in parallel, provides a concise checklist, continues unblocked work, and starts implementation when blockers are satisfied and authorization permits. Durable background execution and recovery belong to the runtime, not the chat. Re-check protocol/project/runtime truth at command boundaries. See BOOTSTRAP.md and the runtime specification for quota, quality, approval, and recovery rules.
