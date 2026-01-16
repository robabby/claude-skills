# remember

Store a memory in Obsidian for cross-session persistence.

## When to Use

- When you learn something important you'll need later
- After making a significant decision
- When discovering a useful pattern or process
- To record facts you don't want to lose

## How It Works

1. Parses the content you provide
2. Classifies the memory type (episodic, semantic, procedural, strategic)
3. Assesses importance (0.0 to 1.0)
4. Extracts searchable concepts
5. Creates a Markdown file in the appropriate folder

## Usage

**Store a decision:**
```
/remember We decided to use Redis for caching because it supports horizontal scaling
```

**Store a fact:**
```
/remember The production API rate limit is 100 requests per minute
```

**Store a pattern:**
```
/remember To fix React hydration errors, use useState + useEffect instead of useMemo with random values
```

**Store an experience:**
```
/remember The debugging session revealed that timeouts were caused by DNS resolution delays
```

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| content | Yes | What to remember (passed after the command) |

## Memory Types

| Type | For | Examples |
|------|-----|----------|
| episodic | Events, experiences | "The session where...", "We hit a wall..." |
| semantic | Facts, knowledge | "The API uses...", "The path is..." |
| procedural | Processes, patterns | "To deploy, run...", "Pattern for..." |
| strategic | Decisions, plans | "We chose X because...", "Next steps..." |

## Importance Scale

- **0.9-1.0**: Critical decisions, core project context
- **0.7-0.8**: Important patterns, significant learnings
- **0.5-0.6**: Useful context, moderate relevance
- **0.3-0.4**: Minor details, low priority

## Example Output

```
Remembered: Redis Caching Decision (type: strategic, importance: 0.85)
Saved to: Areas/AI/Memory/Strategic/2024-01-15 - Redis Caching Decision.md
```

## File Format

The created memory file looks like:

```markdown
---
created: 2024-01-15
type: strategic
importance: 0.85
concepts: [redis, caching, architecture, scaling]
source: explicit
---

# Redis Caching Decision

We decided to use Redis for caching because it supports horizontal scaling.

## Context

This decision enables the application to scale across multiple instances
while maintaining cache consistency.
```

## Related Skills

- [recall](recall.md) - Search for memories you've stored
- [reflect](reflect.md) - Automatically creates memories at session end
- [glean](glean.md) - Surface patterns from stored memories
