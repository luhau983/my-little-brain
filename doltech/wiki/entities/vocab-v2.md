---
title: vocab-v2
type: entity
entity_type: project
tags: [project, doltech, vocab, srs, micronaut, standalone]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-standalone-survey]]"]
---

# vocab-v2

## English

**One-liner.** Vocabulary-learning service built around a **Spaced Repetition System (SRS)**: vocab sets,
flashcards, multiple exercise types, progress/streak analytics, and image enrichment.

**Stack (detected).** **Micronaut** (Netty) / Java 17 / Maven (parent `dol-parent-v2`); MongoDB (`vocab` db);
CQRS (Command/Query bus); Kafka (`dol-event`, disabled by default); MapStruct; OpenAPI. ~943 Java files, 32 controllers. Port 8083.

**Features.**
- **Course vocab management** — `CourseVocabSetRest`/`CourseVocabRest`/`CourseFlashCardRest`: CRUD vocab sets tied to courses (some marked deprecated).
- **SRS engine** — `SrsCalculationService`/`SrsConfigService`/`SrsInitializationService`: fluency-decay scheduling.
  Formula `F_now = max(0, F_stored − D·Δt)` (F fluency 0-100, D decay, K anchor ~2400 min). `SrsConfig` per user/skill.
- **Exercise types** — learn / test / write / matching / review / pronunciation REST endpoints. `VocabTest` (MultipleChoice/Writing), `Quiz`.
- **Progress & analytics** — `CourseVocabSetProgressRest`, `UserVocabSetRest`: stats, streaks. `UserProgressVocabSet`, `UserStreakStatistic`, `VocabReviewLog`.
- **Media & resources** — `ImageSearchRest` (Pexels), AWS S3 upload.
- **Import & validation** — bulk vocab import from Google Sheets/Excel; `vocab-resource-update` Kafka topic.

**Data model.** `Vocab`, `VocabSet`, `SrsConfig`, `UserProgressVocabSet`, `Progress`, `VocabTest`, `UserStreakStatistic`,
`VocabLearningLog`, `VocabReviewLog`, `WordInContext`.

**Integrations.** Directus, Strapi (CMS), document-history, go-user, [[offline-course-management]], Restate-AI (recommendations),
AWS S3, Google Drive, **Pexels** (stock images); MongoDB, Redis. Consumed by [[toeic-assignment]], [[virtual-exam]], etc. for vocab.

**Gotchas.** Deprecated `CourseVocabSet`/`CourseVocab`/`UserVocab` still in use. Kafka disabled by default. Plaintext AWS/Pexels keys in config.
SRS D/F/K tuning location unclear. Tight `dol-*` library coupling.

## Tiếng Việt

**Một dòng.** Service học từ vựng xây quanh **Spaced Repetition System (SRS)**: bộ từ, flashcard, nhiều dạng bài,
phân tích tiến độ/streak, và làm giàu hình ảnh.

**Stack (detect).** **Micronaut** (Netty) / Java 17 (parent `dol-parent-v2`); MongoDB (`vocab`); CQRS; Kafka (mặc định tắt); MapStruct; OpenAPI. ~943 file, 32 controller. Port 8083.

**Chức năng.**
- **Quản lý vocab khoá học** — `CourseVocabSetRest`/`CourseVocabRest`/`CourseFlashCardRest`: CRUD bộ từ theo khoá (một số deprecated).
- **SRS engine** — tính lịch ôn theo fluency-decay: `F_now = max(0, F_stored − D·Δt)`. `SrsConfig` theo user/skill.
- **Dạng bài** — learn/test/write/matching/review/pronunciation. `VocabTest` (MC/Writing), `Quiz`.
- **Tiến độ & analytics** — `UserProgressVocabSet`, `UserStreakStatistic`, `VocabReviewLog`.
- **Media** — `ImageSearchRest` (Pexels), upload S3.
- **Import** — bulk từ Google Sheets/Excel; topic `vocab-resource-update`.

**Data model.** `Vocab`, `VocabSet`, `SrsConfig`, `UserProgressVocabSet`, `Progress`, `VocabTest`, `UserStreakStatistic`, `VocabLearningLog`, `VocabReviewLog`, `WordInContext`.

**Tích hợp.** Directus, Strapi, document-history, go-user, [[offline-course-management]], Restate-AI, AWS S3, Google Drive, **Pexels**; MongoDB, Redis. Được [[toeic-assignment]], [[virtual-exam]]... dùng cho vocab.

**Lưu ý.** Entity `CourseVocab*` deprecated nhưng vẫn dùng. Kafka mặc định tắt. Key AWS/Pexels plaintext trong config. Chỗ tune SRS chưa rõ. Coupling chặt với lib `dol-*`.

## Sources
- [[src-2026-06-22-doltech-standalone-survey]]
