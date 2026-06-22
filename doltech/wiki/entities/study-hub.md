---
title: study-hub
type: entity
entity_type: project
tags: [project, doltech, edtech]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-study-hub-pagination]]"]
---

# study-hub

> ⚠️ Example page from a demo ingest — stack inferred from the default doltech stack; replace the
> project-specific TODOs with real values.

EdTech lesson-delivery backend. Part of the doltech stack.

## Stack & versions
- Java 17 / [[micronaut|Micronaut]]
- Datastore: [[mongodb|MongoDB]]

## Conventions (project-specific)
- _(TODO: real conventions)_

## Gotchas / footguns
- **Deep pagination is slow with `skip/limit`** — use [[keyset-pagination|keyset pagination]] on an
  indexed sort field instead (per [[src-2026-06-22-study-hub-pagination]]).

## Key decisions
- _(none yet — record as ADRs in `wiki/decisions/`)_

## Ownership / people
- _(TODO)_

## Related
[[micronaut]] · [[mongodb]] · [[keyset-pagination]]

## Sources
- [[src-2026-06-22-study-hub-pagination]]
