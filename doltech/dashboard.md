# doltech — Dashboard

> Live views over page frontmatter (needs the **Dataview** plugin enabled in Obsidian).
> (← [front door](../index.md) · [catalog](index.md))

## All pages by type
```dataview
TABLE type, status, source_count AS sources, updated
FROM "doltech/wiki"
WHERE type
SORT type ASC, updated DESC
```

## Stubs needing work
```dataview
LIST
FROM "doltech/wiki"
WHERE status = "stub"
```

## Recently updated
```dataview
TABLE updated, type, status
FROM "doltech/wiki"
WHERE type
SORT updated DESC
LIMIT 10
```

## Sources by ingest date
```dataview
TABLE source_type, author, ingested
FROM "doltech/wiki/sources"
SORT ingested DESC
```
