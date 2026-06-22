---
title: "Spring-monorepo — Feature Matrix"
type: synthesis
tags: [doltech, spring-monorepo, feature-matrix, comparison]
created: 2026-06-22
updated: 2026-06-22
status: active
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# Spring-monorepo — Feature Matrix

> Cross-app capability comparison of the **24 spring-monorepo applications**, synthesized from their
> per-app wiki pages (not a fresh code audit). ✓ = capability is a documented feature; blank = not present / n.a.

## English

### Capability matrix

| App | Author | DoTest | AI-Expl | AI-Mark | Sheet | Course | Kafka | Hist→[[action-history]] | SEO | Rank/Stats |
|-----|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| [[g12]] | ✓ | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [[k12]] | ✓ | ✓ | ✓ |  | ✓ | ✓ |  | ✓ |  | ✓ |
| [[k12-all-subject]] | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |
| [[hsa]] | ✓ | ✓ | ✓ |  | ✓ |  | ✓ | ✓ | ✓ | ✓ |
| [[k10]] | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |  |  | ✓ |
| [[toeic]] | ✓ | ✓ | ✓ |  | ✓ | ✓ | ✓ |  |  | ✓ |
| [[toeic-assignment]] | ✓ | ✓ |  | ✓ |  |  | ✓ |  | ✓ |  |
| [[virtual-exam]] | ✓ | ✓ |  | ✓ |  | ✓ | ✓ |  |  | ✓ |
| [[young-learners-english]] | ✓ | ✓ |  | ✓ |  |  | ✓ |  |  | ✓ |
| [[junior]] | ✓ | ✓ |  | ✓ |  |  |  |  |  |  |
| [[mental-model]] | ✓ | ✓ |  |  |  | ✓ | ✓ |  |  | ✓ |
| [[study-hub]] | ✓ | ✓ |  |  |  | ✓ |  |  |  |  |
| [[ev-dictionary]] | ✓ |  | ✓ |  | ✓ |  |  |  |  |  |
| [[grammar]] | ✓ |  |  |  |  | ✓ |  |  | ✓ |  |
| [[material]] | ✓ | ✓ |  |  |  | ✓ | ✓ |  |  | ✓ |
| [[memories]] | ✓ |  |  |  |  | ✓ |  |  |  | ✓ |
| [[practice-management]] |  |  |  |  |  |  | ✓ |  |  | ✓ |
| [[user-academy-event]] |  |  |  |  |  |  | ✓ |  |  | ✓ |
| [[pd-management]] |  |  |  |  |  |  | ✓ |  |  | ✓ |
| [[billing]] |  |  |  |  |  |  | ✓ |  |  |  |
| [[seo-redirect]] |  |  |  |  | ✓ |  |  |  | ✓ |  |
| [[me-invoice]] |  |  |  |  |  |  |  |  |  |  |
| [[referral]] |  |  |  |  |  |  |  |  |  |  |
| [[action-history]] | — | — | — | — | — | — | — | (sink) | — | — |

**Legend.** Author = content authoring/CRUD · DoTest = student test execution · AI-Expl = AI explanation
generation · AI-Mark = AI speaking/writing marking · Sheet = Google-Sheets/Excel import · Course =
course/classroom integration (`coursesupporter`) · Kafka = event publish/consume · Hist = change-history
to [[action-history]] · SEO = SEO/landing/public pages · Rank = analytics/ranking/leaderboard.

### Observations
- **~12 exam/test platforms** share the same backbone: Author + DoTest + EditableDocument versioning +
  [[cqrs-command-query|CQRS-lite]] + [[predicate-pattern|PredicateBuilder]] queries. That uniformity is the
  monorepo's whole point.
- **AI splits two ways:** *explanation-generation* (g12, k12, k12-all, hsa, k10, toeic, ev-dictionary) vs
  *speaking/writing marking* (junior, k10, k12-all, toeic-assignment, virtual-exam, young-learners-english).
  The marking apps increasingly run it through **Restate** (k12-all, toeic-assignment, virtual-exam, YLE).
- **Event backbone:** test apps emit `completed_test`/do-test events on Kafka → consumed by
  [[practice-management]] (analytics/streaks) and [[user-academy-event]] (Bang Vang leaderboard). These two
  are pure consumers (no authoring/do-test of their own).
- **Change-history** (g12, hsa, k12, k12-all) flows to [[action-history]] via `ActionHistoryRestClient` — it's the audit sink.
- **Non-exam domain apps:** [[billing]] (payments), [[me-invoice]] (e-invoice), [[referral]] (referral programs),
  [[seo-redirect]] (redirects), [[memories]] (media), [[grammar]]/[[ev-dictionary]] (content+SEO). They don't fit the test backbone.
- **Sheet import** (Google Sheets/Excel) is the standard content-ingestion path for exam authoring (g12, k12, k12-all, hsa, k10, toeic, ev-dictionary).

## Tiếng Việt

Bảng ma trận ở trên dùng chung (tên app + ✓). Chú giải cột: **Author** = soạn/CRUD nội dung · **DoTest** =
học sinh làm bài · **AI-Expl** = AI sinh giải thích · **AI-Mark** = AI chấm speaking/writing · **Sheet** =
import Google Sheets/Excel · **Course** = tích hợp khoá/lớp (`coursesupporter`) · **Kafka** = publish/consume
event · **Hist** = đẩy change-history về [[action-history]] · **SEO** = trang SEO/landing/public · **Rank** =
analytics/xếp hạng/leaderboard.

### Nhận xét
- **~12 nền tảng thi** chung một "xương sống": Author + DoTest + versioning EditableDocument + [[cqrs-command-query|CQRS-lite]]
  + query [[predicate-pattern|PredicateBuilder]]. Sự đồng nhất này chính là lý do tồn tại của monorepo.
- **AI chia 2 nhánh:** *sinh giải thích* (g12, k12, k12-all, hsa, k10, toeic, ev-dictionary) vs *chấm speaking/writing*
  (junior, k10, k12-all, toeic-assignment, virtual-exam, young-learners-english). Nhánh chấm ngày càng chạy qua **Restate**.
- **Xương sống sự kiện:** app thi phát `completed_test`/do-test event qua Kafka → [[practice-management]] (analytics/streak)
  và [[user-academy-event]] (leaderboard Bảng Vàng) tiêu thụ. Hai app này thuần consumer.
- **Change-history** (g12, hsa, k12, k12-all) đổ về [[action-history]] qua `ActionHistoryRestClient` — sink audit.
- **App domain khác (không phải thi):** [[billing]], [[me-invoice]], [[referral]], [[seo-redirect]], [[memories]],
  [[grammar]]/[[ev-dictionary]]. Không khớp xương sống thi.
- **Sheet import** là đường nạp nội dung chuẩn khi soạn đề (g12, k12, k12-all, hsa, k10, toeic, ev-dictionary).

> Lưu ý: ma trận suy ra từ các page wiki từng app (không phải audit code lại). ✓ = chức năng đã được ghi nhận; trống = không có / không áp dụng.

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
