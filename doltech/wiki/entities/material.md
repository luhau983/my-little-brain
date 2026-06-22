---
title: material
type: entity
entity_type: project
tags: [project, doltech, content, learning, course]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# material

## English

**One-liner.** Learning-content service for **BLOG / VIDEO / PDF** materials: authoring + publishing,
student progress tracking with practice cloning, and cross-course learning analytics.

**Stack.** Baseline. Hexagonal layout (`adapter`/`port`/`domain`). Kafka events to `academic-resource-interaction`.

**Features.**
- **Material CRUD & publishing** — `/material/*`: create/edit/delete/clone/publish, `publish-for` (NOBODY/PUBLIC/
  COURSE/SCHOOL), edit-progress steps (BASIC→ADVANCED→COMPLETE). Polymorphic `Material` (Blog/Video/PDF) in one collection;
  auto display IDs (`BLOG_001`…).
- **Type-specific authoring** — `/material/{video,blog,pdf}`: CRUD + embedded questions; per-type filter & question delete.
- **Student progress** — `/material/student/progress/{id}/{start,finish,tracking,detail}`: clones practice questions on start,
  scores on finish, publishes START/PROGRESS/SUBMIT/COMPLETE events. Entities `UserMaterial`, `UserMaterialQuestionAnswer`, `TrialStats`.
- **Public trial sessions** — `/public/material/...` via `trialSessionId` (no enrollment).
- **Teacher analytics** — `/material/teacher/course/*`: resource overview, completion, per-student tracking, remove-resource.
- **Cross-course merge** — `hsContactId` (HubSpot contact) joins a student's progress across enrollments.
- **Concurrent edit tracking** — `track-edit` registers the editing user (`ResourceTrackingEdit`).

**Data model.** `material`, `practiceMaterial`, `question`, `practiceQuestion`, `userMaterial`, `userMaterialQuestionAnswer`, `trialStats`, `resourceTrackingEdit`.

**Integrations.** coursesupporter (course/student helpers), Elastic search, course-app-sheet, document-history, offline-course-management, user-service; Kafka `academic-resource-interaction`, Redis.

**Gotchas.** Practice **cloning** per attempt (captures `originalId`+version). `used=true` blocks delete (RESOURCE_USED).
`hsContactId` null on pre-deploy rows until backfill. Stats logic is material-type-sensitive.

## Tiếng Việt

**Một dòng.** Service nội dung học **BLOG / VIDEO / PDF**: soạn + publish, theo dõi tiến độ học sinh (clone practice),
và phân tích học tập xuyên khoá.

**Stack.** Baseline. Kiến trúc hexagonal (`adapter`/`port`/`domain`). Kafka event tới `academic-resource-interaction`.

**Chức năng.**
- **CRUD & publish material** — `/material/*`: tạo/sửa/xoá/clone/publish, `publish-for` (NOBODY/PUBLIC/COURSE/SCHOOL),
  bước soạn (BASIC→ADVANCED→COMPLETE). `Material` đa hình (Blog/Video/PDF) chung 1 collection; auto id (`BLOG_001`…).
- **Soạn theo loại** — `/material/{video,blog,pdf}`: CRUD + câu hỏi nhúng; lọc & xoá câu hỏi theo loại.
- **Tiến độ học sinh** — `/material/student/progress/{id}/{start,finish,tracking,detail}`: clone câu hỏi practice khi start,
  chấm khi finish, publish event START/PROGRESS/SUBMIT/COMPLETE. Entity `UserMaterial`, `UserMaterialQuestionAnswer`, `TrialStats`.
- **Trial công khai** — `/public/material/...` qua `trialSessionId` (không cần ghi danh).
- **Phân tích giáo viên** — `/material/teacher/course/*`: tổng quan resource, tỉ lệ hoàn thành, tracking từng học sinh, gỡ resource.
- **Gộp xuyên khoá** — `hsContactId` (HubSpot) nối tiến độ học sinh qua nhiều khoá.
- **Tracking sửa đồng thời** — `track-edit` ghi user đang sửa (`ResourceTrackingEdit`).

**Data model.** `material`, `practiceMaterial`, `question`, `practiceQuestion`, `userMaterial`, `userMaterialQuestionAnswer`, `trialStats`, `resourceTrackingEdit`.

**Tích hợp.** coursesupporter, Elastic, course-app-sheet, document-history, offline-course-management, user-service; Kafka, Redis.

**Lưu ý.** **Clone** practice mỗi lần làm (giữ `originalId`+version). `used=true` chặn xoá. `hsContactId` null ở row cũ tới khi backfill.

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
