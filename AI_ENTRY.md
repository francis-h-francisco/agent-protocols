# AI Agent Entry Point

This protocol is session-first and repository-backed. The minimal root init.md is the universal bootstrap entry point.

## Session initialization

When the user sends #init with no argument, load the canonical protocol from francis-h-francisco/agent-protocols. If an explicit protocol source is supplied, retrieve that exact source and verify it. Read VERSION, this file, AGENTS.md, and COMMANDS.md; read CHECKPOINT_PROTOCOL.md and SECURITY.md before project execution or when relevant.

Use public HTTPS/raw retrieval first, an existing GitHub integration second, and browser/search third. If all methods fail, state the concrete blocker. Never pretend the protocol was loaded.

After reading the command registry and rules:
1. Load command meanings, routing rules, safety boundaries, and recovery procedure into the current chat's working context.
2. Keep this protocol context available for the remainder of the current chat. Do not ask the user to repeat command definitions or reinitialize before each command.
3. Track the active project only when the user explicitly selects one or it is unambiguously established in the current session. Otherwise leave it unset.
4. Do not require project-local installation, a ChatGPT Project, .agent/, or docs/agent-handoff/ merely to use universal commands.
5. Return a compact response: protocol ready/version, command registry loaded, verified retrieval/access status, active project or not selected, ready.

A fresh chat does not reliably inherit another chat's working context. When the user sends #init in a new chat, retrieve the current protocol again and restore session readiness. Do not claim cross-chat memory unless the platform explicitly verifies it.

## Command dispatch

Treat COMMANDS.md as the universal command registry. Recognize commands by their leading command token, even when the user adds a repository, task, or natural-language details. Each command defines its own required retrieval and action sequence. Do not make the user repeat a project preflight checklist for every command.

If a command is received before initialization, attempt the canonical bootstrap automatically when retrieval tools are available. Then continue the requested command if its meaning and authorization are clear. If the protocol cannot be retrieved, explain the limitation and ask only for the minimum information needed to proceed safely.

Initialization and command recognition are not authorization to perform consequential actions. Follow explicit user instructions, repository permissions, and safety rules.

## Session context and recovery

Maintain a compact working context for the current chat:
- protocol version and whether the command registry was successfully loaded;
- active repository, if selected;
- current task/goal and its status when applicable;
- unresolved approval, safety, or access blockers;
- latest repository state verified.

At the start of a command, before consequential changes, and whenever context appears incomplete or contradictory:
1. Check whether the command registry and required project context are still available.
2. If protocol details are missing, uncertain, or inconsistent, re-fetch relevant protocol files from the canonical source.
3. Re-verify the active repository, branch, commit, task, and approvals from GitHub/project sources as needed.
4. Resume only after required facts are verified.

If recovery succeeds, continue and briefly disclose material recovery when useful. If recovery fails, stop before consequential action and tell the user exactly what is missing. Never silently guess, fabricate memory, or claim to detect every form of hidden context degradation. Agents cannot continuously monitor while idle; checks occur when a message or task boundary gives the agent an opportunity.

## Project selection and retrieval

- #project owner/repo selects the active project for this session after verifying the repository.
- #install owner/repo is optional: it installs or merges project-local instructions/templates. It is not required for command recognition or ordinary repository work.
- When a command names a repository, use that explicit repository for that command. Do not silently change the session's active project unless the command says to.
- When no repository is supplied and no active project is known, ask which repository to use. Never guess based on account ownership or unrelated chat history.
- Retrieve project instructions and state from the target repository when relevant. Prefer existing README, AGENTS.md, contributing guidance, project specifications, task records, and coordination directives. If standard files do not exist, use available verified project documentation; do not require creating a project folder just to continue.

## Optional project continuity files

Projects may adopt .agent/PROJECT_PREFLIGHT.md for project-specific instructions; .agent/coordination/CURRENT_DIRECTIVE.md for the latest coordinator directive; and docs/agent-handoff/ for durable state, tasks, decisions, reports, and reviews.

These files are optional conventions, not prerequisites for session initialization or universal command recognition. Create or install them only when the user requests installation or a workflow genuinely needs durable records. If absent, use existing repository documentation and report any continuity limitation.

## Project execution

Before editing a target repository, inspect its current branch and commit, root instructions, relevant source, existing task/decision records, open PRs, and CI as tools permit. Preserve project-specific conventions and unrelated work. Make focused changes, test where feasible, and report verified outcomes, blockers, and next steps. Use a branch and PR by default unless the user explicitly directs another safe publication method.

## Protocol repository is read-only for consumers

Agents consuming francis-h-francisco/agent-protocols are users, not contributors. Do not edit, branch, commit, push, open PRs, or synchronize changes to the protocol source unless the user explicitly identifies themselves as its maintainer and directly authorizes a specific protocol change. This restriction does not prevent authorized work in a separately designated project repository.
