---
title: toeic-assignment
type: entity
entity_type: project
tags: [project, doltech, toeic, exam, ai-marking, restate]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# toeic-assignment

## English

**One-liner.** TOEIC speaking/writing assessment platform with AI auto-marking (orchestrated by
**Restate**), progress tracking, payment/membership gating, vocab, and SEO content sync via Kafka.

**Stack.** Baseline + heavy **Restate v2** (async marking workflows), Kafka V2, JetCache, EditableDocument versioning.

**Features.**
- **Data entry (exam management)** — `/api/speaking-full/*` (+ part/writing): create/update/publish/clone/delete.
  Entities `ExamTestGroup{Speaking,Writing}`, `ExamPart{Speaking,Writing}` + `*Version`. Publish → SEO sync via Kafka.
- **Do test (student)** — `/academy/do-test/*`: start, save answers, submit (→ AI marking), exam-status. Entity `UserExamProgress`, `UserExamAttempt`, `ExamPartProgress`.
- **AI marking (Restate)** — callbacks `/api/v1/restate/ai-marking-{full,section,question}-test/completion`, `/ai-grammar/completion`.
  Queue docs `AIMarkingGenerated`/`AIExtraGenerated`/`AIMemberGenerated` (status GENERATING/DONE/ERROR); idempotency key.
- **Analysis** — `/api/analyze/progress/{id}`: scores, transcript, vocab, statistics.
- **Payment & access** — `PaymentSupportController` + `AIMemberService`: validates membership via [[billing]] before AI marking; `AITaskPayment` cost tracking.
- **Landing/SEO** — `SEOPageHelper` → Kafka `SYNC_SEO_RESOURCE_TOPIC`.
- **Vocab & Bang Vang** — vocab sets (→ vocab-v2); achievement events `academy_event_bang_vang_action` (→ [[user-academy-event]]).

**Data model.** `exam_test_group_{ws,speaking,writing}(_version)`, `exam_part_{speaking,writing}`, `user_exam_progress`,
`user_exam_attempt`, `ai_marking_generated`, `ai_extra_generated`, `ai_member_generated`. Polymorphic questions/answers/attachments.

**Integrations.** Restate (`restate-int:8080`), [[billing]] (membership), page-management, document-history, english-utils-worker,
editor-utils, s3-service-v2, vocab-v2, Directus; Kafka `toeic-marking:{academy_event_do_test_action,completed_test,academy_event_bang_vang_action}`, Redis.

**Gotchas.** AI marking gated by payment (`AIMemberService` → billing). Restate orchestrates long marking; `AIMarkingGenerated.key` idempotent.
Versioned exam docs (draft mutable, publish spawns `*Version`). Scoring dispatches on `userExamType` (full/section/question). Distinct from the older [[toeic]] (multiple-choice L/R) app.

## Tiếng Việt

**Một dòng.** Nền tảng đánh giá TOEIC speaking/writing với AI chấm tự động (điều phối **Restate**), theo dõi tiến độ,
kiểm soát thanh toán/membership, vocab, và sync SEO qua Kafka.

**Stack.** Baseline + **Restate v2** (workflow chấm async), Kafka V2, JetCache, versioning EditableDocument.

**Chức năng.**
- **Nhập liệu đề** — `/api/speaking-full/*` (+ part/writing): create/update/publish/clone/delete. Entity `ExamTestGroup{Speaking,Writing}`, `ExamPart{...}` + `*Version`. Publish → sync SEO.
- **Học sinh làm bài** — `/academy/do-test/*`: start, lưu đáp án, submit (→ AI chấm), exam-status. Entity `UserExamProgress`, `UserExamAttempt`.
- **AI chấm (Restate)** — callback `/api/v1/restate/ai-marking-{full,section,question}-test/completion`. Queue doc `AI*Generated`; idempotency key.
- **Phân tích** — `/api/analyze/progress/{id}`: điểm, transcript, vocab, thống kê.
- **Thanh toán & quyền** — `AIMemberService`: kiểm tra membership qua [[billing]] trước khi chấm; `AITaskPayment` theo dõi chi phí.
- **Landing/SEO** — `SEOPageHelper` → Kafka `SYNC_SEO_RESOURCE_TOPIC`.
- **Vocab & Bang Vang** — bộ vocab (→ vocab-v2); event thành tích (→ [[user-academy-event]]).

**Data model.** `exam_test_group_*(_version)`, `exam_part_*`, `user_exam_progress`, `user_exam_attempt`, `ai_*_generated`. Đa hình.

**Tích hợp.** Restate, [[billing]], page-management, document-history, english-utils-worker, editor-utils, s3-service-v2, vocab-v2, Directus; Kafka `toeic-marking:*`, Redis.

**Lưu ý.** AI chấm gate bởi thanh toán (qua [[billing]]). Restate điều phối chấm dài; idempotent. Đề có version. Khác với app [[toeic]] cũ (trắc nghiệm L/R).

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
