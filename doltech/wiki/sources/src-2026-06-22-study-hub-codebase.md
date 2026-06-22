---
title: "study-hub — codebase read"
type: source
source_type: codebase
author: doltech
url: ""
raw_path: /home/liuhao/Documents/doltech/spring-monorepo/applications/study-hub
date_published: 2026-06-22
ingested: 2026-06-22
created: 2026-06-22
updated: 2026-06-22
status: active
tags: [study-hub, spring-boot, mongodb, monorepo, architecture]
related: ["[[study-hub]]", "[[spring-boot]]", "[[mongodb]]", "[[querydsl]]", "[[cqrs-command-query]]"]
---

# study-hub — codebase read

Structured read of the [[study-hub]] application in the doltech `spring-monorepo` (2026-06-22).

## TL;DR
[[study-hub]] is a **Spring Boot 4 / Java 25 / [[mongodb|MongoDB]]** EdTech service for kid-track
exercises, using [[cqrs-command-query|CQRS-lite]] + feature-based layout, [[querydsl|QueryDSL]] with
static PredicateBuilders, MapStruct, JetCache, Kafka, and Restate.

## Key points
- Stack: Java 25, Spring Boot 4.0.0, Spring Cloud 2025.1.0-RC1, Gradle (monorepo
  `common-application.gradle`), spring-data-mongodb 4.2.5, [[querydsl|QueryDSL]] 5.1.0, MapStruct 1.6.3,
  Lombok `@SuperBuilder`, JetCache on Redis/Dragonfly, Kafka/Redpanda, Restate, **JWT-only auth**.
- Architecture: feature-based + command/query split. Live code under `kid/exercise/{common,entry,dotest}`
  and `shared/`; `kid/vocab`, `kid/yle`, `ielts/exercise_ai` are scaffolded-empty.
- Data: repos extend `EditableDocumentRepository` / `MongoQueryDSLRepository`; dynamic filters via
  **static PredicateBuilder** classes; `KidExercise` document with draft→editing→published lifecycle
  and polymorphic question subtypes (5 types).
- Conventions: `ValidatorController` + `*ServiceCommand` interface; `BusinessLogicException` +
  global `CusExceptionHandler`; MapStruct MapperFactory registry; `DistributedLockService`; JetCache
  invalidation from the command path.

## Notable claims (project-cited)
- **No DB migration tool** — schema-on-write; indexes auto-created from `@CompoundIndex`/`@Indexed` on startup. (README)
- **QueryDSL Q-classes regenerate at `compileJava`** → run `clean :compileJava` after entity field changes. (README)
- Legacy package misspelling `excercise` is load-bearing — do not rename. (README)

## Open questions
- Kafka topics/schemas study-hub publishes/consumes; where JWT validation happens; Restate workflows beyond TTS.

## Links
[[study-hub]] · [[spring-boot]] · [[mongodb]] · [[querydsl]] · [[cqrs-command-query]] · [[predicate-pattern]]
