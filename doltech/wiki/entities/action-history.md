---
title: action-history
type: entity
entity_type: project
tags: [project, doltech, audit, tracking]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# action-history

## English

**One-liner.** Central audit & tracking service: records AI-generated content history, field-level
change history for exam explanations, and resource download metrics. Many other apps (e.g. [[g12]],
[[hsa]]) push field-change events here.

**Stack.** Baseline ([[spring-boot]] / [[mongodb]] + [[querydsl]]). Kafka bootstrap configured but no
active consumers/producers; no `@Cached` usage yet.

**Features.**
- **AI Generated History** — audit trail of AI-generated content. `POST /api/ai/generated/history/add`,
  `GET /api/ai/generated/history/{documentId}` (paginated, DESC by `lastModifiedAt`). Entity
  `AIGeneratedHistory` (`ai_generated_history`): content (Object), collectionName, dbName, documentId, reason.
- **Field Change History** — granular audit of explanation edits at question/option level.
  `POST /api/field-change-history`, `GET /api/field-change-history` (filters: questionId, documentId,
  fieldName, serviceName, optionKey, explanationType). Entity `FieldChangeHistory`: actionType
  (CREATE/UPDATE/DELETE), explanationType (LINEAR/NON_LINEAR), actionBy.
- **Download Tracking** — count + metadata for resource downloads (upsert-style increment).
  `POST /public/api/download-tracking`, `GET /public/api/download-tracking/history?path=`. Entity
  `DownloadTracking` (`download_tracking_history`): unique `path`, `downloadCount`, fileType, size, year.

**Data model.** `ai_generated_history`, `field_change_history`, `download_tracking_history` (path unique).

**Integrations.** Consumes field-change events from other apps via their `ActionHistoryRestClient`.
Kafka/cache wired but dormant.

**Gotchas.** `/api/*` = authenticated, `/public/api/*` = public. Download tracking enforces unique `path` index.

## Tiếng Việt

**Một dòng.** Service audit & tracking trung tâm: lưu lịch sử nội dung do AI sinh, lịch sử thay đổi
từng field của phần giải thích đề thi, và số liệu download tài nguyên. Nhiều app khác (vd [[g12]],
[[hsa]]) đẩy sự kiện field-change về đây.

**Stack.** Baseline ([[spring-boot]] / [[mongodb]] + [[querydsl]]). Kafka đã cấu hình nhưng chưa có
consumer/producer; chưa dùng cache.

**Chức năng.**
- **AI Generated History** — nhật ký nội dung AI sinh. `POST /api/ai/generated/history/add`,
  `GET /api/ai/generated/history/{documentId}` (phân trang). Entity `AIGeneratedHistory`.
- **Field Change History** — audit chi tiết chỉnh sửa giải thích ở mức câu hỏi/đáp án.
  `POST` + `GET /api/field-change-history` (lọc nhiều tham số). Lưu actionType (CREATE/UPDATE/DELETE),
  explanationType (LINEAR/NON_LINEAR), người sửa.
- **Download Tracking** — đếm + metadata lượt tải (kiểu upsert, tăng đếm).
  `POST` / `GET /public/api/download-tracking`. Entity `DownloadTracking`, `path` là unique index.

**Data model.** 3 collection: `ai_generated_history`, `field_change_history`, `download_tracking_history`.

**Tích hợp.** Nhận field-change từ app khác qua `ActionHistoryRestClient`. Kafka/cache đã nối nhưng chưa dùng.

**Lưu ý.** `/api/*` cần auth, `/public/api/*` công khai. `path` unique cho download tracking.

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
