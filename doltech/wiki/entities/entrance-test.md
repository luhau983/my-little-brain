---
title: entrance-test
type: entity
entity_type: project
tags: [project, doltech, entrance-test, micronaut, micronaut-monorepo]
created: 2026-06-22
updated: 2026-06-22
status: stub
source_count: 1
sources: ["[[src-2026-06-22-doltech-tier3-survey]]"]
---

# entrance-test

## English

> ⚠️ **STUB** — Explore agent cost-paused; assembled from references. **Flagged for re-ingest.**

**One-liner.** Entrance-test (placement) service: manages entrance exams used to place new students,
the backend behind the `entrance-test-*-student` frontends. Micronaut-monorepo app.

**Stack (detected, partial).** Micronaut / Java 17 (micronaut-monorepo, `dol-parent-v2`).

**Known role (from references).** [[junior]] and [[exercise-v2]] call an entrance-test service
(`EntranceTestRestClient`) to create/publish junior entrance tests, fetch metadata, notify skill
start/submit/AI-completion. Frontends: `entrance-test-student`, `entrance-test-junior/sat/toeic-student`, `entrance-test-v2`.

**TODO (re-ingest).** Endpoints, entities (entrance test definitions, user attempts), scoring, exact integrations.

## Tiếng Việt

> ⚠️ **STUB** — agent dừng vì cost; ghép từ tham chiếu. **Cần ingest lại.**

**Một dòng.** Service entrance-test (xếp lớp): quản lý bài thi đầu vào để xếp lớp học sinh mới, backend cho các frontend `entrance-test-*-student`. App micronaut-monorepo.

**Stack (detect, 1 phần).** Micronaut / Java 17 (micronaut-monorepo, `dol-parent-v2`).

**Vai trò đã biết.** [[junior]] và [[exercise-v2]] gọi service entrance-test (`EntranceTestRestClient`) để tạo/publish entrance test, lấy metadata, báo skill start/submit/AI-complete. Frontend: `entrance-test-student`, `entrance-test-junior/sat/toeic-student`, `entrance-test-v2`.

**TODO (ingest lại).** Endpoint, entity, chấm điểm, tích hợp chính xác.

## Sources
- [[src-2026-06-22-doltech-tier3-survey]]
