---
title: Predicate Pattern
type: concept
tags: [query, design-pattern, type-safety, composition]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-micronaut-data-mongodb]]"]
---

# Predicate Pattern

A way to build **dynamic, composable queries** at runtime instead of enumerating every filter
combination as a named method. Each optional filter is a small, testable function that either adds a
constraint or is skipped; predicates compose with AND/OR.

## Why
Name-derived finder methods (e.g. `findByNameAndActiveTrue`) explode combinatorially when filters are
optional. Predicates collapse that to one composable query path.

## In our stack
Used with [[micronaut|Micronaut]] Data over [[mongodb|MongoDB]]. See also [[repository-pattern]].

## Sources
- [[src-2026-06-22-micronaut-data-mongodb]]
