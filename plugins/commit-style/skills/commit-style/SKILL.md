---
description: Check the user's global ~/.claude/CLAUDE.md for a commit message style rule and add one if missing. Use when the user asks to set up commit message conventions, wants their commit style installed on a new machine, or bootstrap commit formatting rules.
---

# Commit Style Skill

Make sure the user's global `~/.claude/CLAUDE.md` has a rule defining commit message style, so it travels with them to any machine where this plugin is installed, instead of relying on manually copying that file.

## Steps

### 1. Check `~/.claude/CLAUDE.md` for an existing rule

Look for a section covering commit message format (e.g. `## Git commit messages` or equivalent). If one already exists, skip to step 4 and report it as already present — don't duplicate or overwrite it.

### 2. If missing, confirm before editing

`~/.claude/CLAUDE.md` is a global, cross-project file — ask the user before editing it. Ask what commit style they want, or offer this default and let them accept or edit it:

```markdown
## Git commit messages

Lowercase, no period, short imperative summary line. Bullet points for details, also lowercase and terse. Example:

\```
added draft schema

- renamed schema to match topic names
- reworked user event document
\```
```

### 3. Add the confirmed rule

Append it to `~/.claude/CLAUDE.md` once the user has confirmed the wording.

### 4. Confirm

Summarize whether the rule was added, already present, or skipped.
