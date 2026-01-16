# Claude Memory Skills

A cross-session memory system for Claude Code, built on Obsidian.

## What This Is

Six custom Claude Code skills that give Claude persistent memory across sessions using your Obsidian vault as storage. Instead of starting fresh each conversation, Claude can remember decisions, patterns, and context from previous work.

The system uses Markdown files with YAML frontmatter, making memories human-readable, searchable, and portable.

## Skills Included

| Skill | Purpose |
|-------|---------|
| **hydrate** | Load context from Obsidian at session start |
| **remember** | Store a memory for cross-session persistence |
| **recall** | Search memories by keyword and concept |
| **reflect** | End-of-session reflection and memory consolidation |
| **glean** | Surface emergent patterns and insights |
| **pickup** | Generate context handoff prompt before clearing sessions |

## Prerequisites

1. **Obsidian** - [obsidian.md](https://obsidian.md/)
2. **Obsidian MCP Server** - Enables Claude Code to read/write to your vault
   - See [Obsidian MCP setup](https://github.com/smithery-ai/mcp-obsidian)

## Installation

1. Clone or download this repository:
   ```bash
   git clone https://github.com/yourusername/claude-skills.git
   ```

2. Copy the skills to your Claude Code skills directory:
   ```bash
   cp -r claude-skills/skills/* ~/.claude/skills/
   ```

3. Configure your Obsidian vault path in the skill files (replace `<vault>` placeholders)

4. Verify skills are available:
   ```bash
   claude
   # Then type /hydrate to test
   ```

See [Installation Guide](docs/installation.md) for detailed setup instructions.

## Quick Start

**Starting a session:**
```
/hydrate
```
Loads your current state, recent memories, and session context.

**Remembering something important:**
```
/remember We decided to use Redis for caching because it supports pub/sub
```
Stores a strategic memory with type classification and importance rating.

**Finding past context:**
```
/recall deployment process
```
Searches memories for relevant information.

**Ending a session:**
```
/reflect
```
Captures session learnings and consolidates important context.

**Session handoff (before /clear):**
```
/pickup
```
Generates a prompt you can paste into a new session to resume work.

## Documentation

- [Installation Guide](docs/installation.md) - Detailed setup instructions
- [Memory System](docs/memory-system.md) - How the memory architecture works

### Skill Documentation

- [hydrate](docs/skills/hydrate.md) - Session startup
- [remember](docs/skills/remember.md) - Storing memories
- [recall](docs/skills/recall.md) - Searching memories
- [reflect](docs/skills/reflect.md) - Session reflection
- [glean](docs/skills/glean.md) - Pattern discovery
- [pickup](docs/skills/pickup.md) - Session handoff

## Memory Types

The system classifies memories into four types:

- **Episodic**: Events and experiences ("The session where we debugged the auth issue")
- **Semantic**: Facts and knowledge ("The API endpoint is /v2/users")
- **Procedural**: Processes and patterns ("To deploy, run npm build then...")
- **Strategic**: Decisions and plans ("We chose PostgreSQL because...")

## Vault Structure

The skills expect this structure in your Obsidian vault:

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

## License

MIT License - see [LICENSE](LICENSE)
