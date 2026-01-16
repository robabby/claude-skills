# pickup

Generate a context handoff prompt before clearing the session.

## When to Use

- Before running `/clear` to start fresh
- When ending a session but wanting to resume later
- When context is getting long but work is incomplete
- To create a resumption point for another session

## How It Works

1. Reviews the current session
2. Extracts key information: goal, progress, decisions, state, next steps
3. Formats as a structured prompt
4. Outputs in a code block for easy copying

## Usage

```
/pickup
```

No parameters—analyzes the current session automatically.

## Output Format

The skill generates a prompt you can paste into a new session:

```markdown
## Session Pickup

### Goal
[One sentence: what we're trying to accomplish]

### Context
[2-3 sentences: relevant background]

### Progress
- [Completed item 1]
- [Completed item 2]

### Key Decisions
- [Decision]: [Brief rationale]

### Current State
[Immediate situation, what we were doing]

### Next Steps
1. [Immediate next action]
2. [Following action]

### Open Questions
- [Any unresolved questions]
```

## Guidelines

The skill follows these principles:

- **Be specific**: File paths, function names, exact values—not vague descriptions
- **Capture rationale**: For decisions, note WHY, not just what
- **Prioritize recency**: Recent context matters more than early conversation
- **Skip the obvious**: Don't include information Claude would know from codebase
- **Include blockers**: Note anything blocking progress
- **Keep it scannable**: Bullets and short phrases, not paragraphs

## What Gets Included

| Include | Skip |
|---------|------|
| Current task and subtasks | General pleasantries |
| Files modified or key files | Files just briefly mentioned |
| Decisions and rationale | Exploratory dead-ends |
| Blockers or open questions | Resolved issues |
| Next concrete steps | Vague future plans |
| Error messages if debugging | Successful outputs |

## Example Output

```markdown
## Session Pickup

### Goal
Implement Redis caching for the product catalog API.

### Context
Working in the commerce-api repo. Using ioredis client.
Cache invalidation via pub/sub already set up.

### Progress
- Added Redis connection in src/lib/redis.ts
- Implemented cache-aside pattern for getProduct()
- Added TTL of 5 minutes based on data freshness needs

### Key Decisions
- Cache-aside over write-through: simpler, good enough for read-heavy
- 5 minute TTL: balance between freshness and hit rate

### Current State
Working on cache invalidation. Need to publish events
when products are updated.

### Next Steps
1. Add publish call in updateProduct()
2. Add subscriber in cache warming service
3. Write tests for invalidation flow

### Open Questions
- Should we warm cache on startup or lazy-load only?
```

## Pickup vs Reflect

| pickup | reflect |
|--------|---------|
| Immediate context transfer | Long-term memory storage |
| For session handoff | For knowledge persistence |
| Includes in-progress state | Captures completed learnings |
| Paste into new session | Stored in Obsidian vault |

Use both when appropriate: `/reflect` to store learnings, `/pickup` to resume work.

## Related Skills

- [reflect](reflect.md) - Store learnings for long-term (vs. immediate handoff)
- [hydrate](hydrate.md) - Load stored context (pickup is for unstored context)
