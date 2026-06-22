---
title: Repository Pattern
type: concept
tags: [data-access, design-pattern, abstraction]
created: 2026-06-22
updated: 2026-06-22
status: stub
source_count: 1
sources: ["[[src-2026-06-22-micronaut-data-mongodb]]"]
---

# Repository Pattern

Abstraction over data access: callers depend on a repository interface, not the datastore. In
[[micronaut|Micronaut]] Data the implementation is **generated at compile time** from the interface
(`@MongoRepository` for [[mongodb|MongoDB]]). Pairs with the [[predicate-pattern]] for dynamic queries.

## Sources
- [[src-2026-06-22-micronaut-data-mongodb]]
