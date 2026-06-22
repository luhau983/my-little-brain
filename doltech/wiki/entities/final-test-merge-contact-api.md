---
title: final-test-merge-contact-api
type: entity
entity_type: project
tags: [project, doltech, hubspot, bigquery, micronaut, micronaut-monorepo]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-tier3-survey]]"]
---

# final-test-merge-contact-api

## English

**One-liner.** Contact **merge & sync** service integrating HubSpot with BigQuery for dedup and avatar
validation/repair. Micronaut-monorepo app.

**Stack (detected).** Micronaut / Java 17 (Undertow); MongoDB, BigQuery, HubSpot API, Kafka, QueryDSL.

**Features.**
- **Contact merge sync** — `POST /api/contact-merge/sync`: sync merged contacts from BigQuery (configurable lookback hours). CQRS command.
- **Broken-avatar scan** — `POST /api/contact-merge/scan-broken-avatar`: scan + repair broken avatar URLs (configurable day range).
- HubSpot REST + Kafka event publishing.

**Data model.** `HSContact` (from dol-common-model-hubspot); HubSpot→MongoDB mappers.

**Integrations.** HubSpot API, Google Cloud BigQuery, Kafka, MongoDB.

**Gotchas.** QueryDSL 4.3.1; custom annotation processors (serde, mongodb-data) at compile. Avatar cleanup is time-windowed.

## Tiếng Việt

**Một dòng.** Service **merge & sync contact** tích hợp HubSpot với BigQuery để dedup và validate/sửa avatar. App micronaut-monorepo.

**Stack (detect).** Micronaut / Java 17; MongoDB, BigQuery, HubSpot API, Kafka, QueryDSL.

**Chức năng.**
- **Sync merge contact** — `POST /api/contact-merge/sync`: sync contact đã merge từ BigQuery (lookback giờ cấu hình được).
- **Scan avatar lỗi** — `POST /api/contact-merge/scan-broken-avatar`: quét + sửa URL avatar lỗi.
- HubSpot REST + publish Kafka.

**Data model.** `HSContact`; mapper HubSpot→MongoDB.

**Tích hợp.** HubSpot API, BigQuery, Kafka, MongoDB.

**Lưu ý.** QueryDSL 4.3.1; annotation processor riêng. Dọn avatar theo cửa sổ thời gian.

## Sources
- [[src-2026-06-22-doltech-tier3-survey]]
