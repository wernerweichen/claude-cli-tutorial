## Starting a Session

```bash
# Interactive session in current directory
claude

# With a starting prompt
claude "explain the auth module"

# Specify a model
claude --model claude-opus-4-8

# Print output and exit (non-interactive)
claude -p "summarise this file" < README.md
```

---

## Slash Commands

| Command | What it does |
|---------|-------------|
| `/help` | List all available commands and skills |
| `/clear` | Clear conversation history |
| `/compact` | Compress context to save tokens |
| `/config` | Open settings (model, theme, permissions) |
| `/cost` | Show token usage for this session |
| `/memory` | View and edit your memory files |
| `/status` | Show current model and context info |

---

## The `!` Prefix

Run a shell command without leaving Claude:

```
> !ls -la
> !git status
> !npm test
```

Output is shown in your terminal. Claude does **not** see this output unless you paste it in.

To let Claude see command output, describe what you ran:

```
> I ran `npm test` and got: [paste output here]
```

---

## Non-Interactive Mode: `-p` Flag

Use Claude in scripts and pipelines:

```bash
# Summarise a file
claude -p "summarise this" < notes.txt

# Generate and pipe to a file
claude -p "write a .gitignore for Node" > .gitignore

# Chain with other tools
git diff | claude -p "write a commit message for this diff"
```

`-p` exits after one response — no interactive session opened.

---

## `--model` Flag

Switch models for a session:

```bash
# Use Opus for complex reasoning
claude --model claude-opus-4-8

# Use Haiku for fast, cheap tasks
claude --model claude-haiku-4-5-20251001

# Default is Sonnet (balance of speed and capability)
claude  # uses claude-sonnet-4-6
```

Current model IDs:
- Opus 4.8: `claude-opus-4-8`
- Sonnet 4.6: `claude-sonnet-4-6`
- Haiku 4.5: `claude-haiku-4-5-20251001`

---

## Permission Modes

Controls what Claude can do without prompting:

| Mode | Claude can... |
|------|--------------|
| Default | Read files; asks before writing or running commands |
| Per-tool allow | Pre-approve specific tools in `settings.json` |
| `--dangerously-skip-permissions` | Do anything without prompting |

Configure per-tool permissions in `.claude/settings.json`:

```json
{
  "permissions": {
    "allow": ["Bash(git *)", "Read", "Edit"]
  }
}
```

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+C` | Cancel current response |
| `↑` | Recall previous prompt |
| `Ctrl+L` | Clear screen (keeps history) |
| `Shift+Enter` | New line without submitting |
| `Ctrl+R` | Search command history |
| `/` at start | Trigger a slash command |
| `!` at start | Run a shell command inline |

---

## Session Management

**Context window:** Claude has a finite context window. When it fills:
- Claude automatically compacts old messages
- Use `/compact` to trigger manually before it fills
- Use `/clear` to start completely fresh (loses all history)

**Resuming sessions:**

```bash
# Resume the last session
claude --continue

# Resume with an interactive session picker
claude --resume

# Resume a specific session by ID
claude --resume <session-id>
```

---

## Quick Reference Card

```
claude                    start interactive session
claude -p "..."           one-shot, non-interactive
claude --model <id>       choose model
claude --continue         resume last session

/help   /clear   /compact   /config   /cost

!<cmd>        run shell command inline
Ctrl+C        cancel response
↑             recall previous prompt
Shift+Enter   new line without submitting
```

Note: Keep this slide visible during Q&A — useful cheat sheet for the audience.
