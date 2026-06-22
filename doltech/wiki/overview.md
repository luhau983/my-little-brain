---
title: Overview
type: overview
tags: [overview, map]
created: 2026-06-22
updated: 2026-06-22
status: active
---

# LittleBrain — Overview

The evolving big picture. Beerus revises this as the KB grows.

## Current focus
EdTech backend: a **[[spring-boot|Spring Boot]] monorepo** ([[study-hub]] et al.) on **[[mongodb|MongoDB]]**,
plus a **[[micronaut|Micronaut]]** default stack. Query design via the [[predicate-pattern|Predicate pattern]]
/ [[querydsl|QueryDSL]] over the [[repository-pattern|Repository pattern]].

## Themes emerging
- **Data access strategy** — dynamic filtering ([[predicate-pattern]] / [[querydsl|QueryDSL]]), MongoDB modeling.
- **Monorepo architecture** — [[spring-boot|Spring Boot]] apps, [[cqrs-command-query|CQRS-lite]], feature-based layout.

## Projects
- [[study-hub]] — EdTech kid-exercise service (Spring Boot 4 / Java 25 / MongoDB).

## Open threads
- Predicate pattern ↔ Micronaut Data MongoDB criteria API specifics.
- Transaction performance on sharded clusters.
