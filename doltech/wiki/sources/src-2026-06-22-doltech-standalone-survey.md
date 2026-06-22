---
title: "doltech standalone services — survey"
type: source
source_type: codebase
author: doltech
url: ""
raw_path: /home/liuhao/Documents/doltech
date_published: 2026-06-22
ingested: 2026-06-22
created: 2026-06-22
updated: 2026-06-22
status: active
tags: [doltech, standalone-services, survey, architecture]
related: ["[[syllabus-service]]", "[[sat-service]]", "[[vocab-v2]]"]
---

# doltech standalone services — survey

Batch codebase read (2026-06-22) of the **standalone services** living directly under
`/home/liuhao/Documents/doltech/<service>` — separate repos, NOT in `spring-monorepo`. Shared source
for the Tier-2 project pages.

## Key finding: mixed stacks
Unlike the spring-monorepo (uniformly Spring Boot 4 / Java 25), standalone services are **mixed**:
- **Micronaut / Java 17** (parent `dol-parent-v2`): [[sat-service]], [[vocab-v2]], [[syllabus-service]],
  [[course-app-sheet-api]], [[course-app-sheet-sync-job]].
- **Spring Boot 3 / Java 17** (parent `dol-parent` v1.5–1.6, older): [[assignment-service]], [[exercise-v2]],
  [[verify-token]], [[online-test-be]].

Common: MongoDB (+ QueryDSL), CQRS (CommandBus/QueryBus), Kafka (`dol-event`, often disabled by default),
Redis/Dragonfly, AWS S3, Directus, shared `dol-common-*` libs. Several embed plaintext int-env credentials
in `application.yml` (gotcha across the fleet).

## Services covered
[[assignment-service]] · [[sat-service]] · [[vocab-v2]] · [[verify-token]] · [[online-test-be]] ·
[[course-app-sheet-api]] · [[course-app-sheet-sync-job]] · [[offline-course-management]] (+ [[syllabus-service]], [[exercise-v2]] earlier).
