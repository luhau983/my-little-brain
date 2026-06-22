# doltech — Index

> Work / engineering knowledge catalog. Beerus updates this on every doltech ingest.
> Navigation: read this, then drill into pages. (← [front door](../index.md) · 📊 [dashboard](dashboard.md))

## Overview
- [Overview](wiki/overview.md) — the evolving big picture of doltech engineering knowledge.

## Sources
- [[src-2026-06-22-micronaut-data-mongodb|Micronaut Data + MongoDB: Repositories & Predicates]]
  — 2026-06-22 · article · repository + predicate patterns on Micronaut Data MongoDB.
- [[src-2026-06-22-study-hub-pagination|study-hub — pagination perf note]]
  — 2026-06-22 · note · skip/limit deep-page slowness → keyset pagination.

## Entities
- [[micronaut|Micronaut]] — JVM framework (AOT/DI) used for the EdTech backend. (1 source)
- [[mongodb|MongoDB]] — document database; primary datastore. (2 sources)
- [[study-hub|study-hub]] — EdTech lesson-delivery backend (Java 17 / Micronaut / MongoDB). (1 source)

## Concepts
- [[predicate-pattern|Predicate Pattern]] — composable, type-safe query building. (1 source)
- [[repository-pattern|Repository Pattern]] — abstraction over data access. (1 source)
- [[keyset-pagination|Keyset Pagination]] — range-based paging; beats skip/limit on deep pages. (1 source)

## Decisions
_(none yet)_

## Syntheses
- [[micronaut-mongodb-query-strategy|Query strategy: Micronaut Data on MongoDB]] — finders vs predicates;
  when to use which. (filed from a query, 2026-06-22)

## Templates
- [Project page template](wiki/entities/_template-project.md) — copy to `wiki/entities/<project>.md`
  to capture what's special about working with a doltech project (stack, conventions, gotchas, decisions).
- [ADR template](wiki/decisions/_template-adr.md) — copy to `wiki/decisions/adr-NNNN-<slug>.md` to record
  an architecture decision (context, decision, consequences with "who pays the cost", alternatives).
