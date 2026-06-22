---
title: marking-form-service
type: entity
entity_type: project
tags: [project, doltech, marking, rubric, micronaut, micronaut-monorepo]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-tier3-survey]]"]
---

# marking-form-service

## English

**One-liner.** CRUD service for **marking rubrics** (forms with scoring criteria + comment templates),
used by the marking/assessment apps. Micronaut-monorepo app.

**Stack (detected).** Micronaut 4 (Undertow) / Java 17; MongoDB (QueryDSL), CQRS, Micrometer/Prometheus, Sentry (disabled).

**Features.**
- **List / search forms** — `GET /api/marking-forms`, `/search` (filter by display type + text). Paginated, DESC by lastModifiedAt.
- **Create / update** — `POST /api/marking-forms`, `PUT /{id}`: name (unique on create), scoring criteria (required if type ≠ PERCENT), comment items, displayType.
- **Get detail / raw** — `GET /{id}`, `/{id}/raw` (different DTOs, same doc).
- **Mark used / delete** — `PUT /{id}/used`, `DELETE /{id}`.

**Data model.** `MarkingFormDAO` (collection `markingForm`, extends shared `MarkingForm`): name, description, scoringCriteria[], commentItems[], scoringDisplayType (PERCENT/…).

**Integrations.** dol-common-marking-form (shared model), dol-common-user; AWS/HubSpot/Strapi declared but **unused**. No messaging.

**Gotchas.** Dup-name check on create only (no DB unique). Scoring criteria mandatory unless PERCENT. `NonEventCommandHandler` (not event-sourced). Plaintext creds. `vietnameseName` field unpopulated (no code path).

## Tiếng Việt

**Một dòng.** Service CRUD **rubric chấm** (form gồm tiêu chí điểm + mẫu comment), dùng bởi các app chấm/đánh giá. App micronaut-monorepo.

**Stack (detect).** Micronaut 4 (Undertow) / Java 17; MongoDB (QueryDSL), CQRS, Prometheus, Sentry (tắt).

**Chức năng.**
- **List / search** — `GET /api/marking-forms`, `/search`. Phân trang.
- **Create / update** — `POST`, `PUT /{id}`: tên (unique lúc create), tiêu chí điểm (bắt buộc nếu type ≠ PERCENT), comment, displayType.
- **Get detail / raw** — `GET /{id}`, `/{id}/raw`.
- **Mark used / delete** — `PUT /{id}/used`, `DELETE /{id}`.

**Data model.** `MarkingFormDAO` (`markingForm`): name, description, scoringCriteria[], commentItems[], scoringDisplayType.

**Tích hợp.** dol-common-marking-form, dol-common-user; AWS/HubSpot/Strapi khai báo nhưng **không dùng**. Không messaging.

**Lưu ý.** Check trùng tên chỉ lúc create. Tiêu chí điểm bắt buộc trừ PERCENT. `NonEventCommandHandler`. Creds plaintext. `vietnameseName` chưa có code điền.

## Sources
- [[src-2026-06-22-doltech-tier3-survey]]
