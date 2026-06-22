---
title: billing
type: entity
entity_type: project
tags: [project, doltech, billing, subscription, payment]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# billing

## English

**One-liner.** Subscription lifecycle, billing, and feature-access control for DolEnglish.
Orchestrates **FlexPrice** (payment SaaS, source of truth for customers/subscriptions), with
[[mongodb|MongoDB]] caching plan/feature/meter/entitlement data, Kafka webhooks, and employee-premium sync.

**Stack.** Baseline + FlexPrice external API, Kafka V2, Feign clients (Directus, Membership, FlexPrice).

**Features.**
- **Customer management** — `/api/v1/customers/*`: info-by-email, credit-history, add/cancel/extend
  subscription, list subscriptions, free-pool remaining. Customer data lives in FlexPrice (no local entity).
- **Subscription management** — `/api/v1/customer-subscriptions/*`: current user detail, **stacked days**
  (cumulative subscription credits across overlapping plans), paged search, event history. Entity `PlanStackedDay`.
- **Plans** — `/api/v1/plans/all` + migration endpoints. Plan/Entitlement/Price/Feature/Meter migrated from
  FlexPrice → MongoDB; runtime reads from MongoDB. See MIGRATION_GUIDE.md.
- **Feature access control** — `POST /api/features/check-access`: validates paid access + returns usage summary.
- **Event tracking** — `POST /api/events/send` (metered events → FlexPrice), `GET /events/last-users`.
  Local `CustomerEvent` collection backfilled async.
- **Webhook processing** — `POST /api/webhooks/flexprice` → Kafka topic `billing.listen_all_webhooks` →
  `FlexPriceWebhookListener` → `WebhookEventProcessorFactory` (per event type: customer/subscription/invoice/payment…).
- **Payment** — event-driven: `ManualSubscriptionAddedEvent` → `SubscriptionPaymentListener` creates payment
  via FlexPrice (retry w/ backoff).
- **Employee premium** — `/api/v1/employee-premium/*`: sync from Directus + Membership, paged snapshots, bulk-extend.

**Data model.** `plan`, `entitlement`, `price`, `feature`, `meter`, `plan_stacked_day`, `customer_event`, `employee_premium`.

**Integrations.** FlexPrice (payments), Directus (employees), Membership (premium/DP), Kafka, Restate, Redis cache.

**Gotchas.** Email is the primary identifier (→ external_customer_id). Dual source of truth: FlexPrice (txns) +
MongoDB (plans/events/snapshots). Stacked-days model excludes DOL_REVIEW/REFERRAL plan types from user views.

## Tiếng Việt

**Một dòng.** Quản lý vòng đời subscription, thanh toán, và kiểm soát quyền truy cập tính năng cho DolEnglish.
Điều phối **FlexPrice** (SaaS thanh toán, nguồn sự thật cho customer/subscription), dùng [[mongodb|MongoDB]]
cache dữ liệu plan/feature/meter/entitlement, webhook qua Kafka, và đồng bộ premium nhân viên.

**Stack.** Baseline + FlexPrice API ngoài, Kafka V2, Feign client (Directus, Membership, FlexPrice).

**Chức năng.**
- **Quản lý customer** — `/api/v1/customers/*`: tra cứu theo email, lịch sử credit, thêm/huỷ/gia hạn subscription,
  free-pool. Dữ liệu customer nằm ở FlexPrice (không lưu local).
- **Quản lý subscription** — `/api/v1/customer-subscriptions/*`: chi tiết user hiện tại, **stacked days** (số ngày
  tích luỹ từ nhiều plan chồng nhau), search phân trang, lịch sử event. Entity `PlanStackedDay`.
- **Plans** — `/api/v1/plans/all` + endpoint migration. Plan/Entitlement/Price/Feature/Meter migrate từ FlexPrice
  sang MongoDB; runtime đọc từ MongoDB.
- **Kiểm soát quyền tính năng** — `POST /api/features/check-access`: kiểm tra đã trả phí + trả usage summary.
- **Theo dõi event** — `POST /api/events/send` (event đo lường → FlexPrice), `GET /events/last-users`. Collection
  `CustomerEvent` backfill bất đồng bộ.
- **Xử lý webhook** — `POST /api/webhooks/flexprice` → Kafka `billing.listen_all_webhooks` → listener →
  `WebhookEventProcessorFactory` (theo loại event).
- **Thanh toán** — hướng sự kiện: `ManualSubscriptionAddedEvent` → tạo payment qua FlexPrice (retry backoff).
- **Employee premium** — `/api/v1/employee-premium/*`: sync từ Directus + Membership, snapshot phân trang, bulk-extend.

**Data model.** `plan`, `entitlement`, `price`, `feature`, `meter`, `plan_stacked_day`, `customer_event`, `employee_premium`.

**Tích hợp.** FlexPrice (thanh toán), Directus (nhân viên), Membership (premium/DP), Kafka, Restate, Redis.

**Lưu ý.** Email là định danh chính (→ external_customer_id). Hai nguồn sự thật: FlexPrice (giao dịch) + MongoDB
(plan/event/snapshot). Stacked-days loại trừ plan kiểu DOL_REVIEW/REFERRAL khỏi view của user.

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
