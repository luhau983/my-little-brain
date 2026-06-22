---
title: seo-redirect
type: entity
entity_type: project
tags: [project, doltech, seo, redirect]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# seo-redirect

## English

**One-liner.** Manages HTTP redirect rules (301/302) across multiple doltech apps, with MongoDB
persistence and Excel bulk import/export via n8n webhooks. Synchronous (no Kafka/Restate).

**Stack.** Baseline (Kafka/Restate present but unused) + n8n Feign client for Sheets↔Excel.

**Features.**
- **Manage redirects (admin)** — `/api/url-redirect/*`: create/update/delete, paged query (by source/target URL, http code, app, date).
  Entity `UrlRedirect` (`urlRedirect`): app (AppEnum: DOL_ENGLISH/TU_HOC_IELTS/TU_DIEN/GRAMMAR), sourceUrl, targetUrl, httpCode.
- **Lookup redirects (public)** — `/public/api/url-redirect/source-url?...`, `/by-app/{app}` (bulk for client-side routing).
  Source URL matched with or without leading `/`.
- **Excel validate & import** — `/api/url-redirect/{validate-excel,import-excel}?spreadSheetUrl=`: fetch sheet via n8n,
  detect duplicates/invalid URL/invalid http code, bulk insert. Errors as `ImportValidationErrorDTO` (row-level).
- **Excel export** — `/api/url-redirect/{export,export-excel}`: JSON → n8n → xlsx bytes.

**Data model.** `urlRedirect` (app, sourceUrl, targetUrl, httpCode + BaseDocument audit).

**Integrations.** n8n (`/webhook/get-sheet-data-by-url`, `/webhook/export-excel-from-json`), user-service (resolve modifier name), Redis cache.

**Gotchas.** Multi-tenant by `AppEnum` (legacy "DOL_ACADEMY" → TU_HOC_IELTS). Only 301/302 allowed (hardcoded regex).
URL normalization treats `/path` == `path`. saveAll not transactional (partial-failure possible).

## Tiếng Việt

**Một dòng.** Quản lý rule redirect HTTP (301/302) cho nhiều app doltech, lưu MongoDB, import/export Excel qua webhook n8n. Đồng bộ (không Kafka/Restate).

**Stack.** Baseline (Kafka/Restate có nhưng không dùng) + n8n Feign client.

**Chức năng.**
- **Quản lý redirect (admin)** — `/api/url-redirect/*`: create/update/delete, query phân trang. Entity `UrlRedirect`: app (AppEnum), sourceUrl, targetUrl, httpCode.
- **Lookup redirect (public)** — `/public/api/url-redirect/source-url?...`, `/by-app/{app}`. Khớp có/không dấu `/` đầu.
- **Validate & import Excel** — `/api/url-redirect/{validate-excel,import-excel}?spreadSheetUrl=`: lấy sheet qua n8n, phát hiện trùng/sai, bulk insert.
- **Export Excel** — `/api/url-redirect/{export,export-excel}`: JSON → n8n → bytes xlsx.

**Data model.** `urlRedirect` (app, sourceUrl, targetUrl, httpCode + audit).

**Tích hợp.** n8n (webhook), user-service, Redis.

**Lưu ý.** Đa tenant theo `AppEnum` (legacy "DOL_ACADEMY" → TU_HOC_IELTS). Chỉ 301/302. Chuẩn hoá `/path` == `path`. saveAll không transaction.

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
