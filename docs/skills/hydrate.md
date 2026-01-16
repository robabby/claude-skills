# hydrate

Load context from the Obsidian memory system at session start.

## When to Use

- At the beginning of every Claude Code session
- When starting work on a specific project or topic
- After a break to refresh context

## How It Works

1. Reads living context documents (Current State, Decision Register)
2. If given a topic, searches for relevant memories
3. If no topic, loads recent memories and session logs
4. Internalizes context without reciting it back
5. Acknowledges briefly what was loaded

## Usage

**Basic session start:**
```
/hydrate
```
Loads current state, recent memories, and recent sessions.

**Topic-focused:**
```
/hydrate metatron
```
Loads current state plus memories related to "metatron".

**Project-specific:**
```
/hydrate authentication
```
Loads context relevant to authentication work.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| topic | No | Focus area for memory search |

## What Gets Loaded

| Source | Purpose |
|--------|---------|
| Current State.md | Your situation, priorities, blockers |
| Decision Register.md | Pending and recent decisions |
| Memories | Relevant or recent cross-session knowledge |
| Sessions | Recent session logs for continuity |

## Example Output

```
Loaded context: Current State shows product v2.0 as primary focus.
8 recent memories loaded including Redis caching decision.
Last session covered API migration work. Ready.
```

## Related Skills

- [reflect](reflect.md) - The counterpart to hydrate; captures context at session end
- [recall](recall.md) - Search memories during a session
- [pickup](pickup.md) - For context handoff when clearing sessions
