## MCP — Model Context Protocol

A protocol for connecting Claude to **external tools and data sources**.

- MCP servers expose tools (functions Claude can call)
- Examples: filesystem access, web search, databases, GitHub, Slack
- You configure which servers Claude connects to in `settings.json`

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/your/path"]
    }
  }
}
```

---

## Adding an MCP Server

1. Find or build an MCP server package
2. Add it to `.claude/settings.json` under `mcpServers`
3. Restart Claude CLI — it connects automatically

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<your-token>"
      }
    }
  }
}
```

Claude can now call GitHub API tools directly in conversation.

---

## Skills

A **skill** is a named, reusable workflow triggered by a slash command.

- Installed via plugins: `/plugin install <name>`
- Invoked with `/skill-name` or `/skill-name args`
- Gives Claude a structured set of instructions to follow

```
/superpowers:brainstorming    guided design dialogue
/superpowers:writing-plans    implementation plan from a spec
/code-review                  review current diff for bugs
/superpowers:systematic-debugging  structured root-cause analysis
```

Skills turn ad-hoc prompts into **repeatable, reliable processes**.

---

## Agents

Claude can spawn **subagents** — independent Claude instances working in parallel or in isolation.

```
Main Claude session
├── Subagent A → research the auth module
├── Subagent B → write tests for the API
└── Subagent C → update documentation
```

- Each subagent has its own context window
- Results are returned to the parent session
- Used for parallelising work or isolating noisy research from the main context

---

## Artifacts

**Artifacts** are files Claude writes to disk during a session.

- Source code, config files, docs, scripts — any file Claude creates
- Created using the `Write` and `Edit` tools
- They persist after the session ends — they are real files in your project

```bash
# After asking Claude to scaffold a project:
your-project/
├── src/index.ts            ← artifact
├── tests/index.test.ts     ← artifact
└── tsconfig.json           ← artifact
```

Review artifacts the same way you'd review a colleague's PR.
