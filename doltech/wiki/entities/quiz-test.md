---
title: quiz-test
type: entity
entity_type: project
tags: [project, doltech, quiz, micronaut, micronaut-monorepo]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-tier3-survey]]"]
---

# quiz-test

## English

**One-liner.** REST API for **quiz/test** management with CQRS + MongoDB, plus user progress tracking.
One of the micronaut-monorepo apps.

**Stack (detected).** Micronaut (Undertow) / Java 17 / Maven; MongoDB (QueryDSL), CQRS, AWS S3 + SQS, Sentry (disabled), OpenAPI.

**Features.**
- **Quiz CRUD + publish** — `POST/PUT/GET/DELETE /api/quiz-tests`, `PUT /api/quiz-tests/publish`. `QuizTest` (extends EditableDocument): name, program, skill, timeLimit, `questionGroup[]`.
- **Discovery** — `GET /api/quiz-tests?search/program/skill/status/availableFor`. `by-test-id/{id}`.
- **User progress** — `GET /api/user-tests/{id}`, `default-user/{id}`. `UserProgressQuizTest` (status `DoTestStatus`, `TestResult`).
- **Mark used** — `PUT /api/quiz-tests/{id}/used`.

**Data model.** `QuizTest` (+ `QuizTestQuestionGroup`), `UserProgressQuizTest`.

**Integrations.** dol-common-question-quiz-test (shared models), user-service, AWS S3/SQS (speech-to-text queue). Used by [[syllabus-service]] as a resource type.

**Gotchas.** **Bug:** `markQuizTestUsed()` dispatches `DeleteQuizTestCommand` (copy-paste, `QuizTestRest.java:97`). Sentry disabled. Plaintext AWS creds. Dup-name check on create only.

## Tiếng Việt

**Một dòng.** REST API quản lý **quiz/test** với CQRS + MongoDB, kèm theo dõi tiến độ. Một app của micronaut-monorepo.

**Stack (detect).** Micronaut (Undertow) / Java 17; MongoDB (QueryDSL), CQRS, AWS S3 + SQS, Sentry (tắt), OpenAPI.

**Chức năng.**
- **CRUD + publish quiz** — `POST/PUT/GET/DELETE /api/quiz-tests`, `PUT .../publish`. `QuizTest` (EditableDocument).
- **Discovery** — `GET /api/quiz-tests?search/program/skill/...`, `by-test-id/{id}`.
- **Tiến độ user** — `GET /api/user-tests/{id}`, `default-user/{id}`. `UserProgressQuizTest`.
- **Mark used** — `PUT /api/quiz-tests/{id}/used`.

**Data model.** `QuizTest` (+ `QuizTestQuestionGroup`), `UserProgressQuizTest`.

**Tích hợp.** dol-common-question-quiz-test, user-service, AWS S3/SQS. Được [[syllabus-service]] dùng như 1 resource type.

**Lưu ý.** **Bug:** `markQuizTestUsed()` lại dispatch `DeleteQuizTestCommand` (`QuizTestRest.java:97`). Sentry tắt. Creds AWS plaintext. Check trùng tên chỉ lúc create.

## Sources
- [[src-2026-06-22-doltech-tier3-survey]]
