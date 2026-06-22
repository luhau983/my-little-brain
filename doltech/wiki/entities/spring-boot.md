---
title: Spring Boot
type: entity
entity_type: framework
tags: [jvm, framework, spring]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-study-hub-codebase]]"]
---

# Spring Boot

JVM application framework. Powers the doltech **`spring-monorepo`** applications (e.g. [[study-hub]])
on **Spring Boot 4.0.0 / Java 25** with Spring Cloud, built by Gradle via a shared
`common-application.gradle`.

## At doltech
- Apps enable a stack of custom starters: `@EnableDolKafka(/V2)`, `@EnableDolJetCache`,
  `@EnableDolExceptionHandler`, `@EnableMongoRepositories`, `@EnableFeignClients`, `@EnableRetry`.
- Auth is **JWT-only** (`java-jwt`) — no Spring Security.
- Data via spring-data-mongodb + [[querydsl|QueryDSL]]; see [[study-hub]] for the reference layout
  ([[cqrs-command-query|CQRS-lite]], feature-based).
- Note: doltech also has a **[[micronaut|Micronaut]]** default stack — both JVM frameworks coexist.

## Related
[[study-hub]] · [[mongodb]] · [[querydsl]] · [[cqrs-command-query]] · [[micronaut]]

## Sources
- [[src-2026-06-22-study-hub-codebase]]
