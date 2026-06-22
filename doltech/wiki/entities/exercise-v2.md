---
title: exercise-v2
type: entity
entity_type: project
tags: [project, doltech, exercise, ai-marking, standalone]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# exercise-v2

## English

**One-liner.** Standalone service for English-language **exercises** (grammar/speaking/writing/listening)
with AI-powered marking, suggestions & recommendations, student progress, and a junior module.

**Stack (detected).** **Spring Boot 3** / Java 17 / Maven (parent `dol-parent` v1.6.4 — older than spring-monorepo),
MongoDB (editable-document + Mongock migrations), Kafka (`dol-event`), Redis (JetCache), AWS **S3**, GraalVM native; CQRS (CommandBus/QueryBus).

**Features.**
- **Exercise CRUD** — `GET/POST/PUT /api/exercises` (filters: program/type/skill/questionType/level/status/date), published &
  offline-course variants. Polymorphic `Exercise` (Grammar/Speaking/Writing/Listening/MiniMentalModal).
- **Progress tracking** — `/api/exercises/progress/{id}/...`: submit page answers, sync audio, complete. `ExerciseProgress`, `ExerciseAttempt`.
- **AI features (async)** — suggestion/marking/recommendation via webhook callbacks `/api/ai/suggestion`, `/api/ai/recommendation`
  (model `exercise-o4-mini-high`); `AIGenerationEvent` tracks PENDING/SUCCESS/FAILED.
- **Junior module** — `/api/junior-exercise/*`: meta-info, valid-for-picking, batch meta (feeds [[junior]] entrance tests).
- **Speech recognition / audio** — speech-to-text via english-utils; audio sync for pronunciation.
- **Document history & versioning** — commit/revert via document-history; EditableDocument (DRAFT/PUBLISHED/ARCHIVED).
- **Public API** — `/api/public/exercises(/progress)` for LMS/mobile.

**Data model.** `exercise` (polymorphic), `exerciseProgress`, `exerciseAttempt`, `aiGenerationEvent`, `exerciseTrackingEdit`.

**Integrations.** go-user, Directus (characters/avatars), document-history, offline-course-management, english-utils-worker,
editor-utils, entrance-test (→ [[junior]]), AWS S3, Kafka `dol-event`, Redis, AI webhook (Kong gateway), Prometheus.

**Gotchas.** Older parent (`dol-parent` v1.6.4) — diverges from spring-monorepo baseline. Manual Kafka ack (no auto-commit).
Mongock migrations. AI all use one model `exercise-o4-mini-high`. GraalVM native → heavy reflection config. Referenced by [[junior]] & [[syllabus-service]].

## Tiếng Việt

**Một dòng.** Service độc lập cho **bài tập** tiếng Anh (grammar/speaking/writing/listening) với AI chấm, gợi ý &
recommendation, theo dõi tiến độ học sinh, và module junior.

**Stack (detect).** **Spring Boot 3** / Java 17 / Maven (parent `dol-parent` v1.6.4 — cũ hơn spring-monorepo),
MongoDB (editable-document + Mongock), Kafka (`dol-event`), Redis (JetCache), AWS **S3**, GraalVM native; CQRS (CommandBus/QueryBus).

**Chức năng.**
- **CRUD bài tập** — `GET/POST/PUT /api/exercises` (lọc nhiều tiêu chí), biến thể published & offline-course. `Exercise` đa hình.
- **Theo dõi tiến độ** — `/api/exercises/progress/{id}/...`: submit đáp án trang, sync audio, complete. `ExerciseProgress`, `ExerciseAttempt`.
- **AI (async)** — suggestion/marking/recommendation qua webhook `/api/ai/suggestion`, `/api/ai/recommendation`
  (model `exercise-o4-mini-high`); `AIGenerationEvent` theo dõi trạng thái.
- **Module junior** — `/api/junior-exercise/*`: meta-info, valid-for-picking, batch meta (cấp cho entrance test của [[junior]]).
- **Speech recognition / audio** — speech-to-text qua english-utils; sync audio phát âm.
- **Document history & version** — commit/revert; EditableDocument (DRAFT/PUBLISHED/ARCHIVED).
- **Public API** — `/api/public/exercises(/progress)` cho LMS/mobile.

**Data model.** `exercise` (đa hình), `exerciseProgress`, `exerciseAttempt`, `aiGenerationEvent`, `exerciseTrackingEdit`.

**Tích hợp.** go-user, Directus, document-history, offline-course-management, english-utils-worker, editor-utils,
entrance-test (→ [[junior]]), AWS S3, Kafka `dol-event`, Redis, AI webhook (Kong), Prometheus.

**Lưu ý.** Parent cũ hơn (`dol-parent` v1.6.4) — lệch baseline spring-monorepo. Kafka ack thủ công. Mongock migration.
AI dùng chung 1 model. GraalVM native → cấu hình reflection nặng. Được [[junior]] & [[syllabus-service]] tham chiếu.

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
