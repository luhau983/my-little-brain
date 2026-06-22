---
title: virtual-exam
type: entity
entity_type: project
tags: [project, doltech, ielts, exam, ai-marking]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# virtual-exam

## English

**One-liner.** IELTS/English exam-practice platform with AI auto-marking for Writing & Speaking
(via **n8n** workflows + **Restate** orchestration), full & single-section tests, progress analytics,
teacher review, and HeyGen real-mode speaking videos.

**Stack.** Baseline + n8n (marking workflows), Restate (long-running steps), Kafka V2, polymorphic exam types (`@JsonTypeInfo`).

**Features.**
- **Test management (data entry)** — `/api/v1/practice/entry` (+ exam-full): CRUD, publish, AI content gen (n8n). Polymorphic
  `ExamTest` (Speaking Part1-3, Writing Task1 Academic/General, Task2), `ExamFullTest`.
- **Do test — single section** — `/api/v1/exam/do-test/{start,submit}`: modes Academy/In-Course/Final/Trial. Entity `VirtualExamTestProgress` (polymorphic) + history.
- **Do test — full exam** — `/api/v1/exam-full/do-test/*`: multi-section, section-wise submit. Entity `VirtualExamFullProgress`.
- **AI marking (Speaking & Writing)** — callbacks `/api/ai/receive-{marking,writing-step,speaking-question}-result`; n8n workflows
  per skill/scope; Restate orchestrates; re-marking trigger. Entities `MarkingProgressStepDoc`, `MarkingCorrection(+History)`, `MarkingChargeHistory`.
- **Progress & analytics** — `/api/v1/progress/{overview,statistic}`, `/api/v1/academy/user/{userId}/overview`, examiner stats.
- **Marking correction (teacher)** — `/api/v1/marking-correction`: review/challenge AI marks; percentile estimate config.
- **My vocab** — `/api/v1/my-vocab`: track difficult words (→ vocab-v2).
- **Real-mode speaking (HeyGen)** — `/api/v1/speaking-answer-real-mode`: store/query generated speaking videos.
- **Course-bound tests** — `/api/v1/course/{courseId}/*`: student tests + teacher class progress.

**Data model.** `examTest` (polymorphic), `exam_full_test`, `virtual_exam_test_progress(_history)`, `virtual_exam_full_progress`,
`marking_correction_history`, `marking_charge_history`, `real_mode_speaking_answer`, `payment_event_log`, `marking_estimate_config`, `percentile`.

**Integrations.** n8n (5 marking workflows), Restate (`restate-int:8080`), audio-service, session-speaking-orchestrator,
online-test-v2, vocab-v2, page-management, english-utils-worker, editor-utils, s3-service-v2, billing, Directus; Kafka V2, Redis.
Emits `completed_test`/`cap_nhat_bang_vang_action` consumed by [[practice-management]] & [[user-academy-event]].

**Gotchas.** Polymorphic exam/progress via `@JsonTypeInfo` (be explicit adding subtypes). `StartFrom` enum (COURSE/ACA/TRIAL)
affects visibility + billing. Marking cost tracked (`MarkingChargeHistory`) tied to payment. n8n↔Restate: n8n runs the AI step, Restate adds durability/retries.

## Tiếng Việt

**Một dòng.** Nền tảng luyện thi IELTS/English với AI chấm tự động Writing & Speaking (qua workflow **n8n** + điều phối
**Restate**), đề full & từng section, phân tích tiến độ, giáo viên review, và video speaking real-mode (HeyGen).

**Stack.** Baseline + n8n (workflow chấm), Restate (bước chạy dài), Kafka V2, loại đề đa hình (`@JsonTypeInfo`).

**Chức năng.**
- **Quản lý đề (data entry)** — `/api/v1/practice/entry` (+ exam-full): CRUD, publish, AI gen nội dung (n8n). `ExamTest` đa hình, `ExamFullTest`.
- **Làm bài — từng section** — `/api/v1/exam/do-test/{start,submit}`: mode Academy/In-Course/Final/Trial. Entity `VirtualExamTestProgress` (đa hình) + history.
- **Làm bài — full** — `/api/v1/exam-full/do-test/*`: nhiều section, submit theo section. Entity `VirtualExamFullProgress`.
- **AI chấm (Speaking & Writing)** — callback `/api/ai/receive-*-result`; workflow n8n theo skill/scope; Restate điều phối; re-marking.
- **Tiến độ & phân tích** — `/api/v1/progress/{overview,statistic}`, `/api/v1/academy/user/{userId}/overview`.
- **Marking correction (giáo viên)** — `/api/v1/marking-correction`: review/challenge điểm AI.
- **My vocab** — `/api/v1/my-vocab` (→ vocab-v2).
- **Speaking real-mode (HeyGen)** — `/api/v1/speaking-answer-real-mode`: lưu/truy vấn video speaking.
- **Test theo khoá** — `/api/v1/course/{courseId}/*`: test học sinh + tiến độ lớp cho giáo viên.

**Data model.** `examTest` (đa hình), `exam_full_test`, `virtual_exam_test_progress(_history)`, `virtual_exam_full_progress`,
`marking_*_history`, `real_mode_speaking_answer`, `payment_event_log`, `marking_estimate_config`, `percentile`.

**Tích hợp.** n8n (5 workflow chấm), Restate, audio-service, session-speaking-orchestrator, online-test-v2, vocab-v2,
page-management, english-utils-worker, editor-utils, s3-service-v2, billing, Directus; Kafka V2, Redis. Emit event tới [[practice-management]] & [[user-academy-event]].

**Lưu ý.** Đề/progress đa hình qua `@JsonTypeInfo`. `StartFrom` (COURSE/ACA/TRIAL) ảnh hưởng hiển thị + billing. Chi phí chấm
gắn thanh toán. Ranh giới n8n↔Restate: n8n chạy bước AI, Restate thêm durability/retry.

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
