---
title: QueryDSL
type: entity
entity_type: library
tags: [query, type-safety, jvm, data-access]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-study-hub-codebase]]"]
---

# QueryDSL

Type-safe query library (v5.1.0) used in the doltech `spring-monorepo` to build [[mongodb|MongoDB]]
queries. Generates `QXxx` metamodel classes from entities at compile time.

## At doltech ([[study-hub]])
- Enabled via `querydslEnabled = true`; repositories extend `MongoQueryDSLRepository<E>`.
- Dynamic filters built with **static PredicateBuilder** classes — the doltech [[predicate-pattern|Predicate pattern]] flavor.
- ⚠️ Q-classes regenerate at `compileJava` — after changing entity fields run `clean :compileJava`,
  else a stale `QXxx` is silently reused.

## Related
[[study-hub]] · [[mongodb]] · [[predicate-pattern]] · [[spring-boot]]

## Sources
- [[src-2026-06-22-study-hub-codebase]]
