# Agent Protocols Runtime — connection details for AI agents

The runtime is the cloud service that runs tasks, keeps durable state, and gives agents GitHub access. **Agents read the address from this file. Users never need to know or remember it.**

| | |
|---|---|
| MCP endpoint (remote, Streamable HTTP) | `https://agent-protocols-api.francis-h-francisco.workers.dev/mcp` |
| REST mirror (for agents without MCP) | `https://agent-protocols-api.francis-h-francisco.workers.dev/api/v1/<tool_name>` |
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

**Product limits:** some products or plans have no custom connectors (for example, free tiers). Say so plainly. The protocol can still be read without the runtime, but nothing that needs the runtime is available.

## What the runtime provides once connected

| Tool | Purpose |
|---|---|
| `runtime_status` | Who you are (name, role, repositories), whether background work is running, and blockers. Call it first. |
| `protocol_get` | The canonical protocol files, for agents that cannot read GitHub. |
| `repo_list`, `repo_read` | GitHub access through the runtime, limited to the repositories this person may use. **This satisfies GitHub readiness.** The agent does not need its own GitHub integration. |
| `project_register`, `task_create`, `task_get`, `task_list`, `task_events`, `artifact_get`, `task_control` | Hand work to the automatic AI team and follow it. |
| `approval_list`, `approval_decide` | Approvals, such as opening a draft PR. Decide only after the user explicitly decides. |
| `agent_pool`, `usage_status` | Free providers, capacity and quotas. |
| `access_invite`, `access_list`, `access_grant`, `access_revoke` | Runtime owner only: manage who can use the runtime and which repositories they may use. |

Mutating tools need an `idempotency_key` (8–128 characters). Reuse the key only when retrying the same action.
