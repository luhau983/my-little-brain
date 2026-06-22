---
title: junior
type: entity
entity_type: project
tags: [project, doltech, exam, ai-marking]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# junior

## English

**One-liner.** English-testing platform for the "Junior" proficiency level: exam/exercise authoring and
entrance-test execution across Vocab/Grammar/Pronunciation skills, with AI marking for writing questions.

**Stack.** Baseline. Inter-service comms via Feign HTTP (not Kafka). AI marking via english-utils queue.

**Features.**
- **Exam Full management** — `/api/exam-full/*`: CRUD, publish, clone. Entity `ExamFull` with vocab/grammar/
  pronunciation parts (lists of `ExamPartTestItem`), versioned.
- **Exam Part management** — `/api/exam-part/*`: CRUD, publish, clone, mark-used. Entity `ExamPart` (Vocab 1-5,
  Grammar 1-3, Pronunciation); polymorphic questions; `markingType` AUTO or AI per part.
- **Entrance test execution** — `/public/api/do-test-entrance/*`: start (full or per-skill), fetch progress, save
  answers, submit skill (→ marking pipeline). Entity `ExamSkillProgress` (status NOT_STARTED→IN_PROGRESS→
  WAITING_AI_MARKING→COMPLETED), embedded `ExamPartProgress` + `UserAnswer`.
- **Result/overview** — `/public/api/do-test-entrance-overview/*`: full overview + per-part answers with keys (review).
- **Junior exercise** — `/api/junior-exercise/*`: skill-based practice sets. Entity `JuniorExercise` (`ExerciseSkillItem`).
- **AI marking** — `POST /api/ai/receive/score`: webhook from english-utils with scored writing; `ProgressHelper`
  updates scores + transitions WAITING_AI_MARKING→COMPLETED. Config `AIConfig` (model `junior-gpt-4o-json`).
- **Internal entrance support** — `/api/internal/entrance/*`: test meta, progress overview, answer-key, manual scoring.

**Data model.** `exam_full(_version)`, `exam_part(_version)`, `exam_skill_progress`, `junior_exercise(_version)`.

**Integrations.** entrance-test service, exercise-v2 ([[exercise-v2]]), english-utils (AI marking), Redis cache.

**Gotchas.** Marking type per part drives status flow (AUTO completes instantly; AI → WAITING). Lazy statistics
(`getStatistic()` recomputes). AI callbacks may arrive out of order — idempotent update by `questionKey`. Versioned at publish.

## Tiếng Việt

**Một dòng.** Nền tảng test tiếng Anh cấp độ "Junior": soạn exam/exercise và làm bài entrance test theo kỹ năng
Vocab/Grammar/Pronunciation, kèm AI chấm câu hỏi viết.

**Stack.** Baseline. Giao tiếp liên service qua Feign HTTP (không Kafka). AI marking qua queue english-utils.

**Chức năng.**
- **Quản lý Exam Full** — `/api/exam-full/*`: CRUD, publish, clone. Entity `ExamFull` gồm các part vocab/grammar/
  pronunciation, có version.
- **Quản lý Exam Part** — `/api/exam-part/*`: CRUD, publish, clone, mark-used. Entity `ExamPart`; câu hỏi đa hình;
  `markingType` AUTO hoặc AI theo part.
- **Làm entrance test** — `/public/api/do-test-entrance/*`: start (full hoặc từng skill), lấy tiến độ, lưu đáp án,
  submit skill (→ pipeline chấm). Entity `ExamSkillProgress` (NOT_STARTED→IN_PROGRESS→WAITING_AI_MARKING→COMPLETED).
- **Kết quả/tổng quan** — `/public/api/do-test-entrance-overview/*`: tổng quan + đáp án từng part kèm key (xem lại).
- **Junior exercise** — `/api/junior-exercise/*`: bộ luyện theo skill. Entity `JuniorExercise`.
- **AI marking** — `POST /api/ai/receive/score`: webhook từ english-utils trả điểm bài viết; cập nhật điểm + chuyển
  WAITING_AI_MARKING→COMPLETED. Config `AIConfig` (model `junior-gpt-4o-json`).
- **Hỗ trợ entrance nội bộ** — `/api/internal/entrance/*`: metadata test, tổng quan tiến độ, answer-key, chấm tay.

**Data model.** `exam_full(_version)`, `exam_part(_version)`, `exam_skill_progress`, `junior_exercise(_version)`.

**Tích hợp.** entrance-test service, [[exercise-v2]], english-utils (AI marking), Redis.

**Lưu ý.** markingType từng part quyết định luồng trạng thái (AUTO xong ngay; AI → WAITING). Thống kê tính lười.
Callback AI có thể đến lệch thứ tự — cập nhật idempotent theo `questionKey`. Tạo version khi publish.

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
