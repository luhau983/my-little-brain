---
title: young-learners-english
type: entity
entity_type: project
tags: [project, doltech, yle, exam, ai-marking, restate]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# young-learners-english

## English

**One-liner.** Cambridge **Young Learners English (YLE)** exam engine for Starter/Mover/Flyer levels:
test authoring, student test sessions, AI-powered speaking/writing grading (Restate), and TTS audio.

**Stack.** Baseline + **Restate** (AI marking + Inworld TTS), per-level controllers/services (Starter/Mover/Flyer).

**Features.**
- **Data entry (authoring)** — `/api/{level}/{practice,full-test}/*` per level (Starter `/api/starter`, Mover `/api/mover`, Flyer `/api/flyer`):
  CRUD + versioning of parts (practice) and aggregated full tests. Validators per level.
- **Do-test (student)** — `/api/{level}/do-test/*`, `/do-test-overview/*`: start/save/submit, real-time answers.
  Identity = `(studentRegistrationKey, subClassKey)` (no userId). `yle_{level}_user_exam_progress`.
- **AI marking (Speaking + Writing)** — webhook `POST /api/{level}/webhook/{taskId}`, result `GET /api/{level}/marking/result/{taskId}`.
  Restate workflows `workflow-dolkid-{skill}-{test-type}-marking`. `yle_ai_{level}_marking` (taskOutputs[] audit, mapOutput snapshot).
- **AI audio (TTS)** — `POST /api/ai-audio/text-to-speech`: Inworld TTS (`inworld-tts-2`) via Restate.
- **AI recovery** — `/api/{level}/recovery/*`: re-dispatch failed marking tasks.
- **Leaderboard** — `/api/leaderboard/**`: best score per (examTestId, userId). `yle_leaderboard_entry`.
- **Picture sets / Vocab sets** — `/api/picture-set/**`, `/api/vocab-set/**` (vocab → vocab-v2).
- **Analyze / insights** — `/api/{level}/analyze/**`: performance analytics + reasoning trace.

**Data model.** `yle_{level}_{practice,full_test}(_version)`, `yle_{level}_user_exam_progress`, `yle_ai_{level}_marking`,
`yle_picture_set`, `yle_leaderboard_entry`. Enums: YleLevel, YleTestType, YlePartType, YleAnswerState, YleMarkingStatus.

**Integrations.** Restate (`restate-int:8080`; Kong gateway for AI), Inworld TTS, page-management, document-history,
english-utils-worker, editor-utils, s3-service-v2, vocab-v2, Directus; Kafka, Redis.

**Gotchas.** **Known debt: 3-level duplication** (Starter/Mover/Flyer each have own service+controller). Production endpoint
paths/collection names/webhook URLs are fixed contracts — changes need cross-client coordination. AI marking webhook idempotent
(`mapOutput` rebuilt). Starter Speaking Part 1 is rule-scored (no AI). Kid-focused (YLE).

## Tiếng Việt

**Một dòng.** Engine thi Cambridge **Young Learners English (YLE)** cho cấp Starter/Mover/Flyer: soạn đề, học sinh làm bài,
AI chấm speaking/writing (Restate), và audio TTS.

**Stack.** Baseline + **Restate** (AI chấm + Inworld TTS), controller/service riêng từng cấp (Starter/Mover/Flyer).

**Chức năng.**
- **Data entry (soạn)** — `/api/{level}/{practice,full-test}/*` mỗi cấp: CRUD + version part (practice) và full test. Validator theo cấp.
- **Do-test (học sinh)** — `/api/{level}/do-test/*`: start/save/submit. Định danh = `(studentRegistrationKey, subClassKey)` (không userId). `yle_{level}_user_exam_progress`.
- **AI chấm (Speaking + Writing)** — webhook `POST /api/{level}/webhook/{taskId}`, result `GET .../marking/result/{taskId}`.
  Workflow Restate `workflow-dolkid-{skill}-{test-type}-marking`. `yle_ai_{level}_marking`.
- **AI audio (TTS)** — `POST /api/ai-audio/text-to-speech`: Inworld TTS qua Restate.
- **AI recovery** — `/api/{level}/recovery/*`: chạy lại task chấm lỗi.
- **Leaderboard** — `/api/leaderboard/**`: điểm tốt nhất theo (examTestId, userId).
- **Picture/Vocab sets** — `/api/picture-set/**`, `/api/vocab-set/**` (vocab → vocab-v2).
- **Analyze** — `/api/{level}/analyze/**`: phân tích + reasoning trace.

**Data model.** `yle_{level}_{practice,full_test}(_version)`, `yle_{level}_user_exam_progress`, `yle_ai_{level}_marking`,
`yle_picture_set`, `yle_leaderboard_entry`.

**Tích hợp.** Restate (Kong gateway cho AI), Inworld TTS, page-management, document-history, english-utils-worker, editor-utils, s3-service-v2, vocab-v2, Directus; Kafka, Redis.

**Lưu ý.** **Nợ kỹ thuật: lặp 3 cấp** (Starter/Mover/Flyer mỗi cấp 1 service+controller). Path/collection/webhook là contract production cố định.
Webhook AI chấm idempotent. Starter Speaking Part 1 chấm theo rule (không AI).

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
