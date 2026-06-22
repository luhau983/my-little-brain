---
title: "Query strategy: Micronaut Data on MongoDB"
type: synthesis
tags: [micronaut, mongodb, query, data-access]
created: 2026-06-22
updated: 2026-06-22
status: active
sources: ["[[src-2026-06-22-micronaut-data-mongodb]]"]
---

# Query strategy: Micronaut Data on MongoDB

> Filed from a QUERY on 2026-06-22: *"What query strategies do we know for Micronaut Data on MongoDB?"*

## Answer
[[micronaut|Micronaut]] Data resolves queries at **compile time** (AOT) — no runtime ORM overhead,
errors caught at build (per [[src-2026-06-22-micronaut-data-mongodb]]). Two complementary strategies:

1. **Static finders** via the [[repository-pattern|Repository pattern]] — name-derived methods on a
   `@MongoRepository` interface (e.g. `findByNameAndActiveTrue`). Best when the filter shape is fixed.
2. **Dynamic filtering** via the [[predicate-pattern|Predicate pattern]] — build a composable
   `Predicate` at runtime; each optional filter adds-or-skips a constraint, composed with AND/OR.
   Use when filters depend on optional input, to avoid the combinatorial explosion of named finders.

**Rule of thumb:** fixed filter → finder; optional/variable filters → predicate.

## Open threads
- How the Predicate pattern maps onto Micronaut Data's MongoDB criteria API specifically.
- Transaction behavior ([[mongodb|MongoDB]] multi-doc ACID since v4.0 / v4.2) under read-heavy load.

## Sources
- [[src-2026-06-22-micronaut-data-mongodb]]
