---
title: hsa
type: entity
entity_type: project
tags: [project, doltech, exam, university-entrance, ai]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# hsa

## English

**One-liner.** Exam platform for Vietnamese university-entrance assessments (VNU Hanoi, VNU HCM, HUST):
exam authoring, full/section/practice test execution, progress & scoring, AI explanation generation,
sheet import/export, and change-history audit.

**Stack.** Baseline + Google Sheets, Directus, AI queue, S3/CDN.

**Features.**
- **Exam test management** — `/api/hsa/exam/*`: create/update/clone/publish/publish-for/delete, bulk mark-used,
  paged (filters: examType, year, schoolType, sectionType, testType, topicType). Entity `HSAExamTest` (`examTest`),
  `QuestionGroup`, `SubQuestionEntryOptionBase`, linear/non-linear explanations.
- **Full exams (multi-section)** — `/api/hsa/exam-full/*` (admin) + `/api/public/do-test/full/*`: start, save section,
  submit, force-reset, check-answer, extend-time, change-mode. Entities `HSAExamFullTest`, `UserExamFullTestProgress`.
- **Practice/section tests** — `/api/public/do-test/practice/*` and `/section/*`: start/save/submit/check-answer/extend.
  Entities `UserExamTest(Progress)`, `UserSectionTest(Progress)`.
- **AI explanation generation** — `/api/hsa/hook/*`: receive result, queue-status, retry-one/all, import. External AI queue;
  school/section choose prompt + explanation type.
- **Sheet import/export** — `/api/hsa/sheet/queue` (Google Sheets import), `/api/public/sheet/export` (Apache POI).
- **Change history** — `HSAExamTestListener` (Mongo BeforeSave) → `ActionHistoryRestClient` → [[action-history]].
- **Common/landing/SEO/sync** — test activity counter, academy landing progress overview, question SEO, initial-history sync.

**Data model.** `examTest`, `examFullTest`, `*Version`, `userExamTest(Progress)`, `userExamFullTest(Progress)`,
`userSectionTest(Progress)`, `testActivityCounter`.

**Integrations.** AI service (webhook), Google Sheets, Directus, [[action-history]], Kafka/V2, S3/CDN, email.

**Gotchas.** Special-case rules per school (`isSpecialCaseOfHN()`, `isMatchBKHN()`). Explanation types LINEAR vs
NONE_LINEAR chosen by school/section. `HSAExamTest` = single section, `HSAExamFullTest` = multi-section bundle. Versioned docs.

## Tiếng Việt

**Một dòng.** Nền tảng thi đánh giá năng lực xét tuyển đại học (ĐHQG Hà Nội, ĐHQG HCM, Bách Khoa HN): soạn đề,
làm bài full/section/practice, tiến độ & chấm điểm, AI sinh giải thích, import/export sheet, và audit lịch sử thay đổi.

**Stack.** Baseline + Google Sheets, Directus, AI queue, S3/CDN.

**Chức năng.**
- **Quản lý đề thi** — `/api/hsa/exam/*`: tạo/sửa/clone/publish/delete, mark-used, phân trang (lọc theo examType,
  năm, schoolType, sectionType...). Entity `HSAExamTest`, `QuestionGroup`, giải thích linear/non-linear.
- **Đề full (nhiều phần)** — `/api/hsa/exam-full/*` + `/api/public/do-test/full/*`: start, lưu từng section, submit,
  force-reset, check-answer, extend-time, change-mode. Entity `HSAExamFullTest`, `UserExamFullTestProgress`.
- **Practice/section test** — `/api/public/do-test/practice|section/*`: start/save/submit/check-answer/extend.
- **AI sinh giải thích** — `/api/hsa/hook/*`: nhận kết quả, queue-status, retry, import. Queue AI ngoài; chọn prompt
  + loại giải thích theo trường/section.
- **Import/export sheet** — `/api/hsa/sheet/queue` (import Google Sheets), `/api/public/sheet/export` (Apache POI).
- **Lịch sử thay đổi** — `HSAExamTestListener` → [[action-history]].
- **Common/landing/SEO/sync** — đếm hoạt động test, tổng quan tiến độ landing, SEO câu hỏi, sync lịch sử ban đầu.

**Data model.** `examTest`, `examFullTest`, `*Version`, `userExamTest(Progress)`, `userExamFullTest(Progress)`,
`userSectionTest(Progress)`, `testActivityCounter`.

**Tích hợp.** AI service (webhook), Google Sheets, Directus, [[action-history]], Kafka/V2, S3/CDN, email.

**Lưu ý.** Quy tắc đặc thù theo trường (`isSpecialCaseOfHN()`, `isMatchBKHN()`). Loại giải thích LINEAR/NONE_LINEAR
chọn theo trường/section. `HSAExamTest` = 1 section, `HSAExamFullTest` = bộ nhiều section. Tài liệu có version.

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
