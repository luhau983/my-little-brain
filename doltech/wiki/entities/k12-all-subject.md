---
title: k12-all-subject
type: entity
entity_type: project
tags: [project, doltech, exam, k12, ai]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# k12-all-subject

## English

**One-liner.** Multi-subject K12 exam platform across 11 subjects (incl. Literature/`van`): test
authoring + versioning, student do-test, AI explanation & marking (via Restate workflows), analytics.

**Stack.** Baseline + Apache Tika/POI, Google Sheets, AI queue (`k12-o4-mini-high`), CDN, **Restate** orchestration.

**Features.**
- **Exam test management** — `/api/exam/{subject}/*`: CRUD, paged (search/status/examType/used), publish (`AvailableFor`),
  Excel export. Subject-specific collections + `*_exam_test_version`. Entity `BaseSubjectExamTest` (extends `EditableDocument`).
- **AI generation & marking** — `/api/hook/*`: explanation received/retry-one/all/import, `marking/{taskId}`, queue-status.
  Restate-orchestrated; question types `AIGapFillQuestion`, `AISelfResponsiveQuestion`.
- **Do-test flow** — `/public/api/do-test/{subject}/*`: start, check-status, save, submit (+`submit-van` for Literature),
  check-answer, extend-time, change-mode. Entities `user_exam_test`, `user_exam_test_progress`; polymorphic `UserAnswer`.
- **Results & analytics** — `/public/api/do-test-overview/*`: result, overview, rank, history; `/analyze/progress/{id}`.
- **Sheet import/export** — Google Sheets (range A2:AT; A2:AC for `van`).
- **Sync & events** — `/api/sync/*`, `/api/internal/sync-to-marketer/{subject}`; Kafka `k12-all-service/{receive_user_do_test_action,completed_test}`; `BaseSubjectExamTestListener` → [[action-history]].
- **Public discovery / Literature view** — public exam details + Literature passage view/tracking (no attempt).

**Data model.** 11 subject `*_exam_test` collections + `*_exam_test_version`, `user_exam_test(_progress)`, `ai_generate_status`, `ai_generate_marking`.

**Integrations.** page-management, document-history, [[action-history]], english-utils-worker, s3-service-v2, editor-utils, Directus; Google Sheets/Cloud, Kafka, Restate, Redis.

**Gotchas.** Subject↔collection 1:1 (11 enums). Literature (`isVan()`) special-cased (separate view session, scoring). Question keys re-ordered on save. Restate `idempotencyKey` guards duplicate AI marking. Sibling of [[g12]] but all-subject.

## Tiếng Việt

**Một dòng.** Nền tảng thi K12 đa môn (11 môn, gồm Ngữ văn/`van`): soạn đề + version, học sinh làm bài, AI sinh
giải thích & chấm (qua workflow Restate), phân tích.

**Stack.** Baseline + Apache Tika/POI, Google Sheets, AI queue (`k12-o4-mini-high`), CDN, **Restate**.

**Chức năng.**
- **Quản lý đề** — `/api/exam/{subject}/*`: CRUD, phân trang, publish, export Excel. Mỗi môn 1 collection + `*_exam_test_version`.
  Entity `BaseSubjectExamTest`.
- **AI sinh & chấm** — `/api/hook/*`: nhận/retry/import giải thích, `marking/{taskId}`, queue-status. Điều phối bằng Restate;
  loại câu `AIGapFillQuestion`, `AISelfResponsiveQuestion`.
- **Luồng do-test** — `/public/api/do-test/{subject}/*`: start, check-status, save, submit (+`submit-van`), check-answer,
  extend-time, change-mode. Entity `user_exam_test(_progress)`; `UserAnswer` đa hình.
- **Kết quả & phân tích** — `/public/api/do-test-overview/*`: result, overview, rank, history; `/analyze/progress/{id}`.
- **Import/export sheet** — Google Sheets (range A2:AT; A2:AC cho `van`).
- **Sync & event** — `/api/sync/*`; Kafka `k12-all-service/...`; `BaseSubjectExamTestListener` → [[action-history]].
- **Khám phá công khai / xem Ngữ văn** — xem chi tiết đề + đọc bài Ngữ văn (không làm bài).

**Data model.** 11 collection `*_exam_test` + `*_exam_test_version`, `user_exam_test(_progress)`, `ai_generate_status`, `ai_generate_marking`.

**Tích hợp.** page-management, document-history, [[action-history]], english-utils-worker, s3-service-v2, editor-utils, Directus; Google, Kafka, Restate, Redis.

**Lưu ý.** Môn↔collection 1:1 (11 enum). Ngữ văn (`isVan()`) xử lý đặc biệt (view session + chấm riêng). Key câu hỏi đánh lại khi save.
Restate `idempotencyKey` chống chấm AI trùng. Là "anh em" của [[g12]] nhưng đa môn.

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
