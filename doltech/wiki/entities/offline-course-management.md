---
title: offline-course-management
type: entity
entity_type: project
tags: [project, doltech, course, offline, micronaut, standalone]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-standalone-survey]]"]
---

# offline-course-management

## English

**One-liner.** Offline / classroom course-management backend: enrollment, per-student progress across
**every resource type** (exercise, vocab, dictation, reading, assignment, online/final/mock/SAT tests),
syllabus & roadmap structure, streaks, and statistics. The central sync hub many apps push progress to.

**Stack (detected).** Micronaut 3.4.3 (Undertow) / Java 17 / Maven (`dol-parent-v2` 2.2.21); MongoDB
(`offline-course`, **107 document classes**) + QueryDSL, Kafka (off by default; many topics), Redis (commented),
AWS S3, Google Drive, Sentry, CQRS. `application.yml` ~6480 lines (per-service event loops).

**Features.**
- **Course management** — `GET/PUT /api/course-management/courses/{id}/*`: general info, students/teachers/TAs, syllabus, class sessions. `CourseSyllabus`→`Week`→`SubWeek`.
- **Learning management** — `GET /api/student/courses/{courseId}/*`: attendance/exercise/vocab statistics by `studentRegistrationKey`.
- **Resource management (per type)** — exercise, vocab set, dictation, reading, sample, online/final/mock/SAT test; each `Course<X>` + `UserCourse<X>` extends `BaseCourseResource`; synced from external services.
- **Assignment management** — `/api/assignment/*`: status, deadline, attempts, best scores; cron `AssignmentJob`/`MissingScoreJob` auto-close overdue.
- **Syllabus / Roadmap** — master syllabus (weeks→subweeks→resources) + per-user roadmap clones (`UserRoadmapDayProgress`, auto-generation commands).
- **Streaks & gamification** — `CourseStreak`/`UserCourseStreak` daily-completion tracking.
- **Statistics** — `StudentResourceStatistic`, `CourseStudentStatistic` aggregated per resource type.
- **Notifications** — Customer.io transactional email (assignment reminders), SMS gateway.

**Data model.** `course_syllabus`, `course_*`/`user_course_*` per resource type, `course_student_status`, `*_statistic`,
`user_roadmap_*`, `sms`/`student_sms`, `email_sent_event`, `Removed*` (soft-delete). All extend `BaseDocument`. ~107 doc classes.

**Integrations.** 20+ Feign rest clients: [[exercise-v2]], [[assignment-service]], online-test, final-test/[[mid-final-test]],
mock-test, [[entrance-test]], roadmap, dictation, vocab/[[vocab-v2]], [[material]], [[study-hub]], k12/g12/[[toeic]]/[[virtual-exam]]/[[mental-model]];
HubSpot, Customer.io, Strapi, Directus, Google Drive, AWS S3, Slack; Kafka topics (`dol-event`, `*-resource-update`, `offline-course.roadmap.{generate,unassign}-resource`).

**Gotchas.** `studyTemplate` (SYLLABUS vs ROADMAP) changes the data hierarchy + sync logic. `studentRegistrationKey` (not userId)
scopes students. Soft-delete `Removed*` collections. Per-service Netty event loops (10 threads) to avoid starvation. Cron 5-min
auto-close. Kafka `enabled:false` in config. Plaintext creds. Micronaut (not Spring). Sat/material/exercise-v2/assignment push progress here.

## Tiếng Việt

**Một dòng.** Backend quản lý khoá học **offline / lớp học**: ghi danh, tiến độ từng học sinh trên **mọi loại tài nguyên**
(exercise, vocab, dictation, reading, assignment, online/final/mock/SAT test), cấu trúc syllabus & roadmap, streak, thống kê.
Hub sync trung tâm mà nhiều app đẩy tiến độ về.

**Stack (detect).** Micronaut 3.4.3 (Undertow) / Java 17 (`dol-parent-v2` 2.2.21); MongoDB (`offline-course`, **107 doc class**)
+ QueryDSL, Kafka (mặc định tắt), Redis (comment), AWS S3, Google Drive, Sentry, CQRS. `application.yml` ~6480 dòng.

**Chức năng.**
- **Quản lý khoá** — `GET/PUT /api/course-management/courses/{id}/*`: info, students/teachers/TAs, syllabus, buổi học. `CourseSyllabus`→`Week`→`SubWeek`.
- **Learning management** — `GET /api/student/courses/{courseId}/*`: thống kê điểm danh/exercise/vocab theo `studentRegistrationKey`.
- **Quản lý resource (theo loại)** — exercise/vocab/dictation/reading/sample/online/final/mock/SAT; `Course<X>` + `UserCourse<X>` (extends `BaseCourseResource`); sync từ service ngoài.
- **Quản lý assignment** — `/api/assignment/*`: status/deadline/attempt/best score; cron auto-close quá hạn.
- **Syllabus / Roadmap** — syllabus gốc (weeks→subweeks→resource) + roadmap clone theo user (`UserRoadmapDayProgress`).
- **Streak** — `CourseStreak`/`UserCourseStreak`.
- **Thống kê** — `StudentResourceStatistic`, `CourseStudentStatistic`.
- **Thông báo** — email Customer.io (nhắc assignment), SMS gateway.

**Data model.** `course_syllabus`, `course_*`/`user_course_*`, `course_student_status`, `*_statistic`, `user_roadmap_*`,
`sms`/`student_sms`, `email_sent_event`, `Removed*` (soft-delete). ~107 doc class.

**Tích hợp.** 20+ Feign client: [[exercise-v2]], [[assignment-service]], online-test, final-test/[[mid-final-test]], mock-test,
[[entrance-test]], roadmap, dictation, [[vocab-v2]], [[material]], [[study-hub]], k12/g12/[[toeic]]/[[virtual-exam]]/[[mental-model]];
HubSpot, Customer.io, Strapi, Directus, Google Drive, AWS S3, Slack; Kafka (`dol-event`, `*-resource-update`, `roadmap.{generate,unassign}-resource`).

**Lưu ý.** `studyTemplate` (SYLLABUS vs ROADMAP) đổi cấu trúc data + logic sync. `studentRegistrationKey` (không phải userId).
Soft-delete `Removed*`. Event loop Netty riêng/service (10 thread). Cron 5 phút auto-close. Kafka `enabled:false`. Creds plaintext.
Micronaut (không Spring). sat/material/exercise-v2/assignment đẩy tiến độ về đây.

## Sources
- [[src-2026-06-22-doltech-standalone-survey]]
