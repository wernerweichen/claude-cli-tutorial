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
