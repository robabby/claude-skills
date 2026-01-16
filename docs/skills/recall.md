# recall

Search Obsidian memories by keyword and concept.

## When to Use

- When you need to find past context about a topic
- Before making a decision that might have prior context
- To check if you've already solved a similar problem
- When you remember storing something but need to retrieve it

## How It Works

1. Parses your search query
2. Searches memory file content for matching terms
3. Searches frontmatter concepts for matching terms
4. Optionally filters by memory type
5. Sorts results by importance
6. Presents top matches with summaries

## Usage

**General search:**
```
/recall deployment
```
Finds all memories mentioning deployment.

**Multi-term search:**
```
/recall redis caching decision
```
Finds memories matching multiple terms.

**Type-filtered search:**
```
/recall deployment procedural
```
Finds only procedural memories about deployment.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| query | Yes | Search terms |
| type | No | Filter: episodic, semantic, procedural, strategic |

## Search Strategies

The skill uses multiple search approaches:

```
# Content search - finds terms in memory body
Grep pattern="deployment" path="<vault>/Areas/AI/Memory"

# Concept search - finds terms in frontmatter
Grep pattern="concepts:.*deployment" path="<vault>/Areas/AI/Memory"

# Type-filtered - searches specific folder
Grep pattern="deployment" path="<vault>/Areas/AI/Memory/Procedural"
```

## Example Output

```
Found 4 memories about "deployment":

1. **Deployment Process for Production** (procedural, importance: 0.8)
   Steps: build, test, push to main, wait for CI, verify in staging...

2. **Blue-Green Deployment Decision** (strategic, importance: 0.75)
   We chose blue-green over rolling updates for zero-downtime...

3. **Deployment Timeout Fix** (episodic, importance: 0.6)
   Session where we debugged the 30-second timeout issue...

Would you like me to read any of these in full?
```

## Search Tips

- Use specific terms you'd naturally search for
- Include project names for targeted results
- Add memory type to narrow results
- Try synonyms if first search is empty

## Related Skills

- [remember](remember.md) - Store memories to search later
- [hydrate](hydrate.md) - Automatically loads relevant memories at session start
- [glean](glean.md) - Surface patterns rather than specific memories
