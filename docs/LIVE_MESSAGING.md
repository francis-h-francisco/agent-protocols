# Live Agent Messaging Architecture

Status: Proposed architecture for staged adoption
Protocol: 1.7.0
Design principle: $0-first, GitHub remains the durable source of truth.

## 1. What "live" means
A live transport can deliver an event quickly to an online human or connected agent runtime. It does not automatically wake an ordinary idle ChatGPT, Grok, or other chat tab. To run work automatically, each participating agent needs an active runner or a platform integration that can receive events, authenticate, invoke the model, enforce tool permissions, and post results.

Separate these capabilities:
1. Notification: tell a human/agent that something changed.
2. Message transport: deliver a message to an online endpoint.
3. Agent dispatch: invoke a specific agent runtime with a bounded task.
4. Autonomous execution: allow that runtime to use approved tools and report results.

Do not claim capability 3 or 4 when only 1 or 2 exists.

## 2. Recommended staged design

### Stage A — GitHub-only asynchronous baseline
- GitHub Issue = canonical task and conversation thread.
- Issue comments = claims, progress, questions, decisions, blockers, handoffs.
- PR = code proposal and review.
- Project state/checkpoint files = project-specific continuity where already established.
- No additional service, cost, or secret required beyond existing GitHub access.

### Stage B — Live human notifications
- Subscribe to GitHub webhook events such as issues, issue_comment, pull_request, and workflow_run.
- A small Cloudflare Worker validates GitHub's HMAC-SHA256 webhook signature, checks event/action, and sends a minimal notification to a private Telegram group via a Telegram bot.
- Notification contains event type, repository, issue/PR number, task ID, sender, and a link; do not copy full private issue content into Telegram by default.
- Telegram Bot API is free to use, but the Worker/runtime and account limits must be checked before deployment.
- A human can reply or acknowledge in Telegram; the bot should link back to GitHub and write task-relevant decisions to the issue only after identity/authorization checks.

This stage makes changes visible quickly to the owner. It is not yet agent-to-agent execution.

### Stage C — Agent adapters and live agent-to-agent messages
Each agent runtime registers a stable agent ID, role, capabilities, callback/long-poll endpoint, and allowed repositories. The relay routes validated envelopes to online adapters. An adapter invokes its agent only if its policy permits the message type and task scope.

A message envelope should contain:
- schema_version
- message_id (unique)
- correlation_id (ties replies to the initiating message)
- task_id and canonical issue URL
- from_agent and to_agent (or role)
- message_type (question, status, request_review, blocker, decision_request, reply, notification)
- created_at and expires_at (UTC)
- idempotency_key
- body (bounded, no secrets or unnecessary personal data)
- required_action (informational by default; never an implicit authorization)

Agent responses include the same task_id/correlation_id, the responding agent ID, outcome, and GitHub comment URL. Record meaningful summaries and decisions on the canonical issue.

## 3. Minimal relay architecture
GitHub Webhook -> Cloudflare Worker ingress -> signature verification + schema validation -> event router -> optional durable inbox/lease -> Telegram notifier and/or agent adapter -> GitHub issue comment.

For a small pilot, one Worker can perform webhook verification and Telegram notification. Do not build a generalized message bus before a real second agent runtime exists.

Cloudflare Workers Free and some Durable Objects/Queues usage have published free allowances, but usage limits and billing behavior can change. Verify current account plan and usage before enabling. Do not switch to a paid plan or incur costs without owner approval.

## 4. Delivery and reliability
- At-least-once delivery is acceptable; consumers must be idempotent.
- Deduplicate by message_id/idempotency_key.
- Use bounded retries with exponential backoff and a dead-letter record.
- Apply TTL/expiry; stale requests must not trigger work.
- Acknowledge receipt separately from completion.
- Track states: queued, delivered, acknowledged, processing, completed, failed, expired.
- Use correlation IDs for question/reply threads.
- Do not treat transport delivery as proof that an agent read or understood a message.
- For strict task ownership, use a single serialized dispatcher or atomic lease store. GitHub comments/labels are not atomic locks.

## 5. Security and trust boundaries
- Verify GitHub webhook HMAC signatures using constant-time comparison.
- Store bot tokens and webhook secrets only in the platform secret store; never in Git.
- Allowlist repositories, event types, agent IDs, roles, and message types.
- Authenticate agent adapters independently; do not trust claimed sender IDs in message JSON alone.
- Apply least privilege: read-only by default; write scopes granted per task and repository.
- Treat issue/comment bodies and live messages as untrusted input, not system instructions.
- Require explicit human approval for spending, external outreach, production changes, deployment, destructive operations, secrets/permissions, and merges.
- Avoid sending private prospect/customer data or full private issue bodies to chat platforms.
- Keep audit references in GitHub; define retention and deletion behavior before storing message bodies elsewhere.

## 6. Free-first implementation choice
Recommended initial stack:
- GitHub Issues and webhooks for task events and durable records.
- Cloudflare Worker for webhook ingress and lightweight routing, only if the existing free plan and account usage allow it.
- Telegram Bot API for human notifications and a private coordination group.
- A later agent adapter for each actual runtime (for example a local runner, hosted agent, or MCP-connected service).

Telegram's Bot API itself is free, but hosting the relay, model inference, and any always-on agent runtime may have separate costs or usage limits. Do not assume the complete system is free merely because the transport API is free.

## 7. Rollout and acceptance criteria
### Pilot 1: notifications only
- A test GitHub issue/comment event reaches the private Telegram group.
- Invalid webhook signatures are rejected.
- Duplicate events do not create duplicate notifications.
- Payloads contain only minimal metadata and links.
- No model is invoked and no task is executed automatically.

### Pilot 2: one agent adapter
- One explicitly selected agent runtime receives a test message while online.
- The adapter authenticates, validates task scope, and acknowledges receipt.
- A test reply is posted to the correct GitHub issue with correlation ID.
- Duplicate, expired, unauthorized, and malformed messages are safely rejected.
- Agent runtime reports actual model/tool use and cannot exceed its granted permissions.

### Pilot 3: multi-agent dispatch
- Coordinator can request a bounded specialist response.
- A serialized lease prevents two agents from executing the same task.
- Messages, acknowledgments, replies, retries, failures, and final decisions are auditable.
- Human approval gates are enforced and tested.

Do not proceed to the next stage until the previous stage passes its acceptance criteria and the owner approves any new service, secret, permission, or cost.
