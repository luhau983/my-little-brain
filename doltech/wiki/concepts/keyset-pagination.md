---
title: Keyset Pagination
type: concept
tags: [pagination, performance, mongodb, query]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-study-hub-pagination]]"]
---

# Keyset Pagination

Paginate by a **range filter on an indexed, ordered field** instead of by offset. Fetch the next page
with `WHERE key > lastSeenKey ORDER BY key LIMIT n` (in [[mongodb|MongoDB]]: `{key: {$gt: lastSeenKey}}`).

## Why
Offset paging (`skip(n).limit(m)`) is **≈ O(n)** — the DB scans and discards `n` rows, so deep pages
degrade. Keyset is constant cost regardless of depth.

## Cost / when not to use
- Needs the sort field indexed + a stable tiebreaker (e.g. `_id`).
- Only supports next/prev, **not** jumping to an arbitrary page number — bad for numbered admin
  tables, fine for infinite scroll.

## In our stack
First seen in [[study-hub]] lesson feed. Related: [[mongodb]], [[repository-pattern]].

## Sources
- [[src-2026-06-22-study-hub-pagination]]
