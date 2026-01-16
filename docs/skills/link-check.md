# link-check

Validate wiki-links in an Obsidian vault.

## When to Use

- During vault maintenance and cleanup
- When you suspect broken links exist
- To find orphaned notes that may need attention
- Before archiving or reorganizing content

## How It Works

1. Scans all Markdown files for `[[wiki-links]]`
2. Validates each link resolves to an existing file
3. Identifies orphaned notes (files with no incoming links)
4. Detects ambiguous links (multiple files match)
5. Generates actionable report

## Usage

**Full vault scan:**
```
/link-check
```

**Scan specific folder:**
```
/link-check Projects/Active
```

**Only check for broken links:**
```
/link-check --broken-only
```

**Only find orphaned notes:**
```
/link-check --orphans-only
```

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| folder | No | Limit scan to specific folder |
| --broken-only | No | Only report broken links |
| --orphans-only | No | Only report orphaned notes |

## What It Detects

| Issue | Description | Impact |
|-------|-------------|--------|
| Broken links | Link target doesn't exist | Navigation fails |
| Orphaned notes | No other file links here | Hard to discover |
| Ambiguous links | Multiple files match | Unpredictable resolution |

## Example Output

```
## Link Check Report

### Summary
- Total links: 1,247
- Broken links: 8
- Orphaned notes: 23

### Broken Links
| Source File | Broken Link |
|-------------|-------------|
| `Projects/Active/Website.md` | [[Design System]] |
| `Areas/Career/Resume.md` | [[Portfolio]] |
| `Resources/Books/Atomic Habits.md` | [[Book Notes Template]] |

### Orphaned Notes
Files with no incoming links:
- `Inbox/Quick thought 2024-03-15.md`
- `Resources/Snippets/bash-aliases.md`
- `Archive/Old Project/notes.md`
(20 more in Archive/)

### Recommendations
1. Create `Design System.md` or update link in Website.md
2. Review Inbox/ items for processing or deletion
3. Orphans in Archive/ may be intentional - consider excluding from future checks
```

## Notes

- Works with or without Obsidian MCP (uses Grep/Glob tools)
- Expected orphans are excluded: CLAUDE.md, templates, index files
- Archive folder orphans are often intentional

## Related Skills

- [vault-status](vault-status.md) - Overall vault health overview
