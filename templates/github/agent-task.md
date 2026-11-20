# Agent task issue template

Use this when your AI product cannot connect to the runtime (for example, a free plan without custom connectors). Any AI can fill it in. You then open it as a GitHub issue yourself, on the web or in the GitHub mobile app.

**Before the first time:**
- The runtime owner must link your GitHub account to your runtime access.
- The owner must also turn on the issue channel for the project repository.

**Each time:**
1. Open a new issue in the project repository.
2. Paste the filled-in text below.
3. Add the label `agent-task`.

Instructions for the AI drafting it:
- Fill in every section.
- Keep acceptance criteria as checkable bullets.
- Do not include secrets, passwords or tokens. Issue text is visible to everyone who can see the repository.

---

**Title:** <short imperative title, e.g. "Add a contributor guide">

### Outcome
<What should exist when this is done, in one or two sentences.>

### Acceptance criteria
- <checkable statement>
- <checkable statement>

### Constraints
- <optional: rules to follow, e.g. "do not change the public API">

### Format
<Document | Files (code changes)>

### Files to read
- <optional: up to 8 repository paths the team should read first>

### Test command
<optional, files only, honoured only for the runtime owner: e.g. `npm test`>

### Publish
<yes | no: whether to offer a draft pull request after approval>

---

**After opening the issue:**
- The runtime replies in the issue within a few minutes, and posts progress there.
- When the work is ready, reply `/approve` to open a **draft** pull request, or `/reject` to decline it.
- Other commands are `/pause`, `/resume` and `/cancel`. They work only from the issue's author or the runtime owner.
