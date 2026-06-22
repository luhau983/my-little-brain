---
title: sat-service-entrance-final
type: entity
entity_type: project
tags: [project, doltech, sat, exam, micronaut, micronaut-monorepo]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-tier3-survey]]"]
---

# sat-service-entrance-final

## English

**One-liner.** SAT **entrance/final** test-execution engine: full-test & section-based progress,
math/RW scoring, with engineer re-edit/re-score capability. Sibling of [[sat-service]] for entrance/final contexts.

**Stack (detected).** Micronaut / Java 17 (Undertow); MongoDB, Kafka, Google Drive, AWS S3, Sentry, Prometheus, QueryDSL.

**Features.**
- **Test-taking** — `POST /api/do-test/full-test/start`, `/{id}/start`, `/{id}/{sectionIndex}/start`; save `PUT /{id}`; submit `POST /{id}/submit` (optimistic-lock retry); fetch `GET /{id}`.
- **Engineer re-edit** — `GET /{id}/engineer`, `POST /{id}/engineer/submit`: overwrite answers & rescore (admin/QA).

**Data model.** `TestProgress` (+ section/module/question hierarchy), `FullTestProgressDTO`, `EngineerSubmitFullTestDTO`.

**Integrations.** MongoDB, Kafka (events), Google Drive (doc sync), AWS S3, Sentry, Prometheus.

**Gotchas.** Optimistic locking + retry on submit/engineer-submit. Score recalculation on engineer override. Editable-document for live updates. Distinct from [[sat-service]] (main authoring/do-test) — this is the entrance/final variant.

## Tiếng Việt

**Một dòng.** Engine làm bài SAT cho **entrance/final**: tiến độ full-test & theo section, chấm math/RW, có khả năng engineer sửa/chấm lại. Anh em với [[sat-service]] cho ngữ cảnh entrance/final.

**Stack (detect).** Micronaut / Java 17; MongoDB, Kafka, Google Drive, AWS S3, Sentry, Prometheus, QueryDSL.

**Chức năng.**
- **Làm bài** — `POST /api/do-test/full-test/start`, `/{id}/start`, `/{id}/{sectionIndex}/start`; save `PUT /{id}`; submit `POST /{id}/submit` (retry optimistic-lock); fetch `GET /{id}`.
- **Engineer sửa lại** — `GET /{id}/engineer`, `POST /{id}/engineer/submit`: ghi đè đáp án & chấm lại (admin/QA).

**Data model.** `TestProgress` (+ section/module/question), `FullTestProgressDTO`, `EngineerSubmitFullTestDTO`.

**Tích hợp.** MongoDB, Kafka, Google Drive, AWS S3, Sentry, Prometheus.

**Lưu ý.** Optimistic lock + retry khi submit/engineer-submit. Chấm lại khi engineer override. Editable-document. Khác [[sat-service]] (bản chính) — đây là biến thể entrance/final.

## Sources
- [[src-2026-06-22-doltech-tier3-survey]]
