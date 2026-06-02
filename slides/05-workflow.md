## Hooks in `settings.json`

Hooks let you **run shell commands automatically** at specific points in Claude's lifecycle.

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          { "type": "command", "command": "npm run lint --silent" }
        ]
      }
    ],
    "Stop": [
      {
        "hooks": [
          { "type": "command", "command": "echo 'Session complete'" }
        ]
      }
    ]
  }
}
```

---

## Hook Event Types

| Event | Fires when... |
|-------|--------------|
| `PreToolUse` | Before Claude calls any tool |
| `PostToolUse` | After Claude calls a tool |
| `Stop` | When Claude finishes a response |
| `Notification` | When Claude sends a notification |

**`matcher`** filters by tool name (supports `|` for multiple):
- `"Edit"` — only on file edits
- `"Bash"` — only on shell commands
- `"Edit|Write"` — on either

---

## Example: Auto-Lint on Every Edit

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "npx eslint --fix \"$CLAUDE_TOOL_RESULT_FILE_PATH\" 2>/dev/null || true"
          }
        ]
      }
    ]
  }
}
```

Claude edits a file → ESLint fixes it automatically → next time Claude reads the file, it sees clean code.

---

## When Workflows Pay Off

**Immediate value (set up once, runs every session):**
- Auto-lint/format on every file edit
- Run tests after code changes
- Desktop notification when Claude finishes a long task

**Team value:**
- Commit `.claude/settings.json` to the repo
- Everyone gets the same hooks and permissions
- Onboarding: `git clone` → `claude` → productive immediately

Note: The shared `settings.json` angle resonates with team leads — it's like `.editorconfig` for AI behaviour.
