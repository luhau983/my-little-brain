---
title: MongoDB
type: entity
entity_type: database
tags: [database, nosql, document-store, bson]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 2
sources: ["[[src-2026-06-22-micronaut-data-mongodb]]", "[[src-2026-06-22-study-hub-codebase]]"]
---

# MongoDB

Document database (BSON). Primary datastore for the EdTech backend. Accessed from [[micronaut]] via
Micronaut Data `@MongoRepository`.

## Transactions
Multi-document **ACID** transactions since v4.0 (replica sets) and v4.2 (sharded clusters).

## Data modeling
- **Embed** when data is read together; **reference** when it grows unbounded.
- Model around access patterns; index aggressively for read-heavy workloads.

## At doltech
- Used by [[study-hub]] via spring-data-mongodb + [[querydsl|QueryDSL]] (also the [[micronaut|Micronaut]]
  default stack). **No migration tool** — schema-on-write; indexes auto-created from `@CompoundIndex` /
  `@Indexed` on startup, so a removed index needs a manual `dropIndex()` (per [[src-2026-06-22-study-hub-codebase]]).

## Related
[[micronaut]] · [[predicate-pattern]] · [[study-hub]] · [[querydsl]]

## Sources
- [[src-2026-06-22-micronaut-data-mongodb]]
- [[src-2026-06-22-study-hub-codebase]]
