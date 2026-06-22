---
title: dol shared libraries (dol-parent-v2_2)
type: entity
entity_type: library
tags: [doltech, shared-libs, framework, dol-parent]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-tier3-survey]]"]
---

# dol shared libraries (dol-parent-v2_2)

## English

**One-liner.** The **35 shared Maven modules** (parent `dol-parent-v2_2`) every doltech backend depends on —
effectively the in-house "framework" that defines the fleet-wide conventions.

**`dol-common-*` — framework & models.**
- Framework: `dol-common` (base exceptions/utils/HTTP), `dol-common-cqrs` (CommandBus/QueryBus — the [[cqrs-command-query|CQRS-lite]] core),
  `dol-common-kafka`, `dol-common-user` (identity, `RequestUtils`), `dol-common-jackson`, `dol-common-mapper`(+`-processor`) (MapStruct),
  `dol-common-rest-client` (Feign), `dol-common-partial-update`, `dol-common-sentry`, `dol-common-gcip`.
- Shared models: `dol-common-model`, `dol-common-model-{assignment,coursesheet,hubspot,test}`, `dol-common-marking-form`,
  `dol-common-question-{multiple-choice,quiz-test}`.

**`dol-component-*` — infra components.**
- Data: `dol-component-mongodb`(+`-data-processor`) ([[mongodb|MongoDB]] + [[querydsl|QueryDSL]]),
  `dol-component-editable-document` (draft→published lifecycle + versioning — used fleet-wide),
  `dol-component-track-user-edit-document`, `dol-component-custom-view`, `dol-component-jpa-{audit,mongo}`.
- AWS: `dol-component-aws-{s3,sns,sqs,dynamo}`. Google: `dol-component-google-drive`. Office: `dol-component-excel`.
- Misc: `dol-component-netty`, `dol-component-serde-processor`, `dol-component-slack`.

**Why it matters.** These modules are the reason every service looks the same: CQRS-lite, `EditableDocument`
lifecycle, QueryDSL `PredicateBuilder`s, `BusinessLogicException` + `CusExceptionHandler`, and shared DTOs for
test/assignment/coursesheet/hubspot. Two parent lineages coexist: `dol-parent-v2` (Micronaut/Java 17 apps) and
older `dol-parent` v1.5–1.6 (some Spring Boot 3 services).

## Tiếng Việt

**Một dòng.** **35 module Maven dùng chung** (parent `dol-parent-v2_2`) mà mọi backend doltech phụ thuộc — chính là
"framework" nội bộ định nghĩa convention toàn fleet.

**`dol-common-*` — framework & model.**
- Framework: `dol-common`, `dol-common-cqrs` (lõi [[cqrs-command-query|CQRS-lite]]), `dol-common-kafka`, `dol-common-user`
  (`RequestUtils`), `dol-common-jackson`, `dol-common-mapper`(+`-processor`), `dol-common-rest-client` (Feign),
  `dol-common-partial-update`, `dol-common-sentry`, `dol-common-gcip`.
- Model: `dol-common-model`, `dol-common-model-{assignment,coursesheet,hubspot,test}`, `dol-common-marking-form`,
  `dol-common-question-{multiple-choice,quiz-test}`.

**`dol-component-*` — component hạ tầng.**
- Data: `dol-component-mongodb`(+`-data-processor`) ([[mongodb]] + [[querydsl|QueryDSL]]),
  `dol-component-editable-document` (lifecycle draft→published + version), `dol-component-track-user-edit-document`,
  `dol-component-custom-view`, `dol-component-jpa-{audit,mongo}`.
- AWS: `dol-component-aws-{s3,sns,sqs,dynamo}`. Google: `dol-component-google-drive`. Office: `dol-component-excel`.
- Khác: `dol-component-netty`, `dol-component-serde-processor`, `dol-component-slack`.

**Vì sao quan trọng.** Đây là lý do mọi service trông giống nhau: CQRS-lite, lifecycle `EditableDocument`, QueryDSL
`PredicateBuilder`, `BusinessLogicException` + `CusExceptionHandler`, DTO dùng chung. Hai dòng parent: `dol-parent-v2`
(Micronaut/Java 17) và `dol-parent` v1.5–1.6 cũ (vài service Spring Boot 3).

## Sources
- [[src-2026-06-22-doltech-tier3-survey]]
