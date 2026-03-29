# Multi-repo orchestration

When a change spans multiple repositories — updating a convention, propagating a rename, syncing docs — git status is the first thing to check, not the last.

## The pattern

```bash
# before touching any repo
git -C ~/path/to/repo status --short

# clean → make changes directly
# dirty → add to that repo's TODO.md and defer
```

Don't interleave your changes with existing uncommitted work. For dirty repos, write the task to `TODO.md` and move on. The agent session in that repo will pick it up.

## Scope in commit messages

When a commit touches multiple projects, put the affected project in the scope:

```
docs(normalize,moonlet): update install path after rename
```

Especially useful in an org-level docs repo where commits describe changes that happened elsewhere.

## Enumerate the sync checklist

Docs fall out of sync because updating them requires touching several places and it's easy to stop early. Put the full list in CLAUDE.md — not as a reminder, as a checklist. For a new project: project page, project table, sidebar config, hero features, org profile README. Missing one leaves a dangling reference.

## TODO.md as cross-session handoff

`TODO.md` per repo is the deferred work queue. When a session can't complete work in a repo (dirty tree, blocked dependency), write to `TODO.md` rather than holding it in context or leaving a mental note. The next session in that repo sees it from turn 1.

---

*Part of the [rhi.zone/cc](https://rhi.zone/cc/) Claude Code foundations. Full guide: [docs.rhi.zone/claude-code-guide](https://docs.rhi.zone/claude-code-guide)*
