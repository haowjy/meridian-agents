---
name: github-issues
description: File and manage backlog items as GitHub Issues. Use instead of markdown backlogs for tracking tech debt, bugs, improvements, and design work.
---

# GitHub Issues

Use GitHub Issues as the single source of truth for backlog tracking.

## When to File vs Fix

- **Fix immediately** if it takes < 5 minutes and you're already in the area
- **File an issue** if it would derail your current task, requires broader context, or needs design discussion

## Labels

Use these labels consistently. Create them if they don't exist.

| Label | Color | When to use |
|-------|-------|-------------|
| `tech-debt` | `#d4c5f9` | Code quality, cleanup, refactoring needs |
| `bug` | `#d73a4a` | Something is broken |
| `improvement` | `#a2eeef` | Enhancement to existing functionality |
| `design` | `#0075ca` | Needs design discussion before implementation |
| `blocked` | `#e4e669` | Waiting on external dependency or another issue |
| `good-first-task` | `#7057ff` | Well-scoped, good for a single spawn |

## Creating Issues

Always include: clear title, what's wrong/needed, relevant file paths, and priority context.

```bash
# Standard issue
gh issue create \
  --title "Short, specific title" \
  --label "tech-debt" \
  --body "$(cat <<'EOF'
## Problem
What's wrong or what's needed.

## Relevant files
- `src/path/to/file.py`

## Notes
Any context that helps someone pick this up later.
EOF
)"

# Quick issue (when context is obvious)
gh issue create \
  --title "Clean up stale helper in module X" \
  --label "tech-debt" \
  --body "Brief description of what and why."
```

## Querying Issues

```bash
# See what's open
gh issue list

# Filter by label
gh issue list --label "tech-debt"
gh issue list --label "bug"

# See details
gh issue view ISSUE_NUMBER

# Search
gh issue list --search "spawn execution"
```

## Closing Issues

Close with a reference to the fixing commit:

```bash
gh issue close ISSUE_NUMBER --comment "Fixed in $(git rev-parse --short HEAD)"
```

Or use `Fixes #N` / `Closes #N` in commit messages for automatic closure.
