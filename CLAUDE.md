# Claude Skills Repository

This repository contains custom Claude Code skills for cross-session memory and vault maintenance using Obsidian.

## Repository Structure

- `skills/` - The actual skill definitions (SKILL.md files)
- `docs/` - User-facing documentation
- `README.md` - Public readme for GitHub

## Skills

| Skill | Purpose |
|-------|---------|
| hydrate | Load context from Obsidian at session start |
| remember | Store a memory for cross-session persistence |
| recall | Search memories by keyword and concept |
| reflect | End-of-session reflection and memory consolidation |
| glean | Surface emergent patterns and insights |
| pickup | Generate context handoff prompt before clearing sessions |
| vault-status | Show vault overview, structure, and recent activity |
| link-check | Find broken wiki-links and orphaned notes |

## Conventions

### Skill File Format

Each skill lives in `skills/{name}/SKILL.md` with YAML frontmatter:

```yaml
---
name: skill-name
description: One-line description for skill discovery
---
```

### Vault Path Placeholder

Skills use `<vault>` as a placeholder for the user's Obsidian vault path. Users replace this during installation.

### Memory Structure

Skills expect this Obsidian vault structure:
```
Areas/AI/
├── Context/
│   ├── Current State.md
│   └── Decision Register.md
├── Memory/
│   ├── Episodic/
│   ├── Semantic/
│   ├── Procedural/
│   └── Strategic/
└── Collaboration/
    └── Sessions/
```

## Development

When modifying skills:
1. Edit the SKILL.md file in `skills/{name}/`
2. Update corresponding docs in `docs/skills/{name}.md` if behavior changes
3. Update `docs/memory-system.md` if the architecture changes
4. Update README.md if adding/removing skills or changing installation
