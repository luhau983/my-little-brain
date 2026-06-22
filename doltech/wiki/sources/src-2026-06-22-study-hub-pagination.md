---
title: "study-hub — pagination perf note"
type: source
source_type: transcript
author: Zeno Sama
url: ""
raw_path: raw/transcripts/2026-06-22-study-hub-pagination.md
date_published: 2026-06-22
ingested: 2026-06-22
created: 2026-06-22
updated: 2026-06-22
status: active
tags: [study-hub, mongodb, pagination, performance]
related: ["[[study-hub]]", "[[mongodb]]", "[[keyset-pagination]]"]
---

# study-hub — pagination perf note

## TL;DR
Deep pagination of the [[study-hub]] lesson list was slow because [[mongodb|MongoDB]] `skip/limit`
scans and discards `skip` docs (cost grows with page depth). Fix: [[keyset-pagination|keyset pagination]].

## Key points
- `skip(n).limit(m)` is ≈ O(n) — deep pages degrade.
- Keyset: sort by an indexed field (`_id`/`createdAt`), next page `{_id: {$gt: lastSeenId}}` + limit → constant cost.
- Needs the sort field indexed + a stable tiebreaker.

## Notable claims
- skip/limit cost grows with page depth. *(per this note)*

## Open questions
- Numbered admin tables in study-hub still need offset paging — keep both strategies?

## Links
[[study-hub]] · [[mongodb]] · [[keyset-pagination]]
