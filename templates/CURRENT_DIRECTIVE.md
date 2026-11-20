# Legacy Coordinator Directive Template

Status: DEPRECATED for new task assignments in Agent Protocol v1.7.0.

Use `templates/AGENT_TASK_ISSUE.md` and create the canonical assignment directly as a GitHub Issue in the target project repository. This makes task instructions immediately visible to authorized collaborators without requiring an unmerged coordinator branch or PR.

Do not create a second directive branch/PR for an ordinary task that can be represented by a GitHub Issue.

This template is retained only as a historical compatibility reference for projects that already have an active coordinator directive published on a branch. Such a directive remains valid until completed or explicitly superseded. New tasks should use the issue-first lifecycle in `COMMANDS.md`, `CHECKPOINT_PROTOCOL.md`, and `docs/LIVE_MESSAGING.md`.

If issue creation is unavailable, provide the complete task instructions in chat and explicitly mark them NOT PUBLISHED. Do not claim another agent can access a chat-only directive.
