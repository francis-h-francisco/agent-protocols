# Agent Protocols Runtime — connection details for AI agents

The runtime is the cloud service that runs tasks, keeps durable state, and gives agents GitHub access. **Agents read the address from this file. Users never need to know or remember it.**

| | |
|---|---|
| MCP endpoint (remote, Streamable HTTP) | `https://agent-protocols-api.francis-h-francisco.workers.dev/mcp` |
| REST mirror (for agents without MCP) | `POST https://agent-protocols-api.francis-h-francisco.workers.dev/api/v1/tools/<tool_name>` with a JSON body and the same sign-in token |
| Sign-in | OAuth 2.1 with PKCE and dynamic client registration; the AI product handles it. The sign-in window asks only for the person's **access password**. |

## How a person connects (once per AI product)

AI products let only the user add a connector, so an agent cannot connect itself. When the runtime is not connected, tell the user the steps **for the product you are running in**, with the MCP endpoint above ready to copy:

- **Claude** (claude.ai, desktop, mobile): Settings → Connectors → **Add custom connector** → name it `Agent Protocols Runtime`, paste the endpoint → **Add** → **Connect**.
- **Grok** (grok.com, paid plans): grok.com/connectors → **New Connector** → **Custom** → paste the endpoint → **Add Connector** → connect.
- **Any other MCP-capable product** (ChatGPT, Gemini, Codex, Cursor, VS Code and others): open its settings for **connectors**, **apps** or **MCP servers** and add a **custom remote MCP server** with the endpoint above. If you are unsure of the current steps for your product, look them up in its official documentation rather than guessing.

Then:

1. The product opens the runtime's sign-in window.
2. The person types their **access password** there. Never ask for it in chat, and never accept it in chat.
3. The window closes and returns to the chat. The connection stays saved in that product for future chats.

**No password yet?** Access is by invitation. The runtime owner creates a one-time invite link (`#invite`), and the person opens it to receive their own password. The owner's own password comes from the runtime's one-time setup page.

**Product limits:** some products or plans have no custom connectors (for example, free tiers). Say so plainly, then offer the **GitHub issue channel** below. The protocol itself can always be read without the runtime.

## Without a connector: the GitHub issue channel (runtime 0.10.0 and later)

Any AI, and the GitHub mobile app, can hand work to the team through GitHub issues.

**Capability tiers.** Pick the path your product supports:

| Your product | Path |
|---|---|
| Can add a custom MCP connector | Connect (above) and use the tools directly. |
| Cannot connect, but can read GitHub or the web | Read the protocol, and draft issues from `templates/github/agent-task.md` for the user to open. |
| Cannot read GitHub | Ask the user to paste the template, then fill it in. |

**One-time setup by the runtime owner:**
- link the person's GitHub account (`access_link_github`);
- turn the channel on for the project (`project_settings` with `issue_channel: true`).

**Each task:**
1. The person opens an issue labelled `agent-task` from the filled template.
2. The runtime checks the issue's **GitHub author**. It accepts the issue only if that account is linked to someone with access to the repository.
3. It replies in the issue and posts progress there.
4. When the work is ready, the person comments `/approve` (draft pull request) or `/reject`. `/pause`, `/resume` and `/cancel` also work.

**Rules:**
- Commands count only from the issue's author or the runtime owner, identified by GitHub's own authorship, never by what the text claims.
- Issue text is visible to everyone who can see the repository, so it must never contain secrets.
- Projects can copy `templates/github/ISSUE_TEMPLATE/agent-task.yml` into `.github/ISSUE_TEMPLATE/` to get a form.

## What the runtime provides once connected

| Tool | Purpose |
|---|---|
| `runtime_status` | Who you are (name, role, repositories), whether background work is running, and blockers. Call it first. |
| `protocol_get` | The canonical protocol files, for agents that cannot read GitHub. |
| `repo_list`, `repo_read` | GitHub access through the runtime, across every GitHub account the owner connected, limited to the repositories this person may use. **This satisfies GitHub readiness.** The agent does not need its own GitHub integration. |
| `task_estimate` | Before `task_create`: the request's tier (T0–T3) with reasons, expected effort, today's free capacity and the options. Creates nothing. |
| `project_register`, `task_create`, `task_get`, `task_list`, `task_events`, `artifact_get`, `task_control`, `task_export` | Hand work to the automatic AI team, follow it, and export its full record. |
| `approval_list`, `approval_decide` | Approvals, such as opening a draft PR. Decide only after the user explicitly decides. |
| `agent_pool`, `usage_status` | Free providers, capacity and quotas. |
| `notify_set` | Opt-in phone or webhook notifications when a task needs approval, is done, failed or is blocked. |
| `access_invite`, `access_list`, `access_grant`, `access_revoke` | Runtime owner only: manage who can use the runtime and which repositories they may use. |
| `dispatch_control`, `provider_set`, `project_settings` | Runtime owner only: pause or resume all background work, switch free providers on or off, and set per-project path rules and the issue channel. |
| `access_link_github` | Runtime owner only: link a person's GitHub account for the issue channel. |

Mutating tools need an `idempotency_key` (8–128 characters). Reuse the key only when retrying the same action.

## How the team works on a task

**Names used throughout the protocol:**
- **Lead:** you, the AI agent in the user's chat app.
- **Crew:** the runtime's free-tier models in their roles: Coordinator, Builder (coder), Writer, Researcher, Reviewer.
- **Runner:** the temporary test environment.

As Lead, keep the hard reasoning, design decisions and final judgment yourself. Give the Crew bounded, testable work, and review what comes back before asking the user to approve.


1. **Plan:** a coordinator model splits the outcome into steps.
2. **Do the work:** writer, coder and researcher models do the steps, using only free providers.
   - Private repositories go only to providers allowed to see private data.
   - If a provider hits its limit, the work switches to another eligible one. If none is free, the task waits and resumes later.
3. **Test (code changes only):** with a test command (runtime owner only), the runtime runs the project's tests in a temporary GitHub Codespace.
   - Failures go back to the coder, up to 3 runs.
   - Temporary branches and codespaces are deleted afterwards.
4. **Review:** a different model reviews the work against the acceptance criteria and the test result, and asks for one revision if needed.
5. **Approve and publish:** the result waits for the person's approval, then opens as a **draft** pull request whose description states the test result. Nothing is ever pushed to the default branch.

**Limits:**
- Each task has a model-call budget, 12 by default.
- Members can create 20 tasks a day.
- Only the owner can attach test commands.
- The owner's path rules limit where file changes may go.
