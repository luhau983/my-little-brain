---
title: "doltech spring-monorepo — applications survey"
type: source
source_type: codebase
author: doltech
url: ""
raw_path: /home/liuhao/Documents/doltech/spring-monorepo/applications
date_published: 2026-06-22
ingested: 2026-06-22
created: 2026-06-22
updated: 2026-06-22
status: active
tags: [doltech, spring-monorepo, survey, architecture]
related: ["[[spring-boot]]", "[[mongodb]]", "[[cqrs-command-query]]"]
---

# doltech spring-monorepo — applications survey

Batch codebase read of the ~24 applications under
`/home/liuhao/Documents/doltech/spring-monorepo/applications` (2026-06-22), to capture each
sub-project's features in detail. Shared source for all per-app project pages.

## Shared baseline (all apps)
[[spring-boot|Spring Boot]] 4 / Java 25 / Gradle, [[mongodb|MongoDB]] + [[querydsl|QueryDSL]],
MapStruct, JetCache (Redis/Dragonfly), Kafka/Redpanda, Restate, JWT auth, feature-based +
[[cqrs-command-query|CQRS-lite]], `BusinessLogicException` + global `CusExceptionHandler`,
`EditableDocument` draft→published lifecycle, static PredicateBuilders.

## Apps covered (project pages)
[[action-history]] · [[billing]] · [[ev-dictionary]] · [[g12]] · [[grammar]] · [[hsa]] · [[junior]] ·
[[k10]] · [[study-hub]] — (more in follow-up batches).

## Note
Per-app pages are bilingual (English section first, Vietnamese below). Feature detail is distilled
from each app's controllers/services/entities; exact endpoint lists live in the project pages.
