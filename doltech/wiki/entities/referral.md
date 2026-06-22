---
title: referral
type: entity
entity_type: project
tags: [project, doltech, referral, wallet, otp]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# referral

## English

**One-liner.** Referral-program management: signup via referral codes, referrer wallets & payment
reconciliation, admin program configuration, multi-channel OTP, and request rate limiting.

**Stack.** Baseline + **Bucket4j** rate limiting (`@RateLimit` aspect + JCache), Firebase + email + **Zalo** OTP/SMS,
Feign clients (SMS gateway, email verifier, bank lookup, Customer.io, dol-admin, n8n).

**Features.**
- **Admin — program management** — `/api/admin/referral-program/*`: CRUD + publish/expire programs with bonus tiers;
  special groups (targeted cohorts). Entities `ReferralProgram(+Version)`, `SpecialGroup`.
- **User — referral & wallet** — `/api/user/referral/*`: generate/use referral code, redemption tracking, balance inquiry,
  payment history, signup via code. Referrer wallets + transactions.
- **OTP verification** — configurable length(4)/TTL(900s)/retries(5); delivery via email or Zalo (template 522010).
- **Rate limiting** — buckets: default 10/h, otp-resend 1/60s, login 5/15m, signup 3/60s, otp-verify 5/10m.
- **Common** — shared email/data queries, wallet transaction management, error-code providers.

**Data model.** `ReferralProgram(+Version)`, `SpecialGroup`, referral codes, redemption history, referrer wallet/payment.

**Integrations.** SMS gateway, Zalo OTP, Rapid Email Verifier, BankLookup, Customer.io, dol-admin, n8n, Firebase, Google;
shared libs (email, firebase, google-component); MongoDB (transactions), Redis cache.

**Gotchas.** Heavy rate-limiting via `@RateLimit` (Bucket4j). Enum-based error codes (Program/ReferralCode/Role/Zalo).
`maximum-redemption-registrations-per-referrer: 7`. MongoDB multi-doc transactions enabled (`MongoTransactionConfig`).

## Tiếng Việt

**Một dòng.** Quản lý chương trình giới thiệu (referral): đăng ký qua mã, ví & đối soát thanh toán người giới thiệu,
cấu hình chương trình (admin), OTP đa kênh, và rate limit request.

**Stack.** Baseline + **Bucket4j** rate limit, Firebase + email + **Zalo** OTP/SMS, Feign (SMS gateway, email verifier, bank lookup, Customer.io, dol-admin, n8n).

**Chức năng.**
- **Admin — quản lý chương trình** — `/api/admin/referral-program/*`: CRUD + publish/expire, bậc thưởng; special group.
  Entity `ReferralProgram(+Version)`, `SpecialGroup`.
- **User — referral & ví** — `/api/user/referral/*`: tạo/dùng mã, theo dõi redemption, tra số dư, lịch sử thanh toán, đăng ký qua mã. Ví + giao dịch.
- **Xác thực OTP** — độ dài(4)/TTL(900s)/retry(5); gửi qua email hoặc Zalo (template 522010).
- **Rate limit** — default 10/h, otp-resend 1/60s, login 5/15m, signup 3/60s, otp-verify 5/10m.
- **Common** — query email/data dùng chung, quản lý giao dịch ví, error-code provider.

**Data model.** `ReferralProgram(+Version)`, `SpecialGroup`, mã referral, lịch sử redemption, ví/thanh toán.

**Tích hợp.** SMS gateway, Zalo, Rapid Email Verifier, BankLookup, Customer.io, dol-admin, n8n, Firebase, Google; MongoDB (transaction), Redis.

**Lưu ý.** Rate-limit nặng qua `@RateLimit` (Bucket4j). Error code dạng enum. Tối đa 7 redemption/người giới thiệu.
Bật MongoDB transaction đa document.

> Lưu ý: tổng hợp từ bản đọc 1 phần (agent dừng vì cost) — có thể bổ sung khi ingest lại.

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
