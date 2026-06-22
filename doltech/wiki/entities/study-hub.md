---
title: study-hub
type: entity
entity_type: project
tags: [project, doltech, edtech, spring-boot, mongodb]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-study-hub-codebase]]"]
---

# study-hub

EdTech learning-content service in the DolEnglish platform. Owns **kid-track exercises** — content
CRUD + test-taking — with scaffolding for IELTS AI exercises, vocab, and YLE (not yet implemented).
One application in the doltech **`spring-monorepo`**. (Per [[src-2026-06-22-study-hub-codebase]].)

## Stack & versions
- **Java 25**, **Spring Boot 4.0.0**, Spring Cloud 2025.1.0-RC1; built with **Gradle** (inherits
  `gradle/common-application.gradle` from the monorepo).
- **[[mongodb|MongoDB]]** via spring-data-mongodb 4.2.5; **[[querydsl|QueryDSL]]** 5.1.0 for type-safe queries.
- **MapStruct** (mapping), **Lombok** (`@SuperBuilder`, never `@Data`), **JetCache** on Redis/Dragonfly,
  **Kafka/Redpanda** (events), **Restate** (async workflows).
- **Auth: JWT only** (`java-jwt`) — no Spring Security.

## Architecture
Feature-based + [[cqrs-command-query|CQRS-lite]]: each feature splits into command vs query
controllers/services/handlers. Layout: `features/<area>/{common,entry,dotest}/{controller,service,
persistence,dto}`. Live code is under `kid/exercise/` (common + `entry` CRUD + `dotest` test-taking)
and `shared/` (TTS, helpers); `kid/vocab`, `kid/yle`, `ielts/exercise_ai` are scaffolded-empty.

## Data access
- Repositories extend `EditableDocumentRepository<E>` or `MongoQueryDSLRepository<E>`.
- Dynamic filtering via **static PredicateBuilder** classes (e.g. `KidExercisePredicateBuilder`) —
  the doltech flavor of the [[predicate-pattern|Predicate pattern]] (static, **not** `@Component`).
- Core entity `KidExercise` (`@Document("kid_exercise")`) extends `BaseEditingDocument` with a
  draft → editing → published lifecycle; polymorphic `ExercisePage` / question subtypes (5 types).

## Conventions (project-specific)
- **Controllers:** command controller extends `ValidatorController<XxxValidator>` + injects the
  `*ServiceCommand` **interface** (never the handler impl); query controller is a plain `@RestController`.
- **Errors:** throw `BusinessLogicException` (never return error DTOs); global `CusExceptionHandler`
  renders the envelope; error codes are enums.
- **Mapping:** MapStruct (`componentModel="spring"`); polymorphic mapping via a **MapperFactory +
  CanHandleMapping** registry — no parallel switch/if-else.
- **Concurrency:** `DistributedLockService.buildKey(...)` → `runWithLock(...)` for concurrent commands.
- **Caching:** JetCache `@Cached` (REMOTE); invalidate from the command path on staleness.
- ⚠️ Legacy package misspelling `excercise` is load-bearing — **do not rename**.

## Gotchas / footguns
- **No DB migration tool** (no Mongock/Flyway). Renaming a field silently breaks old docs — write a
  backfill under `scripts/`.
- **QueryDSL Q-classes regenerate at `compileJava`** — after entity field changes run `clean :compileJava`,
  else stale `QXxx` is reused silently.
- **Indexes auto-created on startup** from `@CompoundIndex`/`@Indexed`; removed indexes need a manual `dropIndex()`.
- `application.yml` may carry inline credentials — override via env; real config lives in
  `dol-online-config/configs/study-hub-spring/{dev,prod}.yml`.
- `src/test/java` is empty; fixtures under `src/test/resources/dummy-data/`.

## Integrations
External (Feign/rest-client): course-app-sheet (+sync-job), **Directus** (CMS), document-history,
go-user-service, **Restate**. Brokers: Kafka/Redpanda. Cache: Redis/Dragonfly. Shared monorepo libs:
`shared-model`, `common`, `kafka`/`kafka_v2`, `rest-client`, `course-supporter`, `dol-config`, `restate-client`.

## Related
[[mongodb]] · [[spring-boot]] · [[querydsl]] · [[cqrs-command-query]] · [[predicate-pattern]] · [[repository-pattern]]

## Open questions
- Kafka topics/schemas study-hub produces/consumes.
- Where JWT validation happens (filter/aspect in `libs:common`?).
- Restate workflows beyond TTS.

## Sources
- [[src-2026-06-22-study-hub-codebase]]
