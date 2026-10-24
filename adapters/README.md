# Adapting the Protocol to Different AI Environments

This protocol uses plain Markdown and JSON and does not require a specific model, vendor, IDE, or agent framework.

## Chat-only assistants
Ask the assistant to read `AI_ENTRY.md` and project state/task files using connected GitHub access or files you provide. If it cannot write to GitHub, request a patch or complete file contents and manually commit them.

## IDE coding agents
Point the agent at `AI_ENTRY.md` and retain project-specific instructions (for example, existing `AGENTS.md`, editor rules, or build instructions). Keep task ownership and checkpoints in Git.

## Automated agents / CI
Grant minimum required permissions. Use short-lived credentials or a trusted GitHub App, branch protections, pull requests, and explicit allowlists. Never expose secrets to model prompts or logs.

## Provider-specific wrappers
A wrapper may map `#next` to a workflow, but the semantics remain: inspect state, claim a unique task, implement, verify, log, checkpoint, and report. Do not make the protocol dependent on hidden chat memory.
