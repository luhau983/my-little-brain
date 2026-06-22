---
title: "Micronaut Data + MongoDB: Repositories & Predicates"
type: source
source_type: article
author: unknown
url: ""
raw_path: raw/articles/micronaut-data-mongodb.md
date_published: ""
ingested: 2026-06-22
created: 2026-06-22
updated: 2026-06-22
status: active
tags: [micronaut, mongodb, data-access, query, jvm]
related: ["[[micronaut]]", "[[mongodb]]", "[[predicate-pattern]]", "[[repository-pattern]]"]
---

# Micronaut Data + MongoDB: Repositories & Predicates

## TL;DR
[[micronaut|Micronaut]] Data compiles queries at build time (AOT) — no runtime ORM overhead, errors
caught at compile. For dynamic optional-filter queries, the [[predicate-pattern|Predicate pattern]]
beats name-derived finder methods, which explode combinatorially.

## Key points
- `@MongoRepository` interfaces; Micronaut Data generates the impl ([[repository-pattern|Repository pattern]]).
- Name-derived finders (`findByNameAndActiveTrue`) are resolved at **compile time**.
- Dynamic queries → build a composable `Predicate` at runtime; each optional filter is a small,
  testable, skippable function; compose with AND/OR.
- [[mongodb|MongoDB]] multi-document ACID transactions since v4.0 (replica sets) / v4.2 (sharded).
- Modeling: embed when read together, reference when unbounded; index aggressively for read-heavy
  EdTech workloads.

## Notable claims
- AOT compile-time query generation removes runtime translation overhead. *(per this source)*

## Open questions
- How does the Predicate pattern map onto Micronaut Data's MongoDB criteria API specifically?
- Transaction performance characteristics on sharded clusters for our workload?

## Links
[[micronaut]] · [[mongodb]] · [[predicate-pattern]] · [[repository-pattern]]
