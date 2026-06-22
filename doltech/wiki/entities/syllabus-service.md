---
title: syllabus-service
type: entity
entity_type: project
tags: [project, doltech, syllabus, micronaut, standalone]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# syllabus-service

## English

**One-liner.** Standalone microservice managing course **syllabi** with a hierarchical structure
(course → week → subweek → resources), publishing registry, and activity audit.

**Stack (detected).** **Micronaut** (Netty) — *not* Spring — / Java 17 / Maven (parent `dol-parent-v2`),
MongoDB (Micronaut Data Document + QueryDSL), Kafka (`dol-common-kafka`), MapStruct, CQRS. ~309 Java files.

**Features.**
- **Syllabus management** — CRUD + tree navigation: `GET /syllabus/{id}/tree`, `/syllabus/{id}/detail`. Hierarchical
  Syllabus→Week→SubWeek docs. Handlers: Detail/Tree/Activity QueryHandlers (strict CQRS command vs query).
- **Syllabus code (publishing registry)** — unique code per published syllabus; PublishResult (SUCCESS/FAILURE/PENDING);
  `SyllabusCodeInUsedException`.
- **Resource management** — attach learning resources (assignment, exercise, material, mental-model, test, vocab, SAT, TOEIC,
  mock, online-test, dictation, virtual-exam) to syllabus items (`ResourceRest`); type-discriminated `Resource` doc.
- **Weeks & subweeks** — calendar structure; `SubWeekRest`; ChangeType ADD/UPDATE/DELETE.
- **Activity logging** — audit of create/update/publish (Action enum).

**Data model.** `Syllabus`, `Week`, `SubWeek`, `Resource` (type discriminator), `SyllabusCode` (unique code), `Activity` (audit).

**Integrations.** Feign rest clients to many apps: [[assignment-service]], exercise, [[material]], [[mental-model]], mock-test,
online-test, sat, [[toeic-assignment]], [[virtual-exam]], [[vocab-v2]]; Kafka; `dol-common-user` (identity).

**Gotchas.** Micronaut annotation processing (11 processors); QueryDSL Q-classes generated via apt-maven-plugin. Strict CQRS.
`dol-component-editable-document` for concurrent-edit tracking. (Cross-cutting hub — links resources from most exam apps.)

## Tiếng Việt

**Một dòng.** Microservice độc lập quản lý **syllabus** khoá học theo cấu trúc phân cấp (course → week → subweek → resource),
registry publish, và audit hoạt động.

**Stack (detect).** **Micronaut** (Netty) — *không phải* Spring — / Java 17 / Maven (parent `dol-parent-v2`),
MongoDB (Micronaut Data + QueryDSL), Kafka, MapStruct, CQRS. ~309 file Java.

**Chức năng.**
- **Quản lý syllabus** — CRUD + duyệt cây: `GET /syllabus/{id}/tree`, `/syllabus/{id}/detail`. Doc phân cấp Syllabus→Week→SubWeek. CQRS chặt.
- **Syllabus code (registry publish)** — mã unique cho syllabus đã publish; PublishResult; `SyllabusCodeInUsedException`.
- **Quản lý resource** — gắn tài nguyên học (assignment, exercise, material, mental-model, test, vocab, SAT, TOEIC, mock,
  online-test, dictation, virtual-exam) vào item syllabus (`ResourceRest`); `Resource` doc theo type.
- **Week & subweek** — cấu trúc lịch; `SubWeekRest`; ChangeType ADD/UPDATE/DELETE.
- **Activity log** — audit create/update/publish.

**Data model.** `Syllabus`, `Week`, `SubWeek`, `Resource` (type discriminator), `SyllabusCode`, `Activity`.

**Tích hợp.** Feign tới nhiều app: [[assignment-service]], exercise, [[material]], [[mental-model]], mock-test, online-test,
sat, [[toeic-assignment]], [[virtual-exam]], [[vocab-v2]]; Kafka; `dol-common-user`.

**Lưu ý.** Annotation processing Micronaut (11 processor); Q-class QueryDSL sinh qua apt-maven-plugin. CQRS chặt.
`dol-component-editable-document` cho tracking sửa đồng thời. (Hub cross-cutting — nối resource từ hầu hết app thi.)

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
