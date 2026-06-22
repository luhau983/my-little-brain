---
title: assignment-service
type: entity
entity_type: project
tags: [project, doltech, assignment, ai-marking, standalone]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-standalone-survey]]"]
---

# assignment-service

## English

**One-liner.** Manages **assignments** (writing/speaking/extra-docs) with multi-role marking
(student / teacher / TA), AI marking, and real-time collaboration via Firebase.

**Stack (detected).** **Spring Boot 3** / Java (parent `dol-parent` v1.6) / Maven; MongoDB (primary) +
**DynamoDB** (correction/version history) + **Firebase Realtime DB** (live marking) + Redis (Dragonfly) +
AWS S3; Kafka; CQRS. Spring Security disabled (auth via `dol-common-user`).

**Features.**
- **Assignment management** — `POST/GET/PUT /api/assignment`: writing/speaking/extra-docs, publish, track. Polymorphic `Assignment`.
- **Student submissions** — `/api/student/assignments/corrections`: submit corrections, view feedback. `WritingCorrection`, `SpeakingCorrection`.
- **Teacher / TA marking** — `/api/teacher-marking`, `/api/ta-marking`: mark, comment, TA→teacher approval workflow. `Score`, `CorrectionHistory`.
- **AI marking (async)** — `/api/system-marking/ai`: event-driven AI marking for writing/speaking. `CorrectionAiSuggestion`.
- **Learning / ranking** — `/api/learning/assignments/...`: corrections + ranking.
- **User-activity stats** — `/api/user-activity-summarize/*`: TA/teacher engagement, inactivity alerts.
- **Cron jobs** — remove expired TA corrections (15m), inactive-participant cleanup, marking-stats update (30m).

**Data model.** `assignment` (+ writing/speaking/extra subtypes), `*_correction`, `correction_history`,
`assignment_progress`, `assignment_tracking_edit`, `user_assignment_marking_statistic`, `correction_ai_suggestion`.
DynamoDB: correction/version history archive. Firebase: `/marking-corrections` live docs.

**Integrations.** user/go-user, Directus, Customer.io (email), document-history, course-app-sheet, [[offline-course-management]],
speaking-assessment, english-utils-worker, [[pd-management]], Firebase Admin, AWS S3; Kafka topics `dol-event`, `mock-test-marking`, `ai-assignment-marking`.

**Gotchas.** Spring Security disabled (custom auth). Polymorphic assignments need discriminator in queries.
Firebase realtime DB for concurrent marking — conflict resolution unclear. Plaintext creds in `application.yml` (dev). Linked from [[pd-management]] (penalties) & [[syllabus-service]].

## Tiếng Việt

**Một dòng.** Quản lý **bài tập lớn (assignment)** (writing/speaking/extra-docs) với chấm đa vai trò
(student / teacher / TA), AI chấm, và cộng tác real-time qua Firebase.

**Stack (detect).** **Spring Boot 3** / Java (parent `dol-parent` v1.6); MongoDB + **DynamoDB** (history) +
**Firebase Realtime DB** (chấm live) + Redis + AWS S3; Kafka; CQRS. Spring Security tắt (auth qua `dol-common-user`).

**Chức năng.**
- **Quản lý assignment** — `POST/GET/PUT /api/assignment`: writing/speaking/extra, publish, track. `Assignment` đa hình.
- **Bài nộp học sinh** — `/api/student/assignments/corrections`: nộp, xem feedback. `WritingCorrection`, `SpeakingCorrection`.
- **Chấm giáo viên / TA** — `/api/teacher-marking`, `/api/ta-marking`: chấm, comment, luồng TA→giáo viên duyệt. `Score`, `CorrectionHistory`.
- **AI chấm (async)** — `/api/system-marking/ai`: chấm AI hướng sự kiện. `CorrectionAiSuggestion`.
- **Learning / ranking** — `/api/learning/assignments/...`.
- **Thống kê hoạt động** — `/api/user-activity-summarize/*`: engagement TA/giáo viên, cảnh báo không hoạt động.
- **Cron** — xoá correction TA hết hạn (15m), dọn participant inactive, cập nhật stats chấm (30m).

**Data model.** `assignment` (+ subtypes), `*_correction`, `correction_history`, `assignment_progress`,
`assignment_tracking_edit`, `user_assignment_marking_statistic`, `correction_ai_suggestion`; DynamoDB history; Firebase live docs.

**Tích hợp.** user/go-user, Directus, Customer.io, document-history, course-app-sheet, [[offline-course-management]],
speaking-assessment, english-utils-worker, [[pd-management]], Firebase, AWS S3; Kafka `dol-event`/`mock-test-marking`/`ai-assignment-marking`.

**Lưu ý.** Spring Security tắt. Assignment đa hình cần discriminator. Firebase real-time cho chấm đồng thời. Creds plaintext trong config (dev). Được [[pd-management]] & [[syllabus-service]] tham chiếu.

## Sources
- [[src-2026-06-22-doltech-standalone-survey]]
