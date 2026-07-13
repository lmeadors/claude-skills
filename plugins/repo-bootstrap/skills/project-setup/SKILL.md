---
name: project-setup
description: Check for CLAUDE.md in the current git repo root and initialize the project if it is missing, then recommend Claude Code automations. Use when starting work in a new project, or when the user says "set up this project", "initialize this project", or "check project setup".
---

# Project Setup

Check the current git repo for CLAUDE.md and set it up if missing, then analyze the codebase for automation opportunities and produce a prioritized proposal.

## Steps

1. Find the git repo root by running: `git rev-parse --show-toplevel`
2. Check whether `CLAUDE.md` exists at that root path.
3. If CLAUDE.md does NOT exist:
   - Tell the user it is missing and that you are initializing it now.
   - Run the `/init` skill to create CLAUDE.md.
   - After `/init` completes, review the result with the user and incorporate any feedback before moving on.
4. If CLAUDE.md already exists:
   - Tell the user it already exists and show the path.
   - Ask if they want to re-run initialization or skip to automations.
5. Run the `/claude-code-setup:claude-automation-recommender` skill to analyze the codebase.
6. After the recommender completes, create a file named `proposed-claude-changes.md` at the repo root containing:
   - A bullet list summary of all proposed changes at the top.
   - Each recommendation as a titled section below, with effort, benefit, and enough detail to implement later.
   - Sections sorted by value (benefit relative to effort), highest first.
   - Do not implement any of the recommendations; this file is a proposal only.
