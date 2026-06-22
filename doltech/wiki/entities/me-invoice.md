---
title: me-invoice
type: entity
entity_type: project
tags: [project, doltech, invoice, integration, tax]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# me-invoice

## English

**One-liner.** Electronic-invoice publishing service for Vietnamese tax compliance via the **MISA
MeInvoice** API: create invoices from internal bills, manage templates/tokens, full audit trail.

**Stack.** Baseline + OpenFeign (MISA client), JetCache token/template caching, Apache Tika. **No Kafka usage observed.**

**Features.**
- **Publish invoice** — `POST /api/publish-invoice`: `InputBillRequestDTO` → transform (`ConvertInvoiceDataHelper`,
  VAT/payment/email) → MISA `POST /invoice` (signType=5) → persist `PublishInvoice` + `PublishInvoiceLog`. Idempotent by `refId`.
- **Retry** — `POST /api/retry-publish-invoice/{logId}`: re-send from a prior log (mapping incomplete — returns null).
- **Lookup** — `GET /api/publish-invoice-info/{refId}`: fetch status from MISA publish-view.
- **Request log** — `GET /api/log-request/{hisId}`: original request JSON for debugging.
- **Token mgmt** — Bearer token per MST, cached 7 days (`MeAuthInvoiceHelper`); test MSTs mapped via `TestCodeUtil`.
- **Template fetch** — invoice templates per business, cached 1 day.

**Data model.** `PublishInvoice` (refId, mst, transactionId, invNo/Series/Code, invDate, errorCode),
`PublishInvoiceLog` (full request+response audit, success flag).

**Integrations.** MISA MeInvoice API (auth/templates/invoice/publishview), MongoDB, Redis cache. JWT per-MST tokens.

**Gotchas.** Idempotency by `refId` (skip re-publish). `DuplicateInvoiceRefID` tolerated; other errors throw. MST stripped
of invisible chars. VAT hardcoded "KCT" (0%, education); unit "Khóa học"; currency VND. BCC hardcoded to an internal email.
Retry feature unfinished. QueryDSL not actually used (standard Spring Data only).

## Tiếng Việt

**Một dòng.** Service phát hành hoá đơn điện tử tuân thủ thuế VN qua API **MISA MeInvoice**: tạo hoá đơn từ bill nội bộ,
quản lý template/token, lưu audit đầy đủ.

**Stack.** Baseline + OpenFeign (client MISA), JetCache cache token/template, Apache Tika. **Không thấy dùng Kafka.**

**Chức năng.**
- **Phát hành hoá đơn** — `POST /api/publish-invoice`: `InputBillRequestDTO` → transform (VAT/thanh toán/email) →
  MISA `POST /invoice` → lưu `PublishInvoice` + `PublishInvoiceLog`. Idempotent theo `refId`.
- **Retry** — `POST /api/retry-publish-invoice/{logId}`: gửi lại từ log cũ (mapping chưa xong — trả null).
- **Tra cứu** — `GET /api/publish-invoice-info/{refId}`: lấy trạng thái từ MISA publish-view.
- **Log request** — `GET /api/log-request/{hisId}`: JSON request gốc để debug.
- **Quản lý token** — Bearer token theo MST, cache 7 ngày; MST test map qua `TestCodeUtil`.
- **Lấy template** — template hoá đơn theo doanh nghiệp, cache 1 ngày.

**Data model.** `PublishInvoice`, `PublishInvoiceLog` (audit request+response, cờ success).

**Tích hợp.** MISA MeInvoice API, MongoDB, Redis. Token JWT theo từng MST.

**Lưu ý.** Idempotent theo `refId`. Lỗi `DuplicateInvoiceRefID` được bỏ qua; lỗi khác thì throw. MST bị strip ký tự ẩn.
VAT hardcode "KCT" (0%, giáo dục); đơn vị "Khóa học"; tiền tệ VND. BCC hardcode email nội bộ. Retry chưa hoàn thiện.
QueryDSL thực tế chưa dùng (chỉ Spring Data chuẩn).

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
