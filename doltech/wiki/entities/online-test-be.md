---
title: online-test-be
type: entity
entity_type: project
tags: [project, doltech, online-test, exam, standalone]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-standalone-survey]]"]
---

# online-test-be

## English

**One-liner.** Online English-test backend: test/section management, AI-powered question generation,
test execution & scoring, and a dictation module.

**Stack (detected).** **Spring Boot** / Java / Maven (parent `dol-parent` v1.6.4). MongoDB (replica set), Kafka/Redpanda,
AWS S3 + CDN, Google Drive/Sheets; CQRS (event-driven — few REST controllers, mostly command/query handlers).

**Features.**
- **AI question generation** — `api/test-sections/ai/explanation/received` (webhook); queues `online-test-gpt-5-mini-high`, `online-test-o3`.
  `AIGenerateQueueService`, `AIGenerateStatusEnum`.
- **User test execution** — `UserDoTestOverviewController`; `FullTestService`, `ScoreService`; `DoTestStatus(V2)`.
- **Test section management** — `test-sections/*`; history via `EditableDocumentWithHistoryService`; `TestSectionPublishHistory`.
- **Dictation module** — `UserDictationService`, `DictationWordType`.
- **Document/content management** — Google Drive + editable-document + track-user-edit.

**Data model.** `Test`, `TestSection`, `Question`, `User`, `Score`, `AIGenerateQueue`, `UserDictation`, `DocumentHistory`,
`TestSectionPublishHistory`. ~60 enums (ContentGroup, EnglishLevel, EnglishSkill, etc.).

**Integrations.** page-management, TTS, user-service, membership, action-history, document-history, editor-utils,
english-utils, Directus, n8n; AWS S3, Google Drive/Sheets, Kafka. Emits `completed_test` consumed by [[practice-management]]/[[user-academy-event]].

**Gotchas.** Mostly CQRS/event-driven (single REST controller observed). Plaintext AWS creds (dev). Mongo replica set required.
AI queue retry (100-item limits). Same older `dol-parent` v1.6.4 as [[exercise-v2]].

> Note: partial read (agent cost-paused) — features/data-model may be incomplete; flagged for re-ingest.

## Tiếng Việt

**Một dòng.** Backend test tiếng Anh online: quản lý test/section, AI sinh câu hỏi, làm bài & chấm điểm, và module dictation.

**Stack (detect).** **Spring Boot** / Java (parent `dol-parent` v1.6.4). MongoDB (replica set), Kafka/Redpanda, AWS S3 + CDN, Google Drive/Sheets; CQRS (event-driven, ít REST controller).

**Chức năng.**
- **AI sinh câu hỏi** — `api/test-sections/ai/explanation/received` (webhook); queue `online-test-gpt-5-mini-high`, `online-test-o3`.
- **Học sinh làm bài** — `UserDoTestOverviewController`; `FullTestService`, `ScoreService`.
- **Quản lý test section** — `test-sections/*`; history qua `EditableDocumentWithHistoryService`.
- **Module dictation** — `UserDictationService`, `DictationWordType`.
- **Quản lý nội dung** — Google Drive + editable-document + track-user-edit.

**Data model.** `Test`, `TestSection`, `Question`, `User`, `Score`, `AIGenerateQueue`, `UserDictation`, `DocumentHistory`, `TestSectionPublishHistory`. ~60 enum.

**Tích hợp.** page-management, TTS, user-service, membership, action-history, document-history, editor-utils, english-utils, Directus, n8n; AWS S3, Google Drive/Sheets, Kafka. Emit `completed_test` (→ [[practice-management]]/[[user-academy-event]]).

**Lưu ý.** Chủ yếu CQRS/event-driven. Creds plaintext (dev). Cần Mongo replica set. AI queue retry (giới hạn 100). Cùng parent cũ `dol-parent` v1.6.4 như [[exercise-v2]].

> Lưu ý: đọc 1 phần (agent dừng vì cost) — feature/data-model có thể chưa đủ; cần ingest lại.

## Sources
- [[src-2026-06-22-doltech-standalone-survey]]
