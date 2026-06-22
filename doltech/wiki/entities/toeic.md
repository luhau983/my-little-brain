---
title: toeic
type: entity
entity_type: project
tags: [project, doltech, toeic, exam, critical]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# toeic

## English

**One-liner.** TOEIC exam-prep platform (Listening/Reading, 7 parts): full tests, parts, questions,
user test-taking & scoring, AI explanation generation, an academy subsystem, and offline-test tracking.
**One of the oldest & most critical doltech services.**

**Stack.** Baseline, but **traditional layered packages** (`controller`/`service/impl`/`repository`/`documents`) —
NOT feature-based like newer apps. AI explanations via n8n (models `toeic-gpt-5-mini-high`, `toeic-o3`).

**Features.**
- **Do-test (practice/exam)** — `/toeic/do-test/{start,meta,progress,submit-answer}`: full/part practice with per-part progress.
  Entities `UserTest`, `UserTestResult`, `UserTestQuestionAnswer`, `UserTestPartInformation`.
- **Full test management** — `/toeic/full-test/*`: CRUD 7-part mock exams. Entities `FullTest`, `Part`, `Question`, `QuestionGroup`.
- **Part & question import** — `/toeic/part/sheet/{import,validate}`, `/sync-mini`: import from Excel/Google Sheets, validate, queue explanations.
- **AI explanation generation** — `/toeic/part/question/explanation/generate`, `/part/queue/receive/explanation` (webhook). `PartExplanationQueue`,
  `Question.explanationGenStatus` (PENDING/PROCESSING/DONE/ERROR).
- **User history & statistics** — `/toeic/user-test-history/by-filter`, `/test-result/result/{id}`. `UserTestHistory`, `TestScore`, `TestTimeTracking`.
- **Academy (learning path)** — `/toeic/academy/*`: versioned exam groups/parts + user progress. `AcademyGroup(+Version)`, `AcademyPart(+Version)`, `UserExamProgress`.
- **Preview & filtering** — `/toeic/preview/*`, `/toeic/filter/test`.
- **Sync (external trigger)** — `/toeic/sync-total`, `/toeic/roadmap/generate`: Kafka events to CRM/marketing.

**Data model.** `question`, `part`, `full_test`, `user_test`, `user_test_result`, `user_test_question_answer`, `user_test_history`,
`part_explanation_queue`, `academy_group(+part)`, `user_exam_progress`, `cfg_{test,part,level}`. Plus `UserOfflineTestResult` (offline).

**Integrations.** coursesupporter, Kafka (test completion/enrollment), Directus, S3, n8n (explanations), english-utils-worker,
offline-course-management, document-history, editor-utils, email, Google Sheets; JetCache.

**Gotchas.** **Critical/oldest service — do NOT refactor core scoring (`ScoringService`) or history logic without explicit instructions.**
`@AuthorCheck` annotation for auth. Offline tests synced on reconnect (`OfflineUserTestProgressTrackingHandler`). Distinct from newer [[toeic-assignment]] (speaking/writing AI marking).

## Tiếng Việt

**Một dòng.** Nền tảng luyện TOEIC (Listening/Reading, 7 part): full test, part, câu hỏi, học sinh làm bài & chấm điểm,
AI sinh giải thích, hệ academy, và theo dõi test offline. **Một trong các service lâu đời & quan trọng nhất của doltech.**

**Stack.** Baseline, nhưng **package phân tầng truyền thống** (`controller`/`service/impl`/`repository`/`documents`) —
KHÔNG feature-based như app mới. AI giải thích qua n8n (model `toeic-gpt-5-mini-high`, `toeic-o3`).

**Chức năng.**
- **Do-test** — `/toeic/do-test/{start,meta,progress,submit-answer}`: làm full/part, theo dõi tiến độ từng part. Entity `UserTest`, `UserTestResult`, ...
- **Quản lý full test** — `/toeic/full-test/*`: CRUD đề mock 7 part. Entity `FullTest`, `Part`, `Question`, `QuestionGroup`.
- **Import part & câu hỏi** — `/toeic/part/sheet/{import,validate}`, `/sync-mini`: import Excel/Sheets, validate, queue giải thích.
- **AI sinh giải thích** — `/toeic/part/question/explanation/generate`, webhook nhận kết quả. `PartExplanationQueue`, `explanationGenStatus`.
- **Lịch sử & thống kê** — `/toeic/user-test-history/by-filter`, `/test-result/result/{id}`.
- **Academy (lộ trình học)** — `/toeic/academy/*`: exam group/part có version + tiến độ user.
- **Preview & lọc** — `/toeic/preview/*`, `/toeic/filter/test`.
- **Sync (trigger ngoài)** — `/toeic/sync-total`, `/toeic/roadmap/generate`: event Kafka tới CRM/marketing.

**Data model.** `question`, `part`, `full_test`, `user_test(_result)`, `user_test_question_answer`, `user_test_history`,
`part_explanation_queue`, `academy_group(+part)`, `user_exam_progress`, `cfg_*`, `UserOfflineTestResult`.

**Tích hợp.** coursesupporter, Kafka, Directus, S3, n8n, english-utils-worker, offline-course-management, document-history, editor-utils, email, Google Sheets; JetCache.

**Lưu ý.** **Service quan trọng/lâu đời — KHÔNG refactor scoring (`ScoringService`) hay logic history nếu không có chỉ thị rõ.**
`@AuthorCheck` cho auth. Test offline sync khi online lại. Khác với [[toeic-assignment]] mới (AI chấm speaking/writing).

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
