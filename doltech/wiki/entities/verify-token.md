---
title: verify-token
type: entity
entity_type: project
tags: [project, doltech, auth, otp, standalone]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-standalone-survey]]"]
---

# verify-token

## English

**One-liner.** JWT/OTP token-verification service: SMS-based OTP generation & validation (TOTP) for phone
verification. Small, focused auth utility.

**Stack (detected).** **Spring Boot** / Java 11+ / Maven (parent `dol-parent` v1.5); MongoDB (`user-profile` db, v2 active) +
DynamoDB (v1 legacy, dormant); Redis pub/sub message broker; Auth0 (m2m); CQRS. Dockerized via Jib.

**Features.**
- **OTP request v2** — `POST /api/otp/request-v2`: generate TOTP secret, store in MongoDB, send SMS. `UserTokenV2` (phone, secret).
- **OTP verify** — `POST /api/otp/verify`: validate TOTP against stored secret, mark phone verified, delete token.
- **OTP request v1 (legacy)** — `POST /api/otp/request`: DynamoDB-backed, **handler disabled**.
- **SMS gateway integration** — REST to `dol-smsgateway-service` (`SendSmsDTO`).
- **Phone normalization** — `PhoneUtils` (Vietnam region hardcoded, NATIONAL/INTERNATIONAL formats).

**Data model.** `UserTokenV2` (MongoDB: phone, secret, createdAt). `UserToken` (DynamoDB, legacy/dormant).

**Integrations.** dol-smsgateway-service (SMS), dol-user-service (phone/verified update — commented out in v1), Auth0 (m2m),
Redis (broker), MongoDB, DynamoDB (legacy).

**Gotchas.** v1 handler disabled (DynamoDB path non-functional). **v2 doesn't update the user profile's verified flag** (flow
incomplete). No TTL on v2 tokens → stale secrets accumulate. v1 TTL 60s vs v2 900s. Plaintext AWS/Mongo/Redis/Auth0 creds in config.

## Tiếng Việt

**Một dòng.** Service xác thực token JWT/OTP: sinh & kiểm tra OTP qua SMS (TOTP) để verify số điện thoại. Tiện ích auth nhỏ, gọn.

**Stack (detect).** **Spring Boot** / Java 11+ (parent `dol-parent` v1.5); MongoDB (`user-profile`, v2 active) + DynamoDB (v1 dormant); Redis pub/sub; Auth0 (m2m); CQRS. Docker (Jib).

**Chức năng.**
- **OTP request v2** — `POST /api/otp/request-v2`: sinh secret TOTP, lưu MongoDB, gửi SMS. `UserTokenV2`.
- **OTP verify** — `POST /api/otp/verify`: validate TOTP, đánh dấu verified, xoá token.
- **OTP request v1 (legacy)** — `POST /api/otp/request`: DynamoDB, **handler đã tắt**.
- **SMS gateway** — REST tới `dol-smsgateway-service`.
- **Chuẩn hoá số ĐT** — `PhoneUtils` (hardcode vùng VN).

**Data model.** `UserTokenV2` (MongoDB), `UserToken` (DynamoDB, legacy).

**Tích hợp.** dol-smsgateway-service, dol-user-service (cập nhật verified — bị comment ở v1), Auth0, Redis, MongoDB, DynamoDB.

**Lưu ý.** Handler v1 tắt. **v2 không cập nhật cờ verified của user** (luồng chưa hoàn chỉnh). v2 token không có TTL → tích luỹ rác. v1 TTL 60s vs v2 900s. Creds plaintext trong config.

## Sources
- [[src-2026-06-22-doltech-standalone-survey]]
