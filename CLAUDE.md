# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A public Claude Code plugin marketplace: a collection of shareable skills packaged as plugins, distributed via `.claude-plugin/marketplace.json`. There is no build, lint, or test tooling — content is markdown (`SKILL.md`) and JSON manifests, validated by structure/convention rather than a compiler.

## Repo structure

```
.claude-plugin/marketplace.json       # marketplace manifest — lists every plugin and its source path
plugins/<name>/.claude-plugin/plugin.json   # plugin manifest (name, description, version, author)
plugins/<name>/skills/<name>/SKILL.md       # the skill's instructions (this is the actual content)
```

Each plugin currently contains exactly one skill named the same as the plugin.

## Adding a new skill/plugin

1. `mkdir -p plugins/<name>/.claude-plugin plugins/<name>/skills/<name>`
2. Add `plugins/<name>/.claude-plugin/plugin.json` (mirror an existing plugin's shape: `name`, `description`, `version`, `author`)
3. Add `plugins/<name>/skills/<name>/SKILL.md` with YAML frontmatter (`description:`) followed by the skill instructions
4. Add an entry to `.claude-plugin/marketplace.json` under `plugins`: `{ "name": "<name>", "source": "./plugins/<name>" }`

## Versioning

Bump the `version` in a plugin's `plugin.json` when its `SKILL.md` changes meaningfully — installed users only pick up updates via `claude plugin marketplace update claude-skills` followed by `claude plugin update <name>` (requires a session restart).

## Memory & error tracking

This repo tracks its own memory and error log in-repo instead of the global `~/.claude/.../memory/` auto-memory system:
- `MEMORY.md` — durable facts about the user, feedback on working style, project context, and references. Write here instead of the home-directory memory store when working in this repo.
- `ERRORS.md` — defects found in skills/code and notable runtime failures, so they aren't silently rediscovered.
