# Claude Code: minimal foundations

Most Claude Code setups grow elaborate fast — role-based agents, sprint workflows, 28 slash commands. This is a different approach: fewer rules, better placed, growing from use rather than spec.

The core insight: **a well-placed sentence beats a page of instructions**. CLAUDE.md at session start is the most diluted position in context. A correction mid-session that doesn't get written down will happen again. A fresh session after a significant wrong turn beats continuing with poisoned context.

The result is something that looks embarrassingly small next to sophisticated workflow systems. That's intentional.

---

## Pages

- **[Starter CLAUDE.md](starter-claude-md.md)** — a general-purpose template. Copy it, delete what doesn't apply, add what you learn.
- **[Post-history injection](hooks.md)** — contextual hints that land *after* conversation history, not before it.

---

## How to use this from Claude Code

Tell Claude to fetch a page:

```
Read https://rhi.zone/cc/starter-claude-md.md and use it as a starting point for my CLAUDE.md
```

Or reference a page in your CLAUDE.md to let Claude navigate here when needed:

```markdown
# See also
- Starter conventions: https://rhi.zone/cc/starter-claude-md.md
```

---

## Full guide

The extended guide with more patterns (session length, retry spirals, cost, usage instrumentation) lives at:
**https://docs.rhi.zone/claude-code-guide**
