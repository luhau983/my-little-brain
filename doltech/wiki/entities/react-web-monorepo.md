---
title: react-web-monorepo
type: entity
entity_type: monorepo
tags: [project, doltech, frontend, nextjs, react, monorepo]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-tier3-survey]]"]
---

# react-web-monorepo

## English

**One-liner.** doltech's **frontend** monorepo (`doltech/`, **Next.js** + pnpm workspace) — ~34 apps + shared
`libs`, covering LMS, landing pages, test-taking, referral, and admin. The UI layer over the backend fleet.

**App groups (~34 under `doltech/apps/`).**
- **LMS:** `lms-student`, `lms-teacher`, `lms-v2`, `lms-course-management`, `lms-toeic`, `lms-grammar`, `lms-mental-model`, `lms-eccs`, `lms-ai-mock-test`.
- **Test-taking (student):** `entrance-test-student`, `entrance-test-{junior,sat,toeic}-student`, `entrance-test-v2`,
  `final-test-student`, `final-test-{sat,toeic}-student`, `online-test-v2`, `mid-final-test`, `course-exercise-v2`.
- **Landing / marketing:** `landing-blog`(+`-detail`), `landing-dictionary`, `landing-grammar`, `landing-thpt`, `landing-tuhoc-app`, `marketing`, `dol-career`.
- **Referral / admin:** `referral-user`, `referral-admin`, `sale-admin`, `auth-centralize`.
- **Utility:** `dolvn-redirect`, `email-template`, `qr`.
- Plus `mongo-migration-v2` (DB migration tool) and shared `libs/`.

**Stack.** Next.js (`next start`), pnpm workspace, Biome (lint/format), knip, Figma config, distributed build/deploy
scripts (S3 dist), commitlint. Consumes the backend REST/`/public` APIs documented across the wiki.

**Gotchas.** Each frontend app maps to one or more backend services (e.g. `entrance-test-*-student` → [[entrance-test]];
`final-test-*` → [[mid-final-test]]; `lms-*` → many; `referral-*` → [[referral]]). Distributed build pipeline.

## Tiếng Việt

**Một dòng.** Monorepo **frontend** của doltech (`doltech/`, **Next.js** + pnpm) — ~34 app + `libs` dùng chung,
phủ LMS, landing, làm bài thi, referral, admin. Tầng UI trên toàn bộ backend.

**Nhóm app (~34 trong `doltech/apps/`).**
- **LMS:** `lms-student`, `lms-teacher`, `lms-v2`, `lms-course-management`, `lms-toeic`, `lms-grammar`, `lms-mental-model`, `lms-eccs`, `lms-ai-mock-test`.
- **Làm bài (student):** `entrance-test-*-student`, `entrance-test-v2`, `final-test-*-student`, `online-test-v2`, `mid-final-test`, `course-exercise-v2`.
- **Landing / marketing:** `landing-blog(+detail)`, `landing-dictionary`, `landing-grammar`, `landing-thpt`, `landing-tuhoc-app`, `marketing`, `dol-career`.
- **Referral / admin:** `referral-user`, `referral-admin`, `sale-admin`, `auth-centralize`.
- **Tiện ích:** `dolvn-redirect`, `email-template`, `qr`. + `mongo-migration-v2`, `libs/`.

**Stack.** Next.js, pnpm workspace, Biome, knip, Figma config, script build/deploy phân tán (S3), commitlint. Gọi API REST/`/public` của backend.

**Lưu ý.** Mỗi app frontend ứng với một/nhiều backend (vd `entrance-test-*-student` → [[entrance-test]]; `final-test-*` →
[[mid-final-test]]; `lms-*` → nhiều; `referral-*` → [[referral]]). Pipeline build phân tán.

## Sources
- [[src-2026-06-22-doltech-tier3-survey]]
