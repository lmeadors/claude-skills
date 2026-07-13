---
name: move-skill
description: Move or copy a Claude Code skill between two locations — a project's loose `.claude/skills/` directory or an existing marketplace's `plugins/<name>/skills/<name>/` — scaffolding plugin.json and marketplace.json entries as needed. Use when the user says "move skill X to Y", "copy skill X into Y", "import skill X into the marketplace", or similar.
---

# Move/Copy Skill

Relocate or duplicate a skill between two locations, each of which can be a loose project skill directory or a packaged marketplace plugin. Scaffold destination plugin/marketplace metadata as needed, then optionally remove the source.

## Steps

1. Ask for the source path and destination path if not supplied.
   - Source: the directory containing the skill's `SKILL.md`, either a project's `.claude/skills/<skill>/` or a marketplace's `plugins/<plugin>/skills/<skill>/`.
   - Destination: the marketplace repo root to copy into (must contain `.claude-plugin/marketplace.json`).
2. Ask whether this is a move (remove from source after confirming) or a copy (leave the source untouched).
3. Read the source SKILL.md. Use the `name` field from its frontmatter as the canonical skill name, falling back to the directory name if there is no frontmatter name.
4. Check whether the source is already a packaged plugin, i.e. it follows the `plugins/<plugin>/skills/<skill>/SKILL.md` layout with a sibling `plugins/<plugin>/.claude-plugin/plugin.json`.
   - If yes, read that plugin.json for its `name`, `description`, and `author` to reuse in the destination instead of asking fresh.
   - If no (a loose project skill with no plugin.json), continue to step 5 to gather that metadata there.
5. List the plugin directories already under `plugins/` in the destination repo and show them to the user. Ask which plugin this skill belongs to, per the structure documented in the destination repo's CLAUDE.md if it has one. Offer to create a new plugin if none fit.
6. If creating a new plugin:
   - Reuse the name/description found in step 4, or ask for a kebab-case plugin name and a one-line description if the source had no plugin.json.
   - Create `plugins/<plugin-name>/.claude-plugin/plugin.json` in the destination, matching the shape of an existing plugin.json there (check whether the destination's convention includes `version`, and whether `author` includes an email).
   - Add a matching entry to the destination's `.claude-plugin/marketplace.json`, mirroring the shape of its existing entries (some marketplaces use bare `name`/`source`, others also carry `description`/`author`/`category` per entry).
7. Check whether `plugins/<plugin-name>/skills/<skill-name>/` already exists in the destination. If it does, ask before overwriting it.
8. Copy the source skill directory into the destination.
9. If this is a move: show the user the exact source path that will be deleted, including the plugin.json and marketplace.json entry if the source was itself a packaged plugin, and ask for explicit confirmation before removing anything. On confirmation, delete it. Do not remove parent directories that hold other content.
10. Report what was added to the destination, what plugin.json/marketplace.json entries were created or changed, and, for a move, what was removed from the source. Remind the user to verify the skill in a real Claude Code session.
