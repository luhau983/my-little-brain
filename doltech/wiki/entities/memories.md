---
title: memories
type: entity
entity_type: project
tags: [project, doltech, media, course, workflow]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# memories

## English

**One-liner.** Course media-memory archive: students/teachers/EC upload photos & videos with an
approval workflow, per-course statistics, role-specific feeds, and a public course gallery.

**Stack.** Baseline (synchronous — **no Kafka/Restate** observed).

**Features.**
- **Media upload & management** — `POST /api/save`, `/api/detail/list`, `GET /api/{id}/detail`. Entity `MemoriesMedia`
  (FileInfoDTO, MediaType, status, courseId, uploadedByUserType); history on status change.
- **Approval workflow (EC portal)** — `/api/ec/*`: paged by status, approve/reject(+reason)/delete, uploader profiles.
  Transitions validated by `MemoriesUtils`. History `memoriesMediaHistory`.
- **Course statistics** — `/api/course/{id}/statistic`, batch list, paged, `recalculate`. Entity `CourseMemories`
  (`mediaStatistic`: waiting/approved/rejected counts).
- **Multi-role feeds** — `/api/student/paged`, `/api/teacher/paged`: query groups (ALL/ME/DOL_USER/ANOTHER_USER/FROM_STUDENT).
- **Public course gallery** — `/api/courses/paged`: rich filters; joins course metadata via course-app-sheet (cached).

**Data model.** `memoriesMedia`, `courseMemories`, `userCourseMemories`, `memoriesMediaHistory`. Enums: status
(WAITING_FOR_APPROVAL/APPROVED/REJECTED/DELETED), UserUploaded (STUDENT/TEACHER/EC), MediaType (IMAGE/VIDEO).

**Integrations.** course-app-sheet (course/registration metadata, cached Feign), user-service (uploader profiles), MongoDB, Redis, Prometheus.

**Gotchas.** Status transitions are rule-checked (e.g. APPROVE only from WAITING/REJECTED). Student uploads need
`studentRegistrationKey` (auto-fetched). **Known bug:** `CourseMemories.calMediaStatistic` swaps image/video counts.

## Tiếng Việt

**Một dòng.** Kho media kỷ niệm khoá học: học sinh/giáo viên/EC upload ảnh & video với luồng duyệt, thống kê theo khoá,
feed theo vai trò, và gallery khoá học công khai.

**Stack.** Baseline (đồng bộ — **không thấy Kafka/Restate**).

**Chức năng.**
- **Upload & quản lý media** — `POST /api/save`, `/api/detail/list`, `GET /api/{id}/detail`. Entity `MemoriesMedia`;
  ghi history khi đổi trạng thái.
- **Luồng duyệt (cổng EC)** — `/api/ec/*`: phân trang theo trạng thái, duyệt/từ chối(+lý do)/xoá, hồ sơ người upload.
  Chuyển trạng thái được validate bởi `MemoriesUtils`. History `memoriesMediaHistory`.
- **Thống kê khoá** — `/api/course/{id}/statistic`, batch, phân trang, `recalculate`. Entity `CourseMemories`.
- **Feed theo vai trò** — `/api/student/paged`, `/api/teacher/paged`: nhóm query (ALL/ME/DOL_USER/ANOTHER_USER/FROM_STUDENT).
- **Gallery công khai** — `/api/courses/paged`: nhiều bộ lọc; join metadata khoá qua course-app-sheet (cache).

**Data model.** `memoriesMedia`, `courseMemories`, `userCourseMemories`, `memoriesMediaHistory`.

**Tích hợp.** course-app-sheet (cached Feign), user-service, MongoDB, Redis, Prometheus.

**Lưu ý.** Chuyển trạng thái có rule (vd APPROVE chỉ từ WAITING/REJECTED). Upload của học sinh cần `studentRegistrationKey`
(tự lấy). **Bug đã ghi nhận:** `CourseMemories.calMediaStatistic` đếm lẫn ảnh/video.

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
