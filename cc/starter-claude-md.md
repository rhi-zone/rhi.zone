# Starter CLAUDE.md

Copy this into `~/.claude/CLAUDE.md` (global) or `CLAUDE.md` (project root). Delete sections that don't apply. Add rules only when you've been corrected — not upfront.

---

```markdown
# CLAUDE.md

## Core Rules

**Corrections are documentation lag, not model failure.** When the same mistake recurs, the fix is writing the invariant down — not repeating the correction. Every correction that doesn't produce a CLAUDE.md edit will happen again. Exception: during active design, corrections are the work itself — don't prematurely document a design that hasn't settled yet.

**Conversation is not memory.** Anything established mid-session that isn't written to a file is gone next session. Write decisions down immediately.

**Don't announce actions.** No "I will now...", no trailing summaries of what you just did. Just do the work.

**Read before modifying.** Never propose changes to code you haven't read. Understand existing patterns before adding to them.

**Keep solutions minimal.** Only make changes directly requested or clearly necessary. Don't add error handling, refactors, or improvements beyond scope. Three similar lines of code is better than a premature abstraction.

**No backward-compatibility debris.** No renamed `_unused` vars, re-exported types, or `// removed` comments. If something is unused, delete it.

## Commit Convention

Use conventional commits: `type(scope): message`

Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`

Write commit messages in imperative mood. The message should say what the commit does, not what you did.

## Session Handoff

Use plan mode as a handoff mechanism when a task is complete or the session has drifted.

**Initiate a handoff after a significant mid-session correction.** When a correction happens after substantial wrong-path work, the wrong reasoning is still in context and keeps pulling. Write down the invariant, then hand off — the next session loads it from turn 1 before any wrong reasoning exists.

A handoff plan contains only: next tasks, blocked/pending items, and what was done this session if it directly affects what comes next. No commands, no build steps, no context summaries — those belong in CLAUDE.md or a TODO file.
```

---

## Layering

CLAUDE.md files layer: global (`~/.claude/CLAUDE.md`) → project root (`CLAUDE.md`) → subdirectory (`crates/foo/CLAUDE.md`). Rules in deeper files extend or override outer ones. Put ecosystem-wide conventions globally, project-specific rules in the project root.

---

## What to add over time

- Invariants you've had to correct twice
- Project-specific conventions (naming, file structure, testing patterns)
- Things that are obvious to you but not inferable from the code

Don't add edge cases preemptively. Rules should earn their place.

---

*Part of the [rhi.zone/cc](https://rhi.zone/cc/) Claude Code foundations. Full guide: [docs.rhi.zone/claude-code-guide](https://docs.rhi.zone/claude-code-guide)*
