---
title: mid-final-test
type: entity
entity_type: project
tags: [project, doltech, exam, final-test, micronaut, micronaut-monorepo]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-tier3-survey]]"]
---

# mid-final-test

## English

**One-liner.** Service for **mid-term / final test** assessments (online & offline, multi-skill
GRAMMAR/READING/LISTENING/WRITING/SPEAKING), with AI + teacher marking, cheating detection, statistics,
and SAT/TOEIC/junior sub-modules. Backend behind `final-test-*-student` & `mid-final-test` frontends.

**Stack (detected).** Micronaut 3.x (Undertow, port 8081) / Java 17; MongoDB (`mid-final-test` db) + QueryDSL,
Kafka (`dol-event`, `ai-final-test-marking`), Redis (configured-off), Google BigQuery, Sentry (off), CQRS.

**Features.**
- **Final test management** — `GET/POST /api/final-tests`: multi-skill composition, TOEIC/SAT variants. `FinalTest`, polymorphic `FinalTestSkill`.
- **Online execution & marking** — `/api/online-final-tests/*`, `/api/online/user-final-tests/*`: submit → progress → AI marking (Kafka) → teacher review. `OnlineUserFinalTest`.
- **Offline submission & teacher marking** — `/api/offline/user-final-tests/*`: manual marking + cheating check. `OfflineUserFinalTest`, `MarkCheatingHistory`.
- **Quiz tests** — `/api/online-final-tests/quiz-test/*` auto-marked.
- **SAT & TOEIC sub-apps** — `/api/sat-test/*`, `/api/cron-job/{sat,toeic}`, `/public/api/toeic-test/email`: dedicated CQRS/Kafka per variant.
- **Junior-exercise sidecar** — `/api/junior-exercise-user-final-test/*`: full sub-app.
- **Statistics** — `/api/{statistic,ta-statistic,teacher-statistic}/*`: teacher/TA/employee marking stats.
- **AI marking pipeline** — `KafkaFinalTestProducer.sendAiMarkingEvent()` → `ai-final-test-marking`.
- **Cron + event logging + cheating** — auto-open/close, reminders; `UserFinalTestEvent` + cheating flags.

**Data model.** `FinalTest`, `FinalTestSkill` (polymorphic), `OnlineUserFinalTest`/`OfflineUserFinalTest`/`CompletedUserFinalTest`,
40+ per-skill progress & marking repos, teacher/TA/employee statistic repos, SAT/TOEIC/junior collections. Marking version history repos.

**Integrations.** [[assignment-service]], [[course-app-sheet-api]], Directus, [[entrance-test]], [[exercise-v2]],
[[marking-form-service]], online-test-v2, [[quiz-test]], [[toeic]], test-report, user, [[virtual-exam]], n8n, english-utils;
HubSpot, Customer.io, Google Drive, AWS S3, BigQuery, Sentry; Kafka `dol-event` + `ai-final-test-marking`; Zalo ZNS (off).
**[[pd-management]] reads unmarked tests from here** for teacher-penalty tracking.

**Gotchas.** 40+ dedicated repos (no generic base). Polymorphic skills need type-switch in `collectTotalDuration()`. Offline flow
separate from online. `EditableDocument` draft/publish. `ProtectOptimisticLockService` for concurrent marking. SAT/TOEIC are
subdomain modules; junior-exercise a sidecar (extractable). Plaintext creds. Kafka localhost fallback.

## Tiếng Việt

**Một dòng.** Service **thi giữa kỳ / cuối kỳ** (online & offline, đa kỹ năng), có AI + giáo viên chấm, phát hiện gian lận,
thống kê, và sub-module SAT/TOEIC/junior. Backend cho frontend `final-test-*-student` & `mid-final-test`.

**Stack (detect).** Micronaut 3.x (Undertow, port 8081) / Java 17; MongoDB (`mid-final-test`) + QueryDSL, Kafka, Redis (tắt), BigQuery, Sentry (tắt), CQRS.

**Chức năng.**
- **Quản lý final test** — `GET/POST /api/final-tests`: ghép đa kỹ năng, biến thể TOEIC/SAT. `FinalTest`, `FinalTestSkill` đa hình.
- **Online execution & marking** — submit → progress → AI chấm (Kafka) → giáo viên review. `OnlineUserFinalTest`.
- **Offline + chấm tay** — chấm thủ công + check gian lận. `OfflineUserFinalTest`, `MarkCheatingHistory`.
- **Quiz** — `/api/online-final-tests/quiz-test/*` tự chấm.
- **Sub-app SAT & TOEIC** — `/api/sat-test/*`, `/api/cron-job/{sat,toeic}`: CQRS/Kafka riêng.
- **Sidecar junior-exercise** — `/api/junior-exercise-user-final-test/*`.
- **Thống kê** — teacher/TA/employee marking stats.
- **Pipeline AI chấm** — `KafkaFinalTestProducer` → `ai-final-test-marking`.
- **Cron + event log + gian lận** — auto-open/close, nhắc; `UserFinalTestEvent` + cờ gian lận.

**Data model.** `FinalTest`, `FinalTestSkill`, `Online/Offline/CompletedUserFinalTest`, 40+ repo progress/marking theo skill,
repo thống kê teacher/TA/employee, collection SAT/TOEIC/junior.

**Tích hợp.** [[assignment-service]], [[course-app-sheet-api]], Directus, [[entrance-test]], [[exercise-v2]], [[marking-form-service]],
online-test-v2, [[quiz-test]], [[toeic]], test-report, user, [[virtual-exam]], n8n, english-utils; HubSpot, Customer.io, Google Drive,
AWS S3, BigQuery, Sentry; Kafka `dol-event` + `ai-final-test-marking`. **[[pd-management]] đọc bài chưa chấm từ đây.**

**Lưu ý.** 40+ repo riêng. Skill đa hình → type-switch. Offline tách online. `EditableDocument`. `ProtectOptimisticLockService`.
SAT/TOEIC là subdomain; junior-exercise là sidecar. Creds plaintext. Kafka localhost fallback.

## Sources
- [[src-2026-06-22-doltech-tier3-survey]]
