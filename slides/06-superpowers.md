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
