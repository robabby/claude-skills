# glean

Surface emergent patterns and insights from memory.

## When to Use

- When you want to see connections across your work
- During planning or strategy sessions
- When something feels significant but you can't articulate it
- Periodically, to discover patterns you might have missed

## How It Works

1. Gathers recent memories (10-15 files)
2. Reads recent session logs (3-5 files)
3. Optionally reads Current State for situational context
4. Reflects on what patterns or insights are emerging
5. Shares findings in freeform prose

## Usage

**General gleaning:**
```
/glean
```
Surfaces patterns from recent context.

**Focused gleaning:**
```
/glean career decisions
```
Focuses on patterns related to a specific area.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| focus | No | Area to focus pattern discovery on |

## Principles

- **Reflection, not retrieval.** Not summarizing memories—noticing what patterns are forming.
- **Genuine over performative.** Only shares what's actually emerging.
- **No automatic storage.** Insights can lead to `/remember`, but that's separate.
- **Freeform expression.** Output shape matches what's emerging.

## Example Output

```
Looking across recent memories and sessions...

There's a thread I'm noticing: the vault work, the API migration, and
the caching decisions all connect to the same underlying theme—reducing
complexity and external dependencies.

The Redis decision wasn't just about scaling; it was about having one
well-understood tool instead of multiple partial solutions. The API
migration is consolidating three endpoints into one. The vault
reorganization is about making implicit knowledge explicit.

There's a pattern of simplification and consolidation emerging across
different domains.
```

## When Nothing Emerges

If no genuine pattern is surfacing, the skill will say so:

```
Nothing's particularly surfacing right now. The recent work has been
fairly routine—no strong patterns or connections jumping out.
```

This is a valid response. The skill doesn't fabricate insight.

## Related Skills

- [recall](recall.md) - Search for specific memories (retrieval vs. reflection)
- [reflect](reflect.md) - Captures learnings; glean surfaces patterns from them
- [hydrate](hydrate.md) - Loads context; glean interprets it
