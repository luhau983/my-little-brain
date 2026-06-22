---
title: mid-final-test
type: entity
entity_type: project
tags: [project, doltech, exam, micronaut, micronaut-monorepo]
created: 2026-06-22
updated: 2026-06-22
status: stub
source_count: 1
sources: ["[[src-2026-06-22-doltech-tier3-survey]]"]
---

# mid-final-test

## English

> ⚠️ **STUB** — Explore agent cost-paused; assembled from references. **Flagged for re-ingest.**

**One-liner.** Mid-term / final-test management service for courses — authoring & administering mid/final
exams, the backend behind the `mid-final-test` and `final-test-*-student` frontends. Micronaut-monorepo app.

**Stack (detected, partial).** Micronaut / Java 17 (micronaut-monorepo, `dol-parent-v2`); MongoDB, BigQuery, Kafka.

**Known role (from references).** [[pd-management]] reads unmarked mid/final tests from a `mid-final-test`
service (for teacher penalty tracking). [[course-app-sheet-sync-job]] auto-opens final tests. Per-upstream thread pool (70) configured by callers.

**TODO (re-ingest).** Endpoints, entities (mid/final test defs, user results), scoring, marking workflow, integrations.

## Tiếng Việt

> ⚠️ **STUB** — agent dừng vì cost; ghép từ tham chiếu. **Cần ingest lại.**

**Một dòng.** Service quản lý bài **giữa kỳ / cuối kỳ** của khoá — soạn & tổ chức thi mid/final, backend cho frontend `mid-final-test` và `final-test-*-student`. App micronaut-monorepo.

**Stack (detect, 1 phần).** Micronaut / Java 17; MongoDB, BigQuery, Kafka.

**Vai trò đã biết.** [[pd-management]] đọc bài mid/final chưa chấm từ service `mid-final-test` (để tính phạt giáo viên). [[course-app-sheet-sync-job]] tự mở final test.

**TODO (ingest lại).** Endpoint, entity, chấm điểm, workflow marking, tích hợp.

## Sources
- [[src-2026-06-22-doltech-tier3-survey]]
