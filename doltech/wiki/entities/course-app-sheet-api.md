---
title: course-app-sheet-api
type: entity
entity_type: project
tags: [project, doltech, course, metadata, micronaut, standalone]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-standalone-survey]]"]
---

# course-app-sheet-api

## English

**One-liner.** REST API for **course/sheet metadata** — the service most exam apps call for course,
class, student-registration, and teacher info. Bridges Google Sheets, BigQuery, MongoDB, HubSpot, Zalo.

**Stack (detected).** **Micronaut 3.4.3 + Undertow** / Java 17 / Maven (parent `dol-parent-v2`); MongoDB (replica set),
**Google BigQuery**, Redis (Lettuce); Kafka (consumers `dol-event`, `course-app-sheet-self`); serde + mongodb-data processors.

**Features (partial read — needs deeper re-ingest).**
- **Course/sheet metadata API** — serves course, sub-class, registration, teacher data to other apps (cached, called via their Feign clients).
- **Google Sheets ↔ data sync** — operational data backed by Google Sheets.
- **BigQuery analytics** — `xenon-heading-309906.dolenglish` dataset.
- **HubSpot sync** — contacts (accounts 21448405, UEF 47430100).
- **Zalo ZNS notifications** — 9 templates (attendance, feedback, tests, scheduling).

**Data model.** Course/sheet domain models under `vn.dolenglish.courseappsheet` (entities not fully read — re-ingest).

**Integrations.** Google Drive/Sheets, BigQuery, HubSpot, Customer.io, n8n (Zoom sync), Zalo ZNS, AWS S3, Kafka, Redis.
**Heavily consumed** by [[memories]], [[material]], [[assignment-service]], [[pd-management]], and most course-aware apps.

**Gotchas.** Custom Micronaut `SEARCH` HTTP method used by callers. Plaintext creds in config. Prod Mongo at `mongo-prod-course-mongodb`.
Partial read — full feature/endpoint map pending re-ingest.

## Tiếng Việt

**Một dòng.** REST API **metadata course/sheet** — service mà hầu hết app thi gọi để lấy thông tin khoá, lớp,
đăng ký học sinh, giáo viên. Cầu nối Google Sheets, BigQuery, MongoDB, HubSpot, Zalo.

**Stack (detect).** **Micronaut 3.4.3 + Undertow** / Java 17 (parent `dol-parent-v2`); MongoDB, **BigQuery**, Redis; Kafka (consumer `dol-event`, `course-app-sheet-self`).

**Chức năng (đọc 1 phần — cần ingest sâu lại).**
- **API metadata course/sheet** — cấp dữ liệu course/sub-class/registration/teacher cho app khác (cached, gọi qua Feign client của họ).
- **Sync Google Sheets ↔ data** — dữ liệu vận hành nền Google Sheets.
- **BigQuery analytics** — dataset `xenon-heading-309906.dolenglish`.
- **Sync HubSpot** — contact.
- **Zalo ZNS** — 9 template (điểm danh, feedback, test, lịch).

**Data model.** Domain course/sheet trong `vn.dolenglish.courseappsheet` (chưa đọc đủ entity — ingest lại).

**Tích hợp.** Google Drive/Sheets, BigQuery, HubSpot, Customer.io, n8n (Zoom), Zalo ZNS, AWS S3, Kafka, Redis.
**Được gọi nhiều** bởi [[memories]], [[material]], [[assignment-service]], [[pd-management]], và hầu hết app có khoá học.

**Lưu ý.** Dùng HTTP method `SEARCH` tuỳ biến của Micronaut. Creds plaintext. Mongo prod `mongo-prod-course-mongodb`. Đọc 1 phần — bản đồ endpoint đầy đủ chờ ingest lại.

## Sources
- [[src-2026-06-22-doltech-standalone-survey]]
