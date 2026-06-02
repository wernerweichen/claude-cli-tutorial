# Claude CLI Tutorial — Design Spec

**Date:** 2026-06-03
**Format:** 30-minute live presentation
**Delivery:** Reveal.js slideshow on GitHub Pages (shown on projector/screen share)

---

## Purpose

A linear tutorial for programmers who already have basic AI agent knowledge. The goal is to teach Claude CLI specifically — what makes it different from other interfaces, how to use it effectively day-to-day, and how to build disciplined workflows with it.

## Audience

Programmers with basic familiarity with AI agent tools (e.g., ChatGPT, Copilot, API usage). No prior Claude CLI experience assumed. Claude CLI installation is assumed complete before the presentation.

---

## Technical Approach

**Stack:** Reveal.js with the built-in Markdown plugin, hosted on GitHub Pages.

- `index.html` is a thin Reveal.js shell (~40 lines) that loads each section from a separate `.md` file
- Slides within each `.md` file are separated by `---`
- No build step required — GitHub Pages serves the static files directly
- Local preview: `python -m http.server`
- All examples are self-contained code blocks (no live demo moments)

**Theme:** `moon` (dark background, projector-friendly, good contrast)
**Navigation:** Horizontal only — simple linear left/right flow
**Code highlighting:** Highlight.js (built into Reveal.js), language-labeled blocks
**Progress bar:** Enabled so presenter can gauge pace

---

## Site Architecture

```
claude-cli-tutorial/
├── index.html                ← Reveal.js shell, loads all sections
├── slides/
│   ├── 00-intro.md
│   ├── 01-cli-vs-others.md
│   ├── 02-commands.md
│   ├── 03-md-files.md
│   ├── 04-mcp-skills.md
│   ├── 05-workflow.md
│   └── 06-superpowers.md
├── assets/
│   └── screenshots/
└── README.md
```

---

## Content Structure

| # | File | Title | Time | Slides |
|---|------|-------|------|--------|
| 0 | `00-intro.md` | Title + Agenda | ~2 min | 2 |
| 1 | `01-cli-vs-others.md` | CLI vs Other Interfaces | ~3 min | 4 |
| 2 | `02-commands.md` | Important Commands | ~8 min | 9 |
| 3 | `03-md-files.md` | Using .md Files Properly | ~8 min | 9 |
| 4 | `04-mcp-skills.md` | MCP, Skills, Agents & Artifacts | ~4 min | 5 |
| 5 | `05-workflow.md` | Setting Up Workflows | ~3 min | 4 |
| 6 | `06-superpowers.md` | The Superpowers Plugin | ~4 min | 5 |
| **Total** | | | **~32 min** | **38** |

---

## Section Outlines

### Section 0 — Intro + Agenda (2 slides)
- Title slide: course name, presenter, date
- Agenda slide: list all 6 topics with time estimates

### Section 1 — CLI vs Other Interfaces (4 slides)
- Comparison table: Web UI vs API vs CLI
- What CLI uniquely provides: file access, persistent context, hooks, automation, terminal integration
- When to use each interface
- Key takeaway: CLI is for developers who want Claude integrated into their actual workflow

### Section 2 — Important Commands (9 slides) — CORE
- Starting a session: `claude` command and flags
- Slash commands overview: `/help`, `/clear`, `/compact`, `/config`, `/cost`
- The `!` prefix: running shell commands inline
- Non-interactive mode: `--print` / `-p` flag for scripting and pipelines
- `--model` flag: switching models on the fly
- Permission modes: what they control, when to use each
- Keyboard shortcuts reference
- Session management: context window, compaction
- Summary slide: quick reference card

### Section 3 — Using .md Files Properly (9 slides) — CORE
- What `CLAUDE.md` is and why it matters
- Where Claude looks for `.md` files (project root, subdirs, user-level)
- What belongs in `CLAUDE.md`: project overview, conventions, commands to run
- What does NOT belong: secrets, large data dumps, redundant code
- Memory system: the `memory/` directory pattern
- Writing effective context: be specific, use imperatives, keep it current
- Multiple `.md` files: how Claude prioritizes and merges them
- Example: before/after a well-written `CLAUDE.md`
- Common mistakes and how to fix them

### Section 4 — MCP, Skills, Agents & Artifacts (5 slides)
- MCP (Model Context Protocol): what it is, how it extends Claude's capabilities
- Adding an MCP server: `settings.json` config pattern
- Skills: plugin-defined slash commands (`/skill-name`)
- Agents: spawning subagents for parallel or isolated tasks
- Artifacts: files Claude produces during a session, how to use them

### Section 5 — Setting Up Workflows (4 slides)
- Hooks in `settings.json`: pre/post tool call, stop hooks
- Common automation patterns: lint on edit, test on save, format on commit
- Example hook: running a command after Claude stops
- When workflows pay off: repeated tasks, team consistency, CI integration

### Section 6 — The Superpowers Plugin (5 slides)
- What superpowers is: a plugin that adds structured engineering workflows as skills
- Installing: `/plugin install superpowers@claude-plugins-official` + `/reload-plugins`
- Key skills and the pipeline they form: `brainstorming` → `writing-plans` → `executing-plans`
- Invoking a skill: `/skill-name` or `/skill-name args`
- Why it matters: turns Claude CLI from a chat tool into a disciplined, repeatable engineering process

---

## Success Criteria

- Presenter can deliver the full deck in 28–32 minutes
- Every code example is self-contained and copy-pasteable
- A viewer leaving the talk can set up `CLAUDE.md`, run core commands, and install the superpowers plugin without additional resources
- Site renders cleanly at 1080p on a projector with no horizontal scrolling
