# Ralph Loop Multi-Line Prompt Fix

**Branch:** `fix/ralph-loop-multiline-arguments`
**Issue:** https://github.com/anthropics/claude-code/issues/16934

## Problem

The `ralph-loop` plugin fails when users provide multi-line prompts with error:
```
Command contains newlines that could separate multiple commands
```

This happens because the original command file passes `$ARGUMENTS` directly through a bash auto-execute block. When prompts contain newlines, Claude Code's security check blocks the command.

## Solution

Changed from bash auto-execute to an instructional approach:
- Claude parses arguments directly (no shell involved)
- Creates state file using Write tool
- Added `mkdir -p .claude` to ensure directory exists

## How to Apply Fix Locally

Copy the fixed command file to your cached plugin:

```bash
cp plugins/ralph-loop/commands/ralph-loop.md \
   ~/.claude/plugins/cache/claude-plugins-official/ralph-loop/*/commands/ralph-loop.md
```

## Files Changed

- `plugins/ralph-loop/commands/ralph-loop.md` - Instructional approach instead of `! auto-execute
- `plugins/ralph-loop/scripts/setup-ralph-loop.sh` - Added `--from-file` fallback (backward compat)
