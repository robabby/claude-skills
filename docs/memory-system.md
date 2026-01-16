# Memory System Architecture

## Overview

The Claude Memory Skills create a persistent memory system using Obsidian as storage. This allows Claude to maintain context across sessions, remember decisions, and build on previous work.

## Memory Lifecycle

```
┌─────────────────────────────────────────────────────────────┐
│                      SESSION START                          │
│                                                             │
│  /hydrate ──► Load Current State ──► Load Recent Memories   │
│              Load Decision Register    Load Session Logs    │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                      DURING SESSION                         │
│                                                             │
│  /remember ──► Store explicit memories                      │
│  /recall ────► Search past memories                         │
│  /glean ─────► Surface patterns from memory                 │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                      SESSION END                            │
│                                                             │
│  /reflect ──► Review session ──► Store learnings            │
│              Update living context if needed                │
│                                                             │
│  /pickup ───► Generate handoff prompt (optional)            │
└─────────────────────────────────────────────────────────────┘
```

## Memory Types

### Episodic Memory
**What**: Events, experiences, things that happened
**Examples**:
- "The session where we debugged the authentication timeout"
- "We hit a wall trying to integrate with the legacy API"
- "The breakthrough moment when we realized the race condition"

**Storage**: `Areas/AI/Memory/Episodic/`

### Semantic Memory
**What**: Facts, knowledge, definitions
**Examples**:
- "The production API endpoint is api.example.com/v2"
- "Rob prefers Tailwind over styled-components"
- "The database uses PostgreSQL 15"

**Storage**: `Areas/AI/Memory/Semantic/`

### Procedural Memory
**What**: How to do things, patterns, processes
**Examples**:
- "To deploy: run tests, build, push to main, wait for CI"
- "Pattern for handling errors: log, notify, graceful fallback"
- "Fix React hydration errors with useState + useEffect"

**Storage**: `Areas/AI/Memory/Procedural/`

### Strategic Memory
**What**: Decisions, plans, approaches
**Examples**:
- "We chose Redis for caching because it supports pub/sub"
- "Decision: Use TypeScript strict mode for new projects"
- "Next phase focuses on performance optimization"

**Storage**: `Areas/AI/Memory/Strategic/`

## Memory File Format

Each memory is a Markdown file with YAML frontmatter:

```markdown
---
created: 2024-01-15
type: strategic
importance: 0.85
concepts: [caching, redis, architecture, performance]
source: explicit
---

# Redis Caching Decision

We decided to use Redis for the caching layer instead of in-memory caching.

## Context

The application needs to scale horizontally, and in-memory caching would require sticky sessions or cache invalidation complexity. Redis provides:
- Shared cache across instances
- Built-in pub/sub for invalidation
- Persistence options if needed
```

### Frontmatter Fields

| Field | Type | Description |
|-------|------|-------------|
| `created` | date | When the memory was created |
| `type` | string | episodic, semantic, procedural, or strategic |
| `importance` | float | 0.0 to 1.0, used for prioritizing search results |
| `concepts` | list | Keywords for search discovery |
| `source` | string | "explicit" (from /remember) or "session" (from /reflect) |

### Importance Scale

- **0.9-1.0**: Critical decisions, core project context
- **0.7-0.8**: Important patterns, significant learnings
- **0.5-0.6**: Useful context, moderate relevance
- **0.3-0.4**: Minor details, low priority

## Living Context Documents

These files are read at every session start and updated as needed:

### Current State.md
Your current situation, priorities, and blockers. Updated when major changes occur.

```markdown
---
updated: 2024-01-15
---

# Current State

## Situation
Currently focused on shipping v2.0 of the product. Interview prep on hold.

## Active Projects
- Product v2.0 release (primary)
- Documentation overhaul
- Performance monitoring setup

## Priorities
1. Fix critical bug in checkout flow
2. Complete API migration
3. Write release notes

## Blockers
- Waiting on design review for settings page
```

### Decision Register.md
Tracks pending and recent decisions for continuity.

```markdown
---
updated: 2024-01-15
---

# Decision Register

## Pending Decisions
- [ ] Choose monitoring solution (Datadog vs self-hosted)
- [ ] Decide on i18n library

## Recent Decisions
| Date | Decision | Rationale |
|------|----------|-----------|
| 2024-01-14 | Use Redis for caching | Horizontal scaling needs |
| 2024-01-10 | TypeScript strict mode | Catch more bugs at compile time |
```

## How Skills Work Together

### Typical Daily Flow

1. **Start session**: `/hydrate` loads context
2. **Work**: Reference memories naturally, use `/recall` when needed
3. **Store insights**: `/remember` for important realizations
4. **End session**: `/reflect` captures learnings

### Context Handoff

When you need to start fresh (clear context) but preserve work:

1. Run `/pickup` to generate a handoff prompt
2. Copy the generated prompt
3. Clear the session (`/clear`)
4. Paste the prompt to resume

### Pattern Discovery

Periodically run `/glean` to surface:
- Recurring themes across projects
- Emerging patterns in your work
- Connections you might have missed

## Search and Retrieval

### How /recall Works

1. Searches memory file content for query terms
2. Searches frontmatter concepts for query terms
3. Optionally filters by memory type
4. Sorts results by importance
5. Returns top matches with summaries

### Optimizing for Search

When creating memories:
- Choose descriptive, searchable concepts
- Use terminology you'll search for later
- Include project names, technologies, people
- Be specific rather than generic

## Best Practices

### Memory Hygiene
- Don't over-store; focus on genuinely useful context
- Update importance levels if priorities change
- Periodically review and prune outdated memories

### Session Discipline
- Start sessions with `/hydrate` for continuity
- Use `/remember` for important realizations during work
- End sessions with `/reflect` to capture learnings

### Context Quality
- Keep Current State.md accurate and updated
- Record decisions in Decision Register.md
- Link memories to related concepts
