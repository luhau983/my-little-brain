# LittleBrain — Log

> One global timeline for both domains. Append-only.
> Entry: `## [YYYY-MM-DD] <op> (<domain>) | <title>`. History: `grep "^## \[" log.md | tail -5`.

## [2026-06-22] schema | LittleBrain initialized
- Created CLAUDE.md schema, README.md, index.md, log.md + folder skeleton. Initialized git repo.

## [2026-06-22] ingest (doltech) | Micronaut Data + MongoDB: Repositories & Predicates
- Source: doltech/raw/articles/micronaut-data-mongodb.md
- Created: doltech/wiki/sources/src-2026-06-22-micronaut-data-mongodb.md
- Entities: doltech/wiki/entities/micronaut.md, mongodb.md
- Concepts: doltech/wiki/concepts/predicate-pattern.md, repository-pattern.md
- Seeded: doltech/wiki/overview.md

## [2026-06-22] schema | Split into two domains: doltech/ + personal/
- Moved raw/, wiki/, outputs/ → doltech/ via git mv (history preserved).
- Created personal/ mirror skeleton (raw/wiki/outputs).
- Updated CLAUDE.md for the two-tree layout; root index.md is now the front door.
- Added per-domain index.md (doltech catalog + empty personal catalog) and personal/wiki/overview.md.

## [2026-06-22] schema (doltech) | Added project-page template
- Created doltech/wiki/entities/_template-project.md (entity_type: project) — a reusable page for
  capturing per-project knowledge: stack, project-specific conventions, gotchas, key decisions, ownership.
- Linked from doltech/index.md under Templates. Workflow: when you learn something special about a
  doltech project, copy the template to `<project-slug>.md` and ingest the learning there.

## [2026-06-22] schema (doltech) | Added ADR template + Dataview dashboard
- Created doltech/wiki/decisions/_template-adr.md (ADR format: context/decision/consequences/alternatives).
- Created doltech/dashboard.md — Dataview views (pages by type, stubs, recently updated, sources).
- Linked both from doltech/index.md.

## [2026-06-22] query (doltech) | What query strategies do we know for Micronaut Data on MongoDB?
- Read: src-2026-06-22-micronaut-data-mongodb, micronaut, mongodb, predicate-pattern, repository-pattern.
- Filed answer back as synthesis: doltech/wiki/syntheses/micronaut-mongodb-query-strategy.md
- Demonstrates the QUERY → file-back loop. doltech/index.md Syntheses updated.

## [2026-06-22] ingest (doltech) | study-hub — pagination perf note
- Source: doltech/raw/transcripts/2026-06-22-study-hub-pagination.md
- Created: doltech/wiki/sources/src-2026-06-22-study-hub-pagination.md
- New entity: doltech/wiki/entities/study-hub.md (entity_type: project, from template)
- New concept: doltech/wiki/concepts/keyset-pagination.md
- Updated: doltech/wiki/entities/mongodb.md (+Performance, +1 source → 2), doltech/wiki/overview.md, doltech/index.md
- Demo ingest — study-hub stack inferred; replace project-specific TODOs with real values.

## [2026-06-22] lint+ingest (doltech) | Real study-hub codebase ingest (superseded demo)
- Read the real project at /home/liuhao/Documents/doltech/spring-monorepo/applications/study-hub.
- Correction: study-hub is **Spring Boot 4 / Java 25 / MongoDB**, NOT Micronaut (earlier demo guess).
- Removed fabricated demo artifacts: raw/transcripts/2026-06-22-study-hub-pagination.md,
  sources/src-2026-06-22-study-hub-pagination.md, concepts/keyset-pagination.md, and the fabricated mongodb Performance note.
- Rewrote entities/study-hub.md with verified facts (stack, architecture, data access, conventions, gotchas).
- Created sources/src-2026-06-22-study-hub-codebase.md; entities/spring-boot.md, querydsl.md; concepts/cqrs-command-query.md.
- Updated mongodb.md (real "At doltech" note + codebase source), overview.md, index.md.
- Schema: added `codebase` to source_type enum in CLAUDE.md.

## [2026-06-22] ingest (doltech) | Full monorepo ingest — Batch 1/3 (8 apps, bilingual)
- Read 8 spring-monorepo apps via parallel Explore agents; created bilingual project pages (EN top, VI below):
  action-history, billing, ev-dictionary, g12, grammar, hsa, junior, k10.
- Created shared source src-2026-06-22-spring-monorepo-survey.md (cited by all app pages).
- index.md: added Projects section (9 apps incl. study-hub). Schema: documented bilingual-page convention.
- Pending: Batch 2/3 (k12, k12-all-subject, material, me-invoice, memories, mental-model, pd-management,
  practice-management) + Batch 3 (referral, seo-redirect, toeic, toeic-assignment, user-academy-event,
  virtual-exam, young-learners-english) + Tier 2/3 (standalone services, micronaut/python/react monorepos).

## [2026-06-22] ingest (doltech) | Full monorepo ingest — Batch 2/3 (8 apps, bilingual)
- Read 8 more spring-monorepo apps (3 via re-dispatch after cost-pause); bilingual project pages:
  k12, k12-all-subject, material, me-invoice, memories, mental-model, pd-management, practice-management.
- index.md Projects updated (17/24 spring apps done). Pending: Batch 3 (referral, seo-redirect, toeic,
  toeic-assignment, user-academy-event, virtual-exam, young-learners-english) + Tier 2/3.

## [2026-06-22] ingest (doltech) | Full monorepo ingest — Batch 3/3 (7 apps) — TIER 1 COMPLETE
- Read final 7 spring-monorepo apps (toeic + young-learners-english via re-dispatch); bilingual project pages:
  referral, seo-redirect, toeic, toeic-assignment, user-academy-event, virtual-exam, young-learners-english.
- ✅ All 24 spring-monorepo applications now have bilingual project pages in doltech/wiki/entities/.
- Note: referral page is from a partial read (agent cost-paused) — flagged for re-ingest.
- Pending Tier 2: standalone services (assignment-service, sat-service, syllabus-service, exercise-v2,
  vocab-v2, online-test-be, course-app-sheet-api/-sync-job, verify-token, offline-course-management).
- Pending Tier 3: micronaut-monorepo, python-monorepo, react-web-monorepo, dol-parent-v2_2 shared libs.

## [2026-06-22] ingest (doltech) | Tier 2 — standalone services (partial: 2 of 10)
- syllabus-service (**Micronaut** / Java 17 — first non-Spring app found) and exercise-v2 (Spring Boot 3, older dol-parent) ingested.
- 3 agents (assignment-service, sat-service, vocab-v2) cost-paused without returning — to re-ingest.
- Blocker noted: Explore subagents increasingly halt on the session cost hook; GateGuard fact-force on every new
  file forces content re-sends. Both inflate cost/latency for the remaining ~8 services + Tier 3. Recommend disabling
  these hooks for the session to finish efficiently.

## [2026-06-22] ingest (doltech) | Tier 2 complete — 10 standalone services
- Added: assignment-service, sat-service, vocab-v2, verify-token, online-test-be (partial), course-app-sheet-api (partial),
  course-app-sheet-sync-job, offline-course-management (stub). (+ syllabus-service, exercise-v2 earlier.)
- Created shared source src-2026-06-22-doltech-standalone-survey.md. Key finding: standalone services are MIXED stack —
  Micronaut (sat, vocab-v2, syllabus, course-app-sheet-*) vs Spring Boot 3 older parent (assignment, exercise-v2, verify-token, online-test-be).
- ✅ All ~34 doltech backend services (24 spring-monorepo + 10 standalone) now catalogued bilingually.
- Re-ingest flags: offline-course-management (stub), online-test-be & course-app-sheet-api (partial), referral (partial).
- Tier 3 (micronaut-monorepo apps, python-monorepo, react-web-monorepo frontend, dol-parent shared libs) NOT started.

## [2026-06-22] ingest (doltech) | Tier 3 complete — FULL doltech ingest done
- micronaut-monorepo: 7 new apps (quiz-test, marking-form-service, final-test-merge-contact-api, hubspot-user-resolver-api,
  sat-service-entrance-final + entrance-test/mid-final-test as stubs). (5 others already done as "standalone".)
- python-monorepo: overview page (7 Python/Restate services: audio, pronunciation, speech, session-orchestrator, restate_ai, vcb_payment, watchdog).
- react-web-monorepo: overview page (Next.js, ~34 frontend apps grouped: LMS / test-taking / landing / referral / admin).
- dol-shared-libraries: reference page cataloguing 35 dol-common-*/dol-component-* modules (parent dol-parent-v2_2).
- ✅ FULL doltech ingested: 24 spring apps + 10 standalone + 7 micronaut + python/react/libs overviews.
- Re-ingest flags: entrance-test, mid-final-test, offline-course-management (stubs); online-test-be, course-app-sheet-api, referral (partial).
