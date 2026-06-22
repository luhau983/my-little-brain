---
title: offline-course-management
type: entity
entity_type: project
tags: [project, doltech, course, offline, standalone]
created: 2026-06-22
updated: 2026-06-22
status: stub
source_count: 1
sources: ["[[src-2026-06-22-doltech-standalone-survey]]"]
---

# offline-course-management

## English

> ⚠️ **STUB** — the Explore agent repeatedly cost-paused without returning a full read. This page is
> assembled from cross-references + partial stack detection. **Flagged for re-ingest.**

**One-liner.** Manages **offline / in-person (classroom) courses** — the central service other apps
push course progress/completion to and read offline-course data from.

**Stack (detected, partial).** Java / **Micronaut** (Maven `pom.xml`, `micronaut-cli.yml`).

**Known role (from references).** Acts as the offline-course hub:
- [[sat-service]] syncs academy progress here (REST-first, Kafka failover).
- [[material]], [[exercise-v2]], [[assignment-service]] integrate for offline-course data/sync.
- Likely manages classroom enrolments, schedules, and offline learning records.

**TODO (re-ingest).** Features/endpoints, data model (collections), exact integrations & messaging topics.

## Tiếng Việt

> ⚠️ **STUB** — agent Explore dừng vì cost 3 lần, chưa đọc đủ. Page này ghép từ cross-reference + detect
> stack 1 phần. **Cần ingest lại.**

**Một dòng.** Quản lý **khoá học offline / trực tiếp (lớp học)** — service trung tâm mà các app khác đẩy
tiến độ/hoàn thành khoá về và đọc dữ liệu offline-course.

**Stack (detect, 1 phần).** Java / **Micronaut** (Maven `pom.xml`, `micronaut-cli.yml`).

**Vai trò đã biết (từ tham chiếu).**
- [[sat-service]] sync academy progress về đây (REST-first, Kafka failover).
- [[material]], [[exercise-v2]], [[assignment-service]] tích hợp lấy/sync dữ liệu offline-course.
- Khả năng quản lý ghi danh lớp, lịch, hồ sơ học offline.

**TODO (ingest lại).** Feature/endpoint, data model, tích hợp & topic chính xác.

## Sources
- [[src-2026-06-22-doltech-standalone-survey]]
