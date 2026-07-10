# claude-skills

Public marketplace of generic, shareable Claude Code skills.

## Add this marketplace

In a Claude Code session:
```
/plugin marketplace add lmeadors/claude-skills
```

From a terminal:
```
claude plugin marketplace add lmeadors/claude-skills
```

## Install a plugin

In a Claude Code session:
```
/plugin install project-memory@claude-skills
```

From a terminal:
```
claude plugin install project-memory@claude-skills
```

## Update

Pull the latest plugin manifests from this marketplace:
```
claude plugin marketplace update claude-skills
```

Then update an installed plugin to the latest version (requires a session restart to apply):
```
claude plugin update project-memory
```

## Add a new skill

1. `mkdir -p plugins/<name>/.claude-plugin plugins/<name>/skills/<name>`
2. Add `plugins/<name>/.claude-plugin/plugin.json`
3. Add `plugins/<name>/skills/<name>/SKILL.md`
4. Add an entry to `.claude-plugin/marketplace.json`
