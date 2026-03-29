# Post-history context injection

CLAUDE.md loads at session start — it's the most diluted position in context by the time you're deep in a conversation. A `UserPromptSubmit` hook can inject text *after* the full conversation history, landing it at the freshest position where it has highest salience.

This is useful for hints that should only fire in specific situations: "before reading a large file, get a structural outline first" — irrelevant most of the time, but exactly right when you need it.

## Minimal setup

Create a hook script at `~/.claude/hooks/context.sh`:

```bash
#!/usr/bin/env bash
# Inject context hints after conversation history.
# The hook receives a JSON payload on stdin; output goes into additionalContext.

# Read the prompt from the hook payload
prompt=$(cat | python3 -c "import sys,json; print(json.load(sys.stdin).get('prompt',''))" 2>/dev/null)

# Add conditional hints
if echo "$prompt" | grep -qiE '\b(read|open|look at|check|explore)\b.*\.(rs|ts|js|py|md)'; then
  echo "Before reading a large file, consider getting a structural outline first if available."
fi
```

Register it in `~/.claude/settings.json`:

```json
{
  "hooks": {
    "UserPromptSubmit": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "~/.claude/hooks/context.sh"
          }
        ]
      }
    ]
  }
}
```

The hook's stdout becomes `additionalContext`, appended after the conversation history in the next turn.

## How it differs from CLAUDE.md

| | CLAUDE.md | Post-history hook |
|---|---|---|
| **Position** | Session start (most diluted) | After full history (freshest) |
| **Content** | Static rules | Dynamic, conditional hints |
| **Runs** | Once at session start | Every prompt |
| **Best for** | Invariants, conventions | Situational nudges |

These complement each other. Static invariants belong in CLAUDE.md. Conditional, situational hints belong in a hook.

## Upgrade path

For more sophisticated matching — hierarchical directory walking, keyword/regex conditions, multiple hint files — see [normalize context](https://docs.rhi.zone/normalize), which is what this approach was designed to grow into.

---

*Part of the [rhi.zone/cc](https://rhi.zone/cc/) Claude Code foundations. Full guide: [docs.rhi.zone/claude-code-guide](https://docs.rhi.zone/claude-code-guide)*
