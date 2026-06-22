---
title: practice-management
type: entity
entity_type: project
tags: [project, doltech, analytics, kafka, practice]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# practice-management

## English

**One-liner.** Student practice tracking & learning analytics: ingests completed-test events from **9
exam systems** via Kafka, computes daily streaks, skill scores, learning targets, and denormalized
landing-page leaderboards. Multi-site aware (IELTS/TOEIC/SAT/K12/DGNL).

**Stack.** Baseline + Kafka V2 (9-topic listener), heavy MongoDB aggregation. Data-intensive.

**Features.**
- **Practice bank** — `/api/practice-bank/*`: bookmark/like tests, status check, "your-practice" paged (system/skill/status/search).
  Entities `UserPracticeBank`, `UserPracticeLike`.
- **Practice history & analytics** — Kafka ingest → `UserPracticeHistory` → analyze queue → `UserPracticeHistoryAnalyze` →
  denormalize to `CompletedTest` (unique `{testId,email}`). Sync/backfill endpoints `/api/sync/*`, `/api/background-job/*`.
- **Streaks** — `/api/streak/overview*`: current/best streak, daily/weekly/monthly breakdown; gap >2 days resets. Entities `UserStreak`, `UserDailyStreak`.
- **Targets & projected exam dates** — `/api/target/{system}`, `/api/projected-exam-date/{system}`: target skill scores,
  exam-date projections. Entities `UserTarget`, `UserProjectedExamDate`, `ExamDateCfg`.
- **Skill statistics** — `/api/statistic/*`: current skills, global averages, practice navigation, daily volume.
- **Landing overview** — `/api/landing-overview/test-completion`: distinct completers, random sample, viewer rank.
- **Site config & sync** — `/api/site-config/config`, retry-analyze; multi-site tagging via `CusSiteManagementHelper`.

**Data model.** `user_practice_bank`, `user_practice_like`, `user_practice_history(_analyze)(_queue)`, `completed_test`
(unique testId+email), `user_streak`, `user_daily_streak`, `user_daily_statistic`, `user_target`, `user_projected_exam_date`, `exam_date_cfg`, `test_summary`.

**Integrations.** Kafka inbound from [[g12]], [[hsa]], [[k10]], [[k12-all-subject]], toeic, sat, virtual-exam, online-test,
toeic-assignment (`*.completed_test`); Feign clients to those services for test metadata; user-service.

**Gotchas.** `dateKey` is `YYYY-MM-DD` string (not datetime). **Every save must carry the `site` tag** (`SiteContext`) or
data corrupts. Only `analyzed=true` results count in landing/leaderboards. `latestAttempt` flag + idempotent `CompletedTest` upsert.
`appendToOverall` controls whether a test counts toward overall rank. Kafka listener swallows errors (resilience).

## Tiếng Việt

**Một dòng.** Theo dõi luyện tập & phân tích học tập: nhận event hoàn thành bài từ **9 hệ thống thi** qua Kafka, tính
streak ngày, điểm kỹ năng, mục tiêu học, và bảng xếp hạng landing (denormalized). Đa site (IELTS/TOEIC/SAT/K12/DGNL).

**Stack.** Baseline + Kafka V2 (listener 9 topic), aggregation MongoDB nặng.

**Chức năng.**
- **Practice bank** — `/api/practice-bank/*`: bookmark/like, check trạng thái, "your-practice" phân trang. Entity `UserPracticeBank`, `UserPracticeLike`.
- **Lịch sử & phân tích** — Kafka ingest → `UserPracticeHistory` → hàng đợi analyze → `UserPracticeHistoryAnalyze` →
  denormalize sang `CompletedTest`. Endpoint sync/backfill `/api/sync/*`, `/api/background-job/*`.
- **Streak** — `/api/streak/overview*`: streak hiện tại/tốt nhất, breakdown ngày/tuần/tháng; gap >2 ngày reset.
- **Mục tiêu & ngày thi dự kiến** — `/api/target/{system}`, `/api/projected-exam-date/{system}`. Entity `UserTarget`, `UserProjectedExamDate`, `ExamDateCfg`.
- **Thống kê kỹ năng** — `/api/statistic/*`: kỹ năng hiện tại, trung bình global, điều hướng luyện, volume ngày.
- **Landing overview** — `/api/landing-overview/test-completion`: số người hoàn thành, mẫu ngẫu nhiên, rank người xem.
- **Site config & sync** — `/api/site-config/config`, retry-analyze; gắn site qua `CusSiteManagementHelper`.

**Data model.** `user_practice_history(_analyze)(_queue)`, `completed_test` (unique testId+email), `user_streak`,
`user_daily_streak`, `user_daily_statistic`, `user_target`, `user_projected_exam_date`, `exam_date_cfg`, `test_summary`, `user_practice_bank/like`.

**Tích hợp.** Kafka nhận từ [[g12]], [[hsa]], [[k10]], [[k12-all-subject]], toeic, sat, virtual-exam, online-test,
toeic-assignment (`*.completed_test`); Feign tới các service đó lấy metadata; user-service.

**Lưu ý.** `dateKey` là chuỗi `YYYY-MM-DD`. **Mọi save phải mang tag `site`** (`SiteContext`) nếu không hỏng dữ liệu.
Chỉ kết quả `analyzed=true` mới tính vào landing/leaderboard. Cờ `latestAttempt` + upsert `CompletedTest` idempotent.
`appendToOverall` quyết định bài có tính vào rank tổng. Listener Kafka nuốt lỗi (resilience).

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
