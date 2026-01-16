# vault-status

Show current vault status using Obsidian MCP tools.

## When to Use

- When starting work to orient yourself to the vault
- To check what's changed recently
- For a quick overview of vault structure
- To verify daily note status

## How It Works

1. Lists top-level vault structure with file counts
2. Retrieves recently modified files (last 7 days)
3. Checks today's daily note status
4. Summarizes vault health and activity

## Usage

**Full vault status:**
```
/vault-status
```

**Focus on specific folder:**
```
/vault-status Projects/Active
```

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| folder | No | Specific folder to focus on |

## Requirements

Requires Obsidian MCP server with these tools:
- `obsidian_list_files_in_vault`
- `obsidian_list_files_in_dir`
- `obsidian_get_recent_changes`
- `obsidian_get_periodic_note`

## Example Output

```
## Vault Status

**Total Files**: 847
**Last Modified**: 2 hours ago

### Structure
- Projects/: 124 files (Active: 45, Backlog: 32, Completed: 47)
- Areas/: 203 files
- Resources/: 312 files
- Archive/: 156 files
- Planner/: 52 files

### Recent Activity (7 days)
- `Projects/Active/AI Ready Vault/AI Ready Vault.md` (today)
- `Areas/AI/Memory/Strategic/2025-01-08 - Product Vision.md` (today)
- `Planner/2025/01-January/2025-01-08.md` (today)
- `Areas/Career/Job Search.md` (yesterday)

### Today
- Daily note: Present (`Planner/2025/01-January/2025-01-08.md`)
- 4 files modified today
```

## Related Skills

- [hydrate](hydrate.md) - Load context at session start (complementary)
- [link-check](link-check.md) - Check vault link health
