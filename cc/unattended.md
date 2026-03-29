# Unattended automation

Claude Code sessions don't have to be interactive. `-p` runs headless with a prompt as an argument; `--dangerously-skip-permissions` skips all permission prompts. Together they enable sessions kicked off by a scheduler without human oversight.

```bash
claude -p --dangerously-skip-permissions "your prompt here"
```

## Concurrency guard

When a timer fires every minute, prevent overlapping sessions with a lockfile and zombie detection:

1. On startup: check for a lockfile. If present, check recent session activity (`.jsonl` file mtime). Active → exit. Stale (crashed) → kill the process, remove lockfile, continue.
2. Write the lockfile *before* spawning, so the next tick sees it immediately.
3. Session removes the lockfile on clean exit.

## Pre-check before spawning

Don't spawn a session for nothing. Query inputs first — notifications, pending events, scheduled tasks — with read-only calls that have no side effects. Only launch if there's something to act on.

```
timer fires every minute
  → check for activity (read-only)
  → nothing? exit immediately
  → something? write lockfile, spawn session
```

This keeps idle cost near zero.

## Prompt structure

The `-p` prompt is the full session instruction. Structure it like a CLAUDE.md section, not a conversational message: numbered steps, explicit commands, clear termination condition. The agent has no human to ask for clarification.

## Nonce lifecycle

If sessions write state, a nonce ties start and end together:

```bash
# session.js start: write nonce, return it
nonce=$(bun scripts/session.js start)

# pass nonce into the prompt so the agent can close cleanly
claude -p --dangerously-skip-permissions \
  "... run session.js end --nonce $nonce when done"
```

The end script can verify no new activity arrived before allowing exit — a clean-shutdown handshake.

## When to use this

Appropriate for agents with a well-defined loop (check → respond → commit → stop), operating on durable external state, with clear termination conditions. Open-ended exploration still benefits from interactive sessions.

---

*Part of the [rhi.zone/cc](https://rhi.zone/cc/) Claude Code foundations. Full guide: [docs.rhi.zone/claude-code-guide](https://docs.rhi.zone/claude-code-guide)*
