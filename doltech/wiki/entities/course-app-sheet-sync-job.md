---
title: course-app-sheet-sync-job
type: entity
entity_type: project
tags: [project, doltech, sync, cron, micronaut, standalone]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-standalone-survey]]"]
---

# course-app-sheet-sync-job

## English

**One-liner.** Cron/sync microservice that synchronizes course enrollment, attendance, feedback, and
schedule data between internal systems (MongoDB/BigQuery), Google Sheets, Zoom, HubSpot, and n8n. Feeds [[course-app-sheet-api]].

**Stack (detected).** **Micronaut 3.4.3** (Netty) / Java 17 / Maven (parent `dol-parent-v2`); MongoDB (replica set), BigQuery,
Redis (Dragonfly), Kafka (`dol-event`, often disabled); Prometheus + Sentry. Port 8080.

**Features (cron-triggered commands).**
- **Course sync** — `GET /api/cron-job/sync-course-app-sheet-student`: enrollment from queue → CourseAppSheet.
- **Attendance / absence** — mark absent, resolve make-up sessions, auto-archive red flags. `AttendanceMakeUpSessionProjected`, `StudentLearningStatus`.
- **Zoom integration** — `/api/cron-job/zoom/sync-registrants*`, `/webhook/`: sync registrants vs roster; record `RegistrantUpdateHistory`.
- **Final test & entrance form** — auto-open final tests; reminder emails.
- **Feedback & review** — CS/student feedback reminders (HubSpot-tracked). `FeedbackReminderTrackingLog`.
- **Email notifications** — daily course-publish + completion emails (Customer.io, 29 templates).
- **Google Sheets sync** — schedules/registration/employees/feedback to multiple sheets.
- **HubSpot contact sync** — students, avatars, registration. `HSContact`.
- **Checklist tasks** — CS in-charge assignments, course task deadlines.
- **BigQuery analytics** — code-DOL usage, EC deal counts.

**Data model.** `CourseAppSheet`, `StudentLearningStatus`, `StudentManagement`, `AttendanceMakeUpSessionProjected`,
`OpData{ScheduleData,Registration,CourseInfo}`, `HSContact`, `*ReminderTrackingLog`, `StudentNote`, `DolHoliday`.

**Integrations.** Google Drive/Sheets, Zoom (webhook + sync), HubSpot, n8n (Zoom recording recovery), Customer.io, Directus,
Kafka, BigQuery, Slack. Sibling/feeder of [[course-app-sheet-api]].

**Gotchas.** Per-upstream event-loop thread pools (saturation risk if jobs overlap). Aggressive 30s query cache. Kafka `enabled:false`
in config. Google service-account JSON in resources (no rotation). Scheduler not in code (external cron triggers the REST endpoints).

## Tiếng Việt

**Một dòng.** Microservice cron/sync đồng bộ enrollment, điểm danh, feedback, lịch giữa hệ nội bộ (MongoDB/BigQuery),
Google Sheets, Zoom, HubSpot, n8n. Feed cho [[course-app-sheet-api]].

**Stack (detect).** **Micronaut 3.4.3** (Netty) / Java 17 (parent `dol-parent-v2`); MongoDB, BigQuery, Redis, Kafka (thường tắt); Prometheus + Sentry. Port 8080.

**Chức năng (command kích bằng cron).**
- **Sync course** — `GET /api/cron-job/sync-course-app-sheet-student`: enrollment từ queue → CourseAppSheet.
- **Điểm danh / vắng** — đánh vắng, xử lý make-up, auto-archive red flag.
- **Zoom** — sync registrant + webhook.
- **Final test & entrance form** — tự mở final test; email nhắc.
- **Feedback** — nhắc feedback CS/học sinh (track HubSpot).
- **Email** — email publish khoá hằng ngày + hoàn thành (Customer.io, 29 template).
- **Sync Google Sheets** — lịch/đăng ký/nhân viên/feedback.
- **Sync HubSpot contact** — học sinh, avatar.
- **Checklist** — phân công CS, deadline task khoá.
- **BigQuery analytics** — usage code DOL, số deal EC.

**Data model.** `CourseAppSheet`, `StudentLearningStatus`, `StudentManagement`, `AttendanceMakeUpSessionProjected`, `OpData*`, `HSContact`, `*ReminderTrackingLog`, `StudentNote`, `DolHoliday`.

**Tích hợp.** Google Drive/Sheets, Zoom, HubSpot, n8n, Customer.io, Directus, Kafka, BigQuery, Slack. Anh em/feeder của [[course-app-sheet-api]].

**Lưu ý.** Thread pool event-loop riêng từng upstream (rủi ro bão hoà nếu job chồng). Cache query 30s. Kafka `enabled:false`. Google SA JSON trong resources. Scheduler không nằm trong code (cron ngoài kích REST endpoint).

## Sources
- [[src-2026-06-22-doltech-standalone-survey]]
