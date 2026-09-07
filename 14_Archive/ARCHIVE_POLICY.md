# Archive Policy

Archive is an **optional organizational layer**, not a day-one requirement.

For a Git-backed KnowledgeBase, a superseded artifact can often remain in its original folder with:

```text
Status: Superseded
Superseded by: ADR-019
```

and Git history provides the historical trail.

Use `14_Archive/` when historical material becomes large enough to interfere with active navigation
and search.

## Never silently delete load-bearing history

Examples:

- Superseded ADRs
- Old architecture versions
- Migration records
- Incident reports
- Changelog history

## Archive metadata

```yaml
status: historical
replaced_by: ADR-XXX
archived_on: YYYY-MM-DD
reason: "..."
```
