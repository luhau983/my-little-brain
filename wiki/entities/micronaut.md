---
title: Micronaut
type: entity
entity_type: framework
tags: [jvm, framework, dependency-injection, aot]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-micronaut-data-mongodb]]"]
---

# Micronaut

JVM framework with **ahead-of-time (AOT)** compilation for dependency injection and data access —
low memory footprint, fast startup. Our EdTech backend framework of choice (Java 17).

## Data access
**Micronaut Data** generates repository implementations and resolves queries at **compile time**
(no runtime reflection/translation overhead; errors caught at build). MongoDB support via
`@MongoRepository`. See [[repository-pattern]] and [[predicate-pattern]] for query strategies.

## Related
[[mongodb]] · [[repository-pattern]] · [[predicate-pattern]]

## Sources
- [[src-2026-06-22-micronaut-data-mongodb]]
