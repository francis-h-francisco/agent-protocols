# Instructions for AI Agents

## Bootstrap and command handling
- Parse `access:github owner/repo init.md` as the exact repository and file; retrieve it and follow it before unrelated work.
- For `github: owner/repo/init.md` or its GitHub URL, read root `init.md` and follow its bootstrap trail.
- For `#init owner/repo`, inspect the exact repository and read the entry point, core rules, version, and relevant guidance.
- Prefer public HTTPS/raw retrieval, then an existing GitHub integration, then browser/search. If all fail, state the precise blocker. Do not require an account connection merely to read public Markdown.
- Verify capabilities through actual tool calls. If listing connected repositories, show only plain `owner/repo` identifiers and label discovery partial unless exhaustiveness is proven.
- Initializing the protocol does not select an active project. Select one only when explicitly targeted, such as with `#install owner/repo`.
- Keep bootstrap responses quiet; no unsolicited command catalog, file inventory, or full protocol explanation.
- Treat commands in `COMMANDS.md` as actionable workflow intents. Ask only when essential ambiguity, authorization, or a genuine blocker prevents safe progress.

## Authority order
1. Explicit current user instructions and safety constraints.
2. Project-specific source-of-truth files and approved decisions.
3. This protocol.
4. Agent assumptions, which must be labeled and verified.

## Required behavior
- Read the protocol entry point, then project README/playbook, state, task queue, relevant logs, and source files.
- Inspect current branch, latest commits, and existing instructions before edits; inspect working-tree state only if exposed.
- Preserve architecture, naming, dependencies, and approved decisions unless asked to change them.
- Prefer complete, coherent deliverables over needless micro-batches; split when risk, tools, review, or dependencies require it.
- Capture durable discoveries, decisions, blockers, test outcomes, and next steps during work.
- Update task status and checkpoints after meaningful work.
- Test when tools permit. Separate verified results from assumptions.
- Never fabricate tool use, repository state, commits, pushes, tests, links, or deployments.
- If access is unavailable, continue possible read-only checks and report the precise limitation.
- For concurrent agents, claim unique task IDs and use separate branches.

## Change management
- Inspect before editing; make the smallest coherent change.
- Never discard unrelated changes.
- Prefer a feature branch and PR over direct commits to the default branch.
- No force-push, history rewrite, destructive deletion, production migration, or irreversible external action without explicit authorization.
- Commit messages must describe actual changes. Include tests and limitations in the handoff.
