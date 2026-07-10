# claude-skills

Public marketplace of generic, shareable Claude Code skills.

## Add this marketplace

```
/plugin marketplace add lmeadors/claude-skills
```

## Install a plugin

```
/plugin install project-memory@claude-skills
```

## Add a new skill

1. `mkdir -p plugins/<name>/.claude-plugin plugins/<name>/skills/<name>`
2. Add `plugins/<name>/.claude-plugin/plugin.json`
3. Add `plugins/<name>/skills/<name>/SKILL.md`
4. Add an entry to `.claude-plugin/marketplace.json`
