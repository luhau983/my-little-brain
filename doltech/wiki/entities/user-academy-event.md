---
title: user-academy-event
type: entity
entity_type: project
tags: [project, doltech, events, gamification, kafka]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# user-academy-event

## English

**One-liner.** Event-tracking & gamification service for user test participation: per-user event
history, the **"Bang Vang"** (Hall of Fame) leaderboard, and academy statistics across test platforms.

**Stack.** Baseline + Kafka V2 (multi-source listeners, DLT retry).

**Features.**
- **User test event tracking** — `/api/event/{templateType}/check-status-by-id(s)`, `/fetch-test-ids-by-status`.
  Kafka ingests `receive_user_do_test_action` from 11 services (hsa, k10, k12, k12-all, online-test, page-management, sat, g12,
  virtual-exam, toeic, toeic-assignment) → upsert `UserDoTestEvent` (state IN_PROGRESS→COMPLETED, timing).
- **Bang Vang leaderboard** — `/api/bang-vang/*`: top-N per (type, templateType, questionKey), user's own rank, debut (go public),
  like/un-like. Entities `BangVang` (scores map, `tongDiem`), `BangVangReaction`, `BangVangKicked`, `BangVangReadyForDebut`.
  Fed by Kafka `cap_nhat_bang_vang_action` (virtual-exam, toeic-assignment).
- **Statistics & analytics** — `/api/event/random-user-practice` (cached 5min), user/global summaries.
- **Sync to page-management** — `/api/sync/*` via `PageManagementRestClient`.
- **Bang Vang rule engine** — `BangVangRuleUtil` / `IeltsMarkingUtil` compute `tongDiem`.

**Data model.** `user_do_test_event`, `user_do_test_summary_event`, `global_do_test_summary_event`, `bang_vang`, `bang_vang_reaction`, `bang_vang_kicked`, `bang_vang_ready_for_debut`.

**Integrations.** Kafka inbound from 11 services + 2 bang-vang topics; Feign to page-management, online-test, toeic-assignment, virtual-exam, [[practice-management]]; Redis.

**Gotchas.** Query endpoints guard `RequestUtils.isAnonymous()`. Kafka deserialization errors logged not rethrown (graceful). Bang Vang rank by (templateType, questionKey) — no enforced unique index. Closely paired with [[practice-management]] (which also consumes `completed_test`).

## Tiếng Việt

**Một dòng.** Service theo dõi event & gamification cho việc tham gia test: lịch sử event từng user, bảng **"Bảng Vàng"**
(Hall of Fame), và thống kê academy xuyên các nền tảng test.

**Stack.** Baseline + Kafka V2 (listener đa nguồn, retry DLT).

**Chức năng.**
- **Theo dõi event làm test** — `/api/event/{templateType}/check-status-by-id(s)`, `/fetch-test-ids-by-status`.
  Kafka nhận `receive_user_do_test_action` từ 11 service → upsert `UserDoTestEvent` (IN_PROGRESS→COMPLETED, thời gian).
- **Bảng Vàng leaderboard** — `/api/bang-vang/*`: top-N theo (type, templateType, questionKey), rank user, debut, like/un-like.
  Entity `BangVang` (map điểm, `tongDiem`), ... Feed từ Kafka `cap_nhat_bang_vang_action`.
- **Thống kê & phân tích** — `/api/event/random-user-practice` (cache 5 phút), summary user/global.
- **Sync sang page-management** — `/api/sync/*`.
- **Rule engine Bảng Vàng** — `BangVangRuleUtil` / `IeltsMarkingUtil` tính `tongDiem`.

**Data model.** `user_do_test_event`, `*_summary_event`, `bang_vang`, `bang_vang_reaction`, `bang_vang_kicked`, `bang_vang_ready_for_debut`.

**Tích hợp.** Kafka nhận từ 11 service + 2 topic bang-vang; Feign tới page-management, online-test, toeic-assignment, virtual-exam, [[practice-management]]; Redis.

**Lưu ý.** Endpoint query chặn `isAnonymous()`. Lỗi deserialize Kafka log chứ không rethrow. Rank theo (templateType, questionKey). Đi cặp với [[practice-management]].

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
