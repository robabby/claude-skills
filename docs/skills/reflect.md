# reflect

End-of-session reflection and memory consolidation.

## When to Use

- At the end of a work session
- After completing a significant piece of work
- Before a break when you want to preserve context
- When you've made decisions worth remembering

## How It Works

1. Reviews what happened during the session
2. Identifies memories worth preserving
3. Classifies each memory by type and importance
4. Creates memory files in appropriate folders
5. Optionally updates living context documents
6. Summarizes what was captured

## Usage

**Full session reflection:**
```
/reflect
```
Reviews the entire session and captures key learnings.

**Focused reflection:**
```
/reflect authentication work
```
Focuses reflection on a specific area.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| focus | No | Area to focus reflection on |

## What Gets Captured

**Always capture:**
- Decisions and their rationale
- Discovered patterns or processes
- Project context that took time to establish
- Unfinished work and next steps

**Consider capturing:**
- Interesting technical details
- User preferences observed
- Problems encountered and solutions found

**Skip:**
- Routine operations with no novel learning
- Information already well-documented elsewhere
- Transient details unlikely to matter later

## Example Output

```
Reflecting on this session...

We worked on: API migration and caching implementation

Key memories to store:
1. **Strategic**: Redis caching decision for horizontal scaling
2. **Procedural**: Cache invalidation pattern using pub/sub
3. **Semantic**: Production cache TTL is 5 minutes
4. **Episodic**: Cache stampede issue and fix

Creating 4 memories...
-> Areas/AI/Memory/Strategic/2024-01-15 - Redis Caching Decision.md
-> Areas/AI/Memory/Procedural/2024-01-15 - Cache Invalidation Pattern.md
-> Areas/AI/Memory/Semantic/2024-01-15 - Production Cache TTL.md
-> Areas/AI/Memory/Episodic/2024-01-15 - Cache Stampede Fix.md

Updated Current State.md with new priority: monitoring setup.

Session context preserved. 4 memories stored.
```

## Reflection Prompts

The skill considers:
- What would I want to know starting fresh on this topic?
- What mistakes shouldn't be repeated?
- What worked well?
- What context would be lost if not stored?

## Related Skills

- [hydrate](hydrate.md) - The counterpart; loads context at session start
- [remember](remember.md) - Store individual memories during the session
- [pickup](pickup.md) - For immediate context handoff (vs. long-term storage)
