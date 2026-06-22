---
title: python-monorepo
type: entity
entity_type: monorepo
tags: [project, doltech, python, ai, restate, monorepo]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-tier3-survey]]"]
---

# python-monorepo

## English

**One-liner.** doltech's **Python services** monorepo (per-app `pyproject.toml` + Dockerfile), several
Restate-based — handles audio/speech AI, payments, and ops automation. Complements the Java/Micronaut
backends (which call these for speaking/AI work).

**Apps (7, under `apps/`).**
- **audio_service** — audio file processing/serving (used by [[assignment-service]], [[virtual-exam]] for speaking audio).
- **pronunciation_assessment** — pronunciation scoring for speaking exercises/tests.
- **speech_analyzer** — speech analysis (transcription / quality).
- **session_speaking_orchestrator** — orchestrates live speaking-test sessions (called by [[virtual-exam]]).
- **restate_ai** — **Restate** durable AI workflows (backs AI marking/explanation across [[sat-service]], exam apps).
- **vcb_payment** — Vietcombank (VCB) payment integration.
- **bitbucket_watchdog** — CI/ops automation watching Bitbucket pipelines.

**Stack.** Python (uv/pyproject), Docker per app, **Restate** orchestration, `restate-data/`. Integrates with
JVM backends over Restate/HTTP (the Java apps' "AI marking via Restate/n8n" callbacks land here).

**Gotchas.** Not Java — separate toolchain. AI/speech heavy lifting lives here; backend apps mostly dispatch + receive webhooks.

## Tiếng Việt

**Một dòng.** Monorepo **dịch vụ Python** của doltech (mỗi app có `pyproject.toml` + Dockerfile), nhiều cái nền
**Restate** — lo audio/speech AI, thanh toán, automation vận hành. Bổ trợ backend Java/Micronaut (vốn gọi sang đây cho speaking/AI).

**Apps (7, trong `apps/`).**
- **audio_service** — xử lý/serve file audio (dùng bởi [[assignment-service]], [[virtual-exam]]).
- **pronunciation_assessment** — chấm phát âm cho bài speaking.
- **speech_analyzer** — phân tích giọng nói (transcription/chất lượng).
- **session_speaking_orchestrator** — điều phối phiên speaking test (gọi bởi [[virtual-exam]]).
- **restate_ai** — workflow AI bền vững nền **Restate** (đỡ AI chấm/giải thích cho [[sat-service]] và app thi).
- **vcb_payment** — tích hợp thanh toán Vietcombank.
- **bitbucket_watchdog** — automation CI/vận hành theo dõi pipeline Bitbucket.

**Stack.** Python (uv/pyproject), Docker mỗi app, **Restate**, `restate-data/`. Nối backend JVM qua Restate/HTTP.

**Lưu ý.** Không phải Java — toolchain riêng. Phần nặng AI/speech ở đây; backend chủ yếu dispatch + nhận webhook.

## Sources
- [[src-2026-06-22-doltech-tier3-survey]]
