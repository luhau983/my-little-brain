---
title: entrance-test
type: entity
entity_type: project
tags: [project, doltech, entrance-test, micronaut, micronaut-monorepo]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-tier3-survey]]"]
---

# entrance-test

## English

**One-liner.** Service managing learner **entrance / placement exams** across test types
(IELTS/TOEIC/SAT/junior), online & offline, with AI marking, EC/TA summarization analytics, and
HubSpot/Customer.io contact sync. Backend behind the `entrance-test-*-student` frontends.

**Stack (detected).** Micronaut 4 (Undertow) / Java 17 / Maven; MongoDB + QueryDSL 4.3.1, Redis (Lettuce),
Kafka, CQRS (`dol-common-cqrs`), AWS S3/SNS/SQS, Google Drive.

**Features.**
- **Entrance test management** — `GET/POST/PUT/DELETE /api/entrance-tests`: skills, duration, level, program, availableFor. `EntranceTest`, `EntranceTestSkill` (Grammar/Listening/Reading/Speaking/Vocab/Writing).
- **User test execution** — `POST /api/user-entrance-tests/{id}/{start,submit}`, `GET .../{userId}/progress`. Polymorphic `UserEntranceTest` (Online/Offline), `EntranceTestSession`. `dealId` unique.
- **AI marking** — `POST /api/mark-entrance-test`, `/api/mark-student/{id}/ai-marking`: speaking/writing scored via Kafka `ai-entrance-test-marking`; `MarkCheatingHistory`, `SpeakingAudioReplaceHistory`.
- **Multi test-type** — TOEIC/SAT/Junior start/progress/submit endpoints; type-specific event handlers.
- **Contact & lead** — `POST /api/contacts(/sync)`: upsert to HubSpot, trigger Customer.io entrance-test email.
- **EC/TA summarize analytics** — `GET /api/{ec,ta,overall}-summarize`: action counts, time-to-finish stats.
- **Progress tracking** — session state in Redis + `ProgressUpdatedEvent` on Kafka.
- **History/audit + Slack notifs** — EditableDocument change history; `POST /api/slack/send-message`.

**Data model.** `entranceTest`, `userEntranceTestV2` (Online/Offline polymorphic), progress, `markCheatingHistory`,
`speakingAudioReplaceHistory`, `eCSummarize`, `taSummarize`, `timeFinishTestStatistic`, `contact`, `oldUserEntranceTest` (legacy).

**Integrations.** [[assignment-service]], [[course-app-sheet-api]], go-user, [[marking-form-service]], online-test-v2,
[[quiz-test]], [[sat-service]], [[toeic]], [[junior]], [[exercise-v2]], test-report, document-history; Directus, HubSpot,
Customer.io, AWS S3/SNS/SQS, Google Drive, Slack; Kafka `dol-event`, `audio-to-text`, `ai-entrance-test-marking`.

**Gotchas.** Feature-domain layout (`toeic_test/`, `sat_test/`, `junior/`…). Polymorphic `UserEntranceTest` via
`@JsonTypeInfo`/`@JsonSubTypes`. Undertow (Netty excluded). Plaintext creds in `application.yml`. Redis = session/stat cache.
SAT progress points at `localhost:8092` (likely dev override). Called by [[junior]] & [[exercise-v2]] via `EntranceTestRestClient`.

## Tiếng Việt

**Một dòng.** Service quản lý **thi đầu vào / xếp lớp** đa loại (IELTS/TOEIC/SAT/junior), online & offline, có AI chấm,
analytics tổng hợp EC/TA, và sync contact HubSpot/Customer.io. Backend cho các frontend `entrance-test-*-student`.

**Stack (detect).** Micronaut 4 (Undertow) / Java 17; MongoDB + QueryDSL, Redis, Kafka, CQRS, AWS S3/SNS/SQS, Google Drive.

**Chức năng.**
- **Quản lý đề đầu vào** — `GET/POST/PUT/DELETE /api/entrance-tests`. `EntranceTest`, `EntranceTestSkill`.
- **Làm bài** — `POST /api/user-entrance-tests/{id}/{start,submit}`, `GET .../{userId}/progress`. `UserEntranceTest` (Online/Offline đa hình), `EntranceTestSession`. `dealId` unique.
- **AI chấm** — speaking/writing qua Kafka `ai-entrance-test-marking`; `MarkCheatingHistory`, `SpeakingAudioReplaceHistory`.
- **Đa loại test** — endpoint TOEIC/SAT/Junior start/progress/submit; event handler theo loại.
- **Contact & lead** — `POST /api/contacts(/sync)`: upsert HubSpot, gửi email Customer.io.
- **Analytics EC/TA** — `GET /api/{ec,ta,overall}-summarize`: số action, thời gian hoàn thành.
- **Theo dõi tiến độ** — state session ở Redis + `ProgressUpdatedEvent` qua Kafka.
- **History/audit + Slack** — EditableDocument; `POST /api/slack/send-message`.

**Data model.** `entranceTest`, `userEntranceTestV2` (đa hình), progress, `markCheatingHistory`, `speakingAudioReplaceHistory`,
`eCSummarize`, `taSummarize`, `timeFinishTestStatistic`, `contact`, `oldUserEntranceTest`.

**Tích hợp.** [[assignment-service]], [[course-app-sheet-api]], go-user, [[marking-form-service]], online-test-v2, [[quiz-test]],
[[sat-service]], [[toeic]], [[junior]], [[exercise-v2]], test-report, document-history; Directus, HubSpot, Customer.io,
AWS S3/SNS/SQS, Google Drive, Slack; Kafka `dol-event`, `audio-to-text`, `ai-entrance-test-marking`.

**Lưu ý.** Layout theo feature-domain. `UserEntranceTest` đa hình (`@JsonTypeInfo`). Undertow (loại Netty). Creds plaintext.
Redis = cache session/stat. SAT progress trỏ `localhost:8092` (dev?). Được [[junior]] & [[exercise-v2]] gọi qua `EntranceTestRestClient`.

## Sources
- [[src-2026-06-22-doltech-tier3-survey]]
