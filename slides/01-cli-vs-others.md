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
