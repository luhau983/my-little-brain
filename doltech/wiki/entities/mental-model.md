---
title: mental-model
type: entity
entity_type: project
tags: [project, doltech, quiz, leaderboard, course]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# mental-model

## English

**One-liner.** Manages & runs "mental model" tests (multi-choice quizzes) with student leaderboards,
progress tracking, and course integration via a provider (SPI) pattern.

**Stack.** Baseline. Kafka producer-only (via coursesupporter events); no consumer.

**Features.**
- **Mental model data entry** — `/api/mental-models/*`: CRUD, clone, publish/publish-for, track-edit, bulk mark-used.
  Entity `MentalModel` (extends `BaseEditingDocument`) + version; fields studyTemplate, practiceType, polymorphic `testContent`.
- **Query & pagination** — `/api/mental-models/{paged,published-paged,by-ids}`: filter by program/level/practiceType/status/used/date.
- **Test execution (do-test)** — `/api/do-test/*`: start, save, submit, result, view-attempt. Entity `Progress` (`progress`):
  userResourceId, mentalModelKey, status, userAnswers, statistic; `@Retryable` on submit (optimistic lock).
- **Leaderboard** — `/api/learning-management/student/{subClassKey}/{resourceId}/leaderboard`. Entity `StudentLeaderBoard`;
  override only if higher score (or same score faster); max 2 attempts count (`MAX_ATTEMPT_CAN_COUNT_IN_LEADERBOARD`).
- **Course integration** — `/api/learning-management/*` (student) + `/api/course/course-mental-models/*` (teacher):
  per-student/class stats via coursesupporter `FilterService`/`StatisticService`.
- **Backfill utils** — `/api/learning-management/backfill/latest-progress-id?dryRun=`.

**Data model.** `mentalModel` (+version), `progress`, `student_leader_board`.

**Integrations.** coursesupporter (providers: ResourceInfo/CourseSupporter/Roadmap/Extra), Kafka events
(NotifyStart/Progress/Complete via `CourseStatusEventHandler`), Redis, MongoDB.

**Gotchas.** Auto-redo triggers at 80% correctness. Leaderboard caps counted attempts at 2. Publishes course events via
Spring ApplicationEventPublisher (in-process) → Kafka; does not consume. Progress pins the mental-model version taken.

## Tiếng Việt

**Một dòng.** Quản lý & chạy test "mental model" (quiz trắc nghiệm) kèm bảng xếp hạng học sinh, theo dõi tiến độ,
và tích hợp khoá học qua provider (SPI).

**Stack.** Baseline. Chỉ producer Kafka (qua event coursesupporter); không consume.

**Chức năng.**
- **Nhập liệu mental model** — `/api/mental-models/*`: CRUD, clone, publish/publish-for, track-edit, mark-used.
  Entity `MentalModel` (+version); studyTemplate, practiceType, `testContent` đa hình.
- **Query & phân trang** — `/api/mental-models/{paged,published-paged,by-ids}`: lọc program/level/practiceType/status/used/ngày.
- **Làm bài (do-test)** — `/api/do-test/*`: start, save, submit, result, view-attempt. Entity `Progress`; `@Retryable` khi submit.
- **Leaderboard** — `/api/learning-management/student/{subClassKey}/{resourceId}/leaderboard`. Entity `StudentLeaderBoard`;
  chỉ override nếu điểm cao hơn (hoặc bằng nhưng nhanh hơn); tối đa 2 lần tính.
- **Tích hợp khoá học** — `/api/learning-management/*` (học sinh) + `/api/course/course-mental-models/*` (giáo viên):
  thống kê học sinh/lớp qua coursesupporter.
- **Backfill** — `/api/learning-management/backfill/latest-progress-id?dryRun=`.

**Data model.** `mentalModel` (+version), `progress`, `student_leader_board`.

**Tích hợp.** coursesupporter (provider SPI), event Kafka (NotifyStart/Progress/Complete), Redis, MongoDB.

**Lưu ý.** Auto-redo khi đạt 80% đúng. Leaderboard chỉ tính 2 lần thử. Publish event qua Spring ApplicationEventPublisher
(in-process) → Kafka; không consume. Progress ghim version mental-model lúc làm.

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
