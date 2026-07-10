---
description: Initialize a project to track memory and errors in-repo (MEMORY.md, ERRORS.md) instead of Claude Code's home-directory auto-memory system. Use when the user asks to set up project-based/project-local/project-specific memory, wants memory and error tracking committed to the repo, or wants to bootstrap MEMORY.md/ERRORS.md for a project.
---

# Project Memory Skill

Set up a project so that durable facts, feedback, and error history are tracked in files inside the repo instead of Claude Code's home-directory auto-memory system (`~/.claude/projects/.../memory/`). This keeps that history visible and version-controlled alongside the code.

## Steps

### 1. Create `MEMORY.md` at the project root

Skip this step if `MEMORY.md` already exists — don't overwrite existing content.

```markdown
# MEMORY.md

Project-local memory for this repo. This replaces the global `~/.claude/.../memory/` store for work done here — write durable facts, feedback, and context to this file (not the home-directory memory system) so they travel with the repo and are visible to anyone reading it.

Keep entries short. Group under the headings below; add a heading if a new category is needed. For feedback/project entries, include a brief **Why:** so future readers can judge whether it still applies.

## User

## Feedback

## Project

## Reference
```

### 2. Create `ERRORS.md` at the project root

Skip this step if `ERRORS.md` already exists.

```markdown
# ERRORS.md

Log of skill defects and runtime failures for this repo, so they aren't silently rediscovered/refixed.

Add an entry when:
- A skill run fails or produces wrong output because of bad input, an edge case, or unexpected data — note what happened and how it was resolved.
- A defect is found in a SKILL.md's own instructions/logic (not a one-off bad input) — note what was wrong and the fix (or link to the commit that fixed it).

Format:

\```
## YYYY-MM-DD — <plugin/skill name>
**What happened:** ...
**Cause:** ...
**Fix/resolution:** ...
\```

Newest entries at the top.
```

### 3. Wire up the project's `CLAUDE.md`

- If the project has a `CLAUDE.md`, add this section (skip if a section covering the same thing already exists):

  ```markdown
  ## Memory & error tracking

  This repo tracks its own memory and error log in-repo instead of the global `~/.claude/.../memory/` auto-memory system:
  - `MEMORY.md` — durable facts about the user, feedback on working style, project context, and references. Write here instead of the home-directory memory store when working in this repo.
  - `ERRORS.md` — defects found in skills/code and notable runtime failures, so they aren't silently rediscovered.
  ```

- If the project has no `CLAUDE.md`, create one containing only that section. Mention to the user that `/init` can be run separately to fill in the rest of the file (build/test commands, architecture).

### 4. Check the user's global `~/.claude/CLAUDE.md`

The project files only take effect if the user's global instructions tell Claude to prefer them. Read `~/.claude/CLAUDE.md` and check whether it already has a rule like:

```markdown
## Memory
- If the current project has a `MEMORY.md` and/or `ERRORS.md` at its repo root, use those instead of the home-directory auto-memory system for that project.
- Only fall back to the home-directory memory system for projects that don't have these files.
```

If an equivalent rule is missing, this is a global, cross-project file — ask the user before editing it. If they agree, add the section (don't duplicate if similar text already exists).

### 5. Confirm

Summarize what was created/changed: which of `MEMORY.md`, `ERRORS.md`, project `CLAUDE.md` were added vs. already present, and whether the global `CLAUDE.md` rule was added, already present, or skipped.
