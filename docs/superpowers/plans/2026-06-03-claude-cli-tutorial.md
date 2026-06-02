# Claude CLI Tutorial — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a 38-slide Reveal.js presentation on GitHub Pages teaching Claude CLI to developers with basic AI agent experience.

**Architecture:** A single `index.html` Reveal.js shell loads 7 Markdown slide files from a `slides/` directory using the Reveal.js Markdown plugin. No build step needed — GitHub Pages serves the static files directly. Local preview requires `python -m http.server` because the Markdown plugin uses `fetch()` and won't work with `file://` URLs.

**Tech Stack:** Reveal.js 5.x (CDN), Highlight.js (bundled with Reveal.js), GitHub Pages

---

## File Map

| File | Responsibility |
|------|----------------|
| `index.html` | Reveal.js shell — loads all slide files, configures theme and plugins |
| `slides/00-intro.md` | Title + agenda (2 slides) |
| `slides/01-cli-vs-others.md` | CLI vs other interfaces (4 slides) |
| `slides/02-commands.md` | Important commands — CORE (9 slides) |
| `slides/03-md-files.md` | Using .md files — CORE (9 slides) |
| `slides/04-mcp-skills.md` | MCP, skills, agents, artifacts (5 slides) |
| `slides/05-workflow.md` | Setting up workflows (4 slides) |
| `slides/06-superpowers.md` | The Superpowers plugin (5 slides) |
| `.nojekyll` | Prevents GitHub Pages Jekyll processing |
| `README.md` | Repo description and local preview instructions |

---

### Task 1: Create Reveal.js Shell

**Files:**
- Create: `index.html`
- Create: `.nojekyll`
- Create: `assets/screenshots/.gitkeep`

- [ ] **Step 1: Create `index.html`**

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Claude CLI Tutorial</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reveal.js@5/dist/reset.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reveal.js@5/dist/reveal.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reveal.js@5/dist/theme/moon.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reveal.js@5/plugin/highlight/monokai.css">
  <style>
    .reveal pre code { max-height: 480px; font-size: 0.85em; }
    .reveal table { font-size: 0.75em; }
  </style>
</head>
<body>
  <div class="reveal">
    <div class="slides">
      <section data-markdown="slides/00-intro.md"
               data-separator="^\n---\n"
               data-separator-vertical="^\n--\n"
               data-separator-notes="^Note:"></section>
      <section data-markdown="slides/01-cli-vs-others.md"
               data-separator="^\n---\n"
               data-separator-vertical="^\n--\n"
               data-separator-notes="^Note:"></section>
      <section data-markdown="slides/02-commands.md"
               data-separator="^\n---\n"
               data-separator-vertical="^\n--\n"
               data-separator-notes="^Note:"></section>
      <section data-markdown="slides/03-md-files.md"
               data-separator="^\n---\n"
               data-separator-vertical="^\n--\n"
               data-separator-notes="^Note:"></section>
      <section data-markdown="slides/04-mcp-skills.md"
               data-separator="^\n---\n"
               data-separator-vertical="^\n--\n"
               data-separator-notes="^Note:"></section>
      <section data-markdown="slides/05-workflow.md"
               data-separator="^\n---\n"
               data-separator-vertical="^\n--\n"
               data-separator-notes="^Note:"></section>
      <section data-markdown="slides/06-superpowers.md"
               data-separator="^\n---\n"
               data-separator-vertical="^\n--\n"
               data-separator-notes="^Note:"></section>
    </div>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/reveal.js@5/dist/reveal.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/reveal.js@5/plugin/markdown/markdown.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/reveal.js@5/plugin/highlight/highlight.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/reveal.js@5/plugin/notes/notes.js"></script>
  <script>
    Reveal.initialize({
      hash: true,
      progress: true,
      slideNumber: 'c/t',
      transition: 'slide',
      plugins: [RevealMarkdown, RevealHighlight, RevealNotes]
    });
  </script>
</body>
</html>
```

- [ ] **Step 2: Create `.nojekyll`**

Create an empty file named `.nojekyll` at the repo root. This prevents GitHub Pages from running Jekyll, which would otherwise ignore files in `slides/`.

PowerShell: `New-Item -ItemType File .nojekyll`
Unix: `touch .nojekyll`

- [ ] **Step 3: Create `assets/screenshots/` placeholder**

PowerShell:
```powershell
New-Item -ItemType Directory -Force assets/screenshots
New-Item -ItemType File assets/screenshots/.gitkeep
```

Unix:
```bash
mkdir -p assets/screenshots && touch assets/screenshots/.gitkeep
```

- [ ] **Step 4: Verify the shell loads**

Start a local server:
```bash
python -m http.server 8000
```

Open http://localhost:8000. Expected: dark moon-theme slide, Reveal.js navigation arrows visible, no JS errors in DevTools (CORS warnings about missing slide files are expected until slides exist).

- [ ] **Step 5: Commit**

```bash
git add index.html .nojekyll assets/screenshots/.gitkeep
git commit -m "feat: add Reveal.js shell and project scaffolding"
```

---

### Task 2: Intro + Agenda Slides

**Files:**
- Create: `slides/00-intro.md`

- [ ] **Step 1: Create `slides/00-intro.md`**

```markdown
# Claude CLI Tutorial

### From Chat to Workflow

*For developers with AI agent experience*

---

## Agenda

| # | Topic | Time |
|---|-------|------|
| 1 | CLI vs Other Interfaces | ~3 min |
| 2 | Important Commands | ~8 min |
| 3 | Using `.md` Files Properly | ~8 min |
| 4 | MCP, Skills, Agents & Artifacts | ~4 min |
| 5 | Setting Up Workflows | ~3 min |
| 6 | The Superpowers Plugin | ~4 min |
```

- [ ] **Step 2: Verify in browser**

With `python -m http.server 8000` running, open http://localhost:8000. Expected: first slide shows the title and subtitle; pressing `→` shows the agenda table with 6 rows.

- [ ] **Step 3: Commit**

```bash
git add slides/00-intro.md
git commit -m "feat: add intro and agenda slides"
```

---

### Task 3: CLI vs Other Interfaces Slides

**Files:**
- Create: `slides/01-cli-vs-others.md`

- [ ] **Step 1: Create `slides/01-cli-vs-others.md`**

```markdown
## Claude Interfaces

| | Web UI | API | CLI |
|---|---|---|---|
| Audience | Anyone | Developers | Developers |
| File access | ✗ | ✗ | ✓ |
| Persistent context | ✗ | Manual | ✓ CLAUDE.md |
| Hooks & automation | ✗ | ✗ | ✓ |
| Terminal integration | ✗ | ✗ | ✓ |
| Interactive session | ✓ | ✗ | ✓ |

---

## What CLI Adds

- **File access** — read and write any file in your project
- **Persistent context** — `CLAUDE.md` loads automatically every session
- **Hooks** — run shell commands before/after Claude acts
- **Terminal integration** — pipe input/output, chain with other tools
- **Plugins & skills** — extend Claude's capabilities with structured workflows

---

## When to Use Each

**Web UI** → quick questions, image analysis, casual brainstorming

**API** → building products, programmatic generation, batch processing

**CLI** → coding, file manipulation, project workflows, automation

---

## Key Insight

> The CLI treats Claude as a **collaborator in your terminal**,
> not a chatbot in a browser.

Everything else in this tutorial builds on that.

Note: Emphasise the mental model shift — same model, different relationship.
```

- [ ] **Step 2: Verify in browser**

Navigate to the Section 1 slides. Expected: 4 slides total; comparison table on slide 1; bullet list on slide 2; three bold lines on slide 3; blockquote on slide 4.

- [ ] **Step 3: Commit**

```bash
git add slides/01-cli-vs-others.md
git commit -m "feat: add CLI vs other interfaces slides"
```

---

### Task 4: Important Commands Slides (CORE)

**Files:**
- Create: `slides/02-commands.md`

- [ ] **Step 1: Create `slides/02-commands.md`**

```markdown
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

# List recent sessions
claude --list-sessions

# Resume a specific session
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
```

- [ ] **Step 2: Verify in browser**

Navigate to Section 2. Expected: 9 slides; bash code blocks with syntax highlighting; JSON block on the permissions slide highlighted; all tables render cleanly; progress bar advances through slides.

- [ ] **Step 3: Commit**

```bash
git add slides/02-commands.md
git commit -m "feat: add important commands slides"
```

---

### Task 5: Using .md Files Properly Slides (CORE)

**Files:**
- Create: `slides/03-md-files.md`

- [ ] **Step 1: Create `slides/03-md-files.md`**

```markdown
## What Is `CLAUDE.md`?

A plain Markdown file that Claude reads **automatically at the start of every session**.

- Placed at your project root (or `~/.claude/CLAUDE.md` for user-level defaults)
- Acts as persistent instructions — you don't re-explain your project every session
- Think of it as a **briefing document** for your AI collaborator

```bash
your-project/
└── CLAUDE.md   ← loaded automatically every session
```

---

## Where Claude Looks

Claude reads `.md` files from multiple locations, in priority order:

```
~/.claude/CLAUDE.md            ← user-level (always loaded)
your-project/CLAUDE.md         ← project root (always loaded)
your-project/src/CLAUDE.md     ← loaded when Claude works in src/
```

More specific files take precedence over more general ones on conflicts.

---

## What Belongs in `CLAUDE.md`

```markdown
## Project Overview
A REST API for managing user subscriptions. Node.js + PostgreSQL.

## Stack
- Runtime: Node.js 20
- DB: PostgreSQL 15 via `pg` library
- Test runner: Jest

## Key Commands
- `npm test`          run all tests
- `npm run lint`      ESLint + Prettier
- `npm run migrate`   run DB migrations

## Conventions
- snake_case for DB columns, camelCase in JS
- All endpoints return `{ data, error }` shape
- Write tests before implementation
```

---

## What Does NOT Belong

| Don't put this | Why |
|----------------|-----|
| API keys, secrets | Security risk — files get committed |
| Large data dumps | Wastes context window every session |
| Copy-pasted code | Code is already readable; don't duplicate it |
| Session history | `CLAUDE.md` is instructions, not a log |
| "Be helpful and concise" | Personality prompts waste context |

**Rule of thumb:** If Claude can read it from the codebase, don't repeat it in `CLAUDE.md`.

---

## The Memory System

Claude Code supports a `memory/` directory for notes that persist across sessions:

```
~/.claude/projects/<project-hash>/memory/
├── user_profile.md        ← who you are, how you work
├── feedback_testing.md    ← corrections and preferences Claude should remember
└── project_context.md     ← ongoing decisions and goals
```

Tell Claude to save something:

> *"Remember that we always use integration tests, not mocks."*

Claude writes a memory file and indexes it in `MEMORY.md`.

---

## Writing Effective Context

**Be specific and imperative:**

```markdown
# Vague (bad)
Be careful with the database.

# Specific (good)
Never drop tables. Always use migrations in `db/migrations/`.
Run `npm run migrate:dry` before any schema change.
```

**Use headings** so Claude can locate sections quickly.

**Keep it current** — stale instructions are worse than no instructions.

---

## Multiple `.md` Files

For large projects, split context by area:

```
your-project/
├── CLAUDE.md              ← project-wide: stack, commands, conventions
├── src/api/CLAUDE.md      ← API-specific: auth patterns, endpoint shape
└── src/db/CLAUDE.md       ← DB-specific: schema notes, migration rules
```

Claude loads the nearest `.md` file when working in a subdirectory.

---

## Before & After

**Before (vague):**
```markdown
This is a web app. Use good practices.
Work carefully with the database.
```

**After (effective):**
```markdown
## Stack
Next.js 14, Prisma ORM, PostgreSQL, Jest

## Commands
- `npm test`                   run tests
- `npx prisma migrate dev`     apply migrations

## Rules
- Never use `prisma.$executeRaw` — use typed queries only
- All API routes must validate input with Zod before touching the DB
```

---

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Empty `CLAUDE.md` | Add at minimum: stack, key commands, conventions |
| Never updating it | Review after major refactors — stale context misleads Claude |
| Too long (500+ lines) | Split into subdirectory files; trim redundant entries |
| Secrets in the file | Use `.env`; put env var *names* in `CLAUDE.md`, not values |
| Long prose paragraphs | Use short, imperative bullet points instead |

Note: The before/after slide resonates most with audiences — give it extra time.
```

- [ ] **Step 2: Verify in browser**

Navigate to Section 3. Expected: 9 slides; `markdown` and `bash` code blocks highlighted; all tables render cleanly; no slides bleed off-screen vertically.

- [ ] **Step 3: Commit**

```bash
git add slides/03-md-files.md
git commit -m "feat: add using .md files slides"
```

---

### Task 6: MCP, Skills, Agents & Artifacts Slides

**Files:**
- Create: `slides/04-mcp-skills.md`

- [ ] **Step 1: Create `slides/04-mcp-skills.md`**

```markdown
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
```

- [ ] **Step 2: Verify in browser**

Navigate to Section 4. Expected: 5 slides; JSON blocks highlighted; directory tree renders as a plain text block; agent diagram renders as plain text lines.

- [ ] **Step 3: Commit**

```bash
git add slides/04-mcp-skills.md
git commit -m "feat: add MCP, skills, agents, and artifacts slides"
```

---

### Task 7: Workflow Setup Slides

**Files:**
- Create: `slides/05-workflow.md`

- [ ] **Step 1: Create `slides/05-workflow.md`**

```markdown
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
```

- [ ] **Step 2: Verify in browser**

Navigate to Section 5. Expected: 4 slides; JSON code blocks highlighted; hook event table renders cleanly.

- [ ] **Step 3: Commit**

```bash
git add slides/05-workflow.md
git commit -m "feat: add workflow setup slides"
```

---

### Task 8: Superpowers Plugin Slides

**Files:**
- Create: `slides/06-superpowers.md`

- [ ] **Step 1: Create `slides/06-superpowers.md`**

```markdown
## The Superpowers Plugin

A plugin that adds **structured engineering workflows** as skills to Claude CLI.

Without it: Claude is a capable but free-form collaborator.

With it: Claude follows opinionated, repeatable processes — like having a senior engineer pair with you who never skips steps.

```bash
/plugin install superpowers@claude-plugins-official
/reload-plugins
```

---

## Installing Superpowers

```bash
# Step 1: Install the plugin
/plugin install superpowers@claude-plugins-official

# Step 2: Apply changes (required after every install)
/reload-plugins

# Verify it loaded — you should see superpowers:* skills listed
/help
```

The plugin installs to `~/.claude/plugins/` and persists across all sessions.

---

## The Core Skills Pipeline

Most engineering work follows this path:

```
/superpowers:brainstorming
    ↓  produces a design spec
/superpowers:writing-plans
    ↓  produces a task-by-task implementation plan
/superpowers:subagent-driven-development
    ↓  executes the plan with review between tasks
/superpowers:verification-before-completion
    ↓  verifies work before claiming done
```

Each skill is a structured dialogue — asks questions, builds an artefact, hands off to the next.

---

## Invoking a Skill

```bash
# Start brainstorming a new feature
/superpowers:brainstorming I want to add user authentication

# Review the current diff for bugs
/code-review

# Deep multi-agent review (cloud, billed)
/code-review ultra

# Debug a failing test with structured root-cause analysis
/superpowers:systematic-debugging
```

Skills accept natural-language arguments. They read context, ask clarifying questions, and guide you through the process.

---

## Why It Matters

| Without superpowers | With superpowers |
|--------------------|------------------|
| Free-form prompting | Structured, repeatable process |
| Re-explain context each time | Spec + plan + memory persist across sessions |
| Easy to skip steps | Checklist enforces completeness |
| Claude guesses your intent | Brainstorming clarifies before any code is written |

**The payoff:** less time fixing AI mistakes, more time on real problems.

Note: Good place to pause for questions — audiences often ask "can it do X?" about specific skills.
```

- [ ] **Step 2: Verify in browser**

Navigate to Section 6. Expected: 5 slides; bash code blocks highlighted; pipeline diagram renders as a plain text block; final comparison table renders cleanly.

- [ ] **Step 3: Commit**

```bash
git add slides/06-superpowers.md
git commit -m "feat: add superpowers plugin slides"
```

---

### Task 9: README and GitHub Pages Deployment

**Files:**
- Create: `README.md`

- [ ] **Step 1: Create `README.md`**

```markdown
# Claude CLI Tutorial

A 30-minute Reveal.js presentation on GitHub Pages teaching Claude CLI to developers with basic AI agent experience.

**Live site:** https://\<your-github-username\>.github.io/claude-cli-tutorial/

## Topics

1. CLI vs Other Interfaces
2. Important Commands
3. Using `.md` Files Properly
4. MCP, Skills, Agents & Artifacts
5. Setting Up Workflows
6. The Superpowers Plugin

## Local Preview

```bash
python -m http.server 8000
# Open http://localhost:8000
```

Requires a local server — the Markdown plugin uses `fetch()` and won't work with `file://` URLs.

## Slide Navigation

| Key | Action |
|-----|--------|
| `→` / `Space` | Next slide |
| `←` | Previous slide |
| `F` | Fullscreen |
| `S` | Speaker notes |
| `Esc` | Slide overview |
```

- [ ] **Step 2: Commit README**

```bash
git add README.md
git commit -m "feat: add README with local preview and navigation instructions"
```

- [ ] **Step 3: Create GitHub repo and push**

Using GitHub CLI (replace `<your-username>` with your actual GitHub username):

```bash
gh repo create claude-cli-tutorial --public --source=. --remote=origin --push
```

Or manually via the web UI:
1. Go to https://github.com/new
2. Name: `claude-cli-tutorial`, set to Public, do NOT add a README
3. Then push:
```bash
git remote add origin https://github.com/<your-username>/claude-cli-tutorial.git
git push -u origin main
```

- [ ] **Step 4: Enable GitHub Pages**

In your GitHub repo:
1. Go to **Settings** → **Pages**
2. Source: **Deploy from a branch**
3. Branch: `main`, directory: `/ (root)`
4. Click **Save**

Wait ~2 minutes, then open `https://<your-username>.github.io/claude-cli-tutorial/`

- [ ] **Step 5: Verify live site**

Open the GitHub Pages URL. Expected:
- Title slide loads with dark moon theme
- `→` navigates through all 38 slides without errors
- Code blocks have syntax highlighting
- No JavaScript errors in browser DevTools
- Progress bar visible at bottom of screen
- Site renders without horizontal scrolling at 1080p
