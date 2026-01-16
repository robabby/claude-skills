# Installation Guide

## Prerequisites

Before installing these skills, ensure you have:

1. **Claude Code CLI** installed and working
2. **Obsidian** installed with a vault set up
3. **Obsidian MCP Server** configured for Claude Code

## Step 1: Install Obsidian MCP Server

The skills require the Obsidian MCP server to read and write to your vault.

1. Install the MCP server following the official guide:
   - [mcp-obsidian on GitHub](https://github.com/smithery-ai/mcp-obsidian)

2. Configure it in your Claude Code MCP settings (`~/.claude/mcp.json` or similar):
   ```json
   {
     "mcpServers": {
       "obsidian": {
         "command": "npx",
         "args": ["-y", "mcp-obsidian", "/path/to/your/vault"]
       }
     }
   }
   ```

3. Verify it works by starting Claude Code and checking for Obsidian tools.

## Step 2: Download the Skills

Clone the repository:

```bash
git clone https://github.com/robabby/claude-skills.git
cd claude-skills
```

Or download as a ZIP and extract.

## Step 3: Copy Skills to Claude Code

Copy the skills directory contents to your Claude Code skills location:

```bash
cp -r skills/* ~/.claude/skills/
```

This creates:
```
~/.claude/skills/
├── hydrate/
│   └── SKILL.md
├── remember/
│   └── SKILL.md
├── recall/
│   └── SKILL.md
├── reflect/
│   └── SKILL.md
├── glean/
│   └── SKILL.md
└── pickup/
    └── SKILL.md
```

## Step 4: Configure Vault Paths

The skills use `<vault>` as a placeholder for your Obsidian vault path.

Edit each SKILL.md file and replace `<vault>` with your actual vault path:

```bash
# Example: Replace <vault> with /Users/yourname/Documents/MyVault
sed -i '' 's|<vault>|/Users/yourname/Documents/MyVault|g' ~/.claude/skills/*/SKILL.md
```

Or edit manually in each file.

## Step 5: Create Vault Structure

Create the expected directory structure in your Obsidian vault:

```bash
mkdir -p "/path/to/your/vault/Areas/AI/Context"
mkdir -p "/path/to/your/vault/Areas/AI/Memory/Episodic"
mkdir -p "/path/to/your/vault/Areas/AI/Memory/Semantic"
mkdir -p "/path/to/your/vault/Areas/AI/Memory/Procedural"
mkdir -p "/path/to/your/vault/Areas/AI/Memory/Strategic"
mkdir -p "/path/to/your/vault/Areas/AI/Collaboration/Sessions"
```

Create the initial context files:

**Areas/AI/Context/Current State.md:**
```markdown
---
updated: 2024-01-01
---

# Current State

## Situation
[Your current priorities and context]

## Active Projects
- [Project 1]
- [Project 2]

## Blockers
- None currently
```

**Areas/AI/Context/Decision Register.md:**
```markdown
---
updated: 2024-01-01
---

# Decision Register

## Pending Decisions
- None currently

## Recent Decisions
| Date | Decision | Rationale |
|------|----------|-----------|
```

## Step 6: Verify Installation

1. Start Claude Code:
   ```bash
   claude
   ```

2. Test a skill:
   ```
   /hydrate
   ```

3. You should see Claude acknowledge loading context from your vault.

## Troubleshooting

### Skills not appearing

- Ensure skills are in `~/.claude/skills/`
- Check each skill has a `SKILL.md` file
- Restart Claude Code

### MCP server errors

- Verify Obsidian MCP server is configured correctly
- Check the vault path in your MCP config
- Ensure the vault exists and is readable

### Path errors

- Replace all `<vault>` placeholders with your actual vault path
- Use absolute paths, not relative paths
- Ensure paths don't have trailing slashes

## Customization

### Changing the vault structure

If you prefer a different folder structure, edit the paths in each SKILL.md file. The default structure is:

```
Areas/AI/
├── Context/          # Living context documents
├── Memory/           # Classified memories
│   ├── Episodic/
│   ├── Semantic/
│   ├── Procedural/
│   └── Strategic/
└── Collaboration/
    └── Sessions/     # Session logs
```

### Adding more context sources

Edit `hydrate/SKILL.md` to include additional files Claude should read at session start.

### Adjusting memory classification

Edit `remember/SKILL.md` and `reflect/SKILL.md` to change how memories are classified or where they're stored.
