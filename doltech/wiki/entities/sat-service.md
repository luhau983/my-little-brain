---
title: sat-service
type: entity
entity_type: project
tags: [project, doltech, sat, exam, micronaut, standalone]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-standalone-survey]]"]
---

# sat-service

## English

**One-liner.** Backend for the DOL **SAT** exam platform: authoring (Reading/Writing + Math), auto-generation
from a question bank, test-taking (section/module/full/adaptive), scoring, progress, and AI explanations.

**Stack (detected).** **Micronaut 4 on Undertow** / Java 17 / Maven (parent `dol-parent-v2`); MongoDB (replica set),
Kafka (`dol-event`, failover only), S3, Google Drive; CQRS. ~807 Java files. Port 8087.

**Features.**
- **Authoring / content** — `/admin/*`: create/edit/publish FullTest, SectionTest, RW/Math ModuleTest; draft→publish + versioning.
- **Question bank** — `/test-detail/*`: reusable `QuestionWrapper(+Version)`; `Question` (MultipleChoice / FillAnswer), tagged `KnowledgeCode`.
- **Auto-generation** — `/auto-gen/*`: generate tests by qty/topic/level/difficulty/knowledge.
- **Sheet import** — `/admin/sheet/*`: import questions from Google Sheets; sync Directus.
- **AI explanation** — `/module-tests/explanation/generate`, `/ai/restate/receive/result`: via english-utils OR **Restate** durable
  workflow (feature-flagged `sat.restate.enable`); `AIGenerateQueue` state machine; webhook callback.
- **Do-test** — `/do-test/*`, `/attempt-test/*`: section/module/full/auto-gen; **adaptive 33-66-100 routing**; academy-mode variant.
- **Scoring** — `/attempt-test/submit-answer`, `/test-result/*`: evaluate MC + fill-answer (math service); % per section/module.
- **Progress & analysis** — `/test-progress/*`, `/test-result/analyze`: knowledge-code breakdown, weakness analysis; academy leaderboard.

**Data model.** `FullTest`, `SectionTest`, `RWModuleTest`/`MathModuleTest`, `QuestionWrapper(+Version)`, `Question`,
`*Progress` (Section/Module/Full), `AttemptTest`, `TestResult(+Detail)`, `AcademyProgress`, `AIGenerateQueue`.

**Integrations.** english-utils (AI), **Restate** (durable explanation workflow), Directus (prompts), math evaluator, n8n,
S3, user/go-user, document-history/action-history, [[offline-course-management]] (academy progress sync — REST-first, Kafka failover), page-management, Google Drive.

**Gotchas.** Auth gateway-injected (no `@Secured`). Optimistic lock + `@Retryable` on writes. Adaptive routing (≥66%/≥33% boundaries).
Restate vs english-utils both hit same callback → must be idempotent. Kafka is **failover**, not primary. Plaintext int creds in config; needs `-s settings.xml` (private Nexus), JDK 17.

## Tiếng Việt

**Một dòng.** Backend nền tảng **SAT** của DOL: soạn đề (Reading/Writing + Math), auto-gen từ ngân hàng câu hỏi,
làm bài (section/module/full/adaptive), chấm điểm, tiến độ, và AI giải thích.

**Stack (detect).** **Micronaut 4 trên Undertow** / Java 17 / Maven (parent `dol-parent-v2`); MongoDB, Kafka (failover), S3, Google Drive; CQRS. ~807 file. Port 8087.

**Chức năng.**
- **Soạn / nội dung** — `/admin/*`: tạo/sửa/publish FullTest, SectionTest, RW/Math ModuleTest; draft→publish + version.
- **Ngân hàng câu hỏi** — `/test-detail/*`: `QuestionWrapper(+Version)` tái dùng; `Question` (MC/FillAnswer) gắn `KnowledgeCode`.
- **Auto-gen** — `/auto-gen/*`: sinh đề theo số lượng/topic/level/độ khó/knowledge.
- **Import sheet** — `/admin/sheet/*`: import câu hỏi từ Google Sheets; sync Directus.
- **AI giải thích** — qua english-utils HOẶC **Restate** workflow (feature flag); `AIGenerateQueue`; webhook.
- **Do-test** — `/do-test/*`, `/attempt-test/*`: section/module/full/auto-gen; **adaptive 33-66-100**; academy-mode.
- **Chấm điểm** — `/attempt-test/submit-answer`, `/test-result/*`: chấm MC + fill-answer; % theo section/module.
- **Tiến độ & phân tích** — `/test-progress/*`, `/test-result/analyze`: breakdown theo knowledge-code; leaderboard academy.

**Data model.** `FullTest`, `SectionTest`, `RW/MathModuleTest`, `QuestionWrapper(+Version)`, `Question`, `*Progress`, `AttemptTest`, `TestResult(+Detail)`, `AcademyProgress`, `AIGenerateQueue`.

**Tích hợp.** english-utils, **Restate**, Directus, math evaluator, n8n, S3, user/go-user, document-history, [[offline-course-management]] (sync REST-first, Kafka failover), page-management, Google Drive.

**Lưu ý.** Auth do gateway bơm. Optimistic lock + `@Retryable`. Adaptive (ngưỡng ≥66%/≥33%). Restate & english-utils chung callback → phải idempotent. Kafka là **failover**. Creds plaintext; cần `-s settings.xml`, JDK 17.

## Sources
- [[src-2026-06-22-doltech-standalone-survey]]
