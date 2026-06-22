# doltech — Index

> Work / engineering knowledge catalog. Beerus updates this on every doltech ingest.
> Navigation: read this, then drill into pages. (← [front door](../index.md) · 📊 [dashboard](dashboard.md))

## Overview
- [Overview](wiki/overview.md) — the evolving big picture of doltech engineering knowledge.

## Sources
- [[src-2026-06-22-micronaut-data-mongodb|Micronaut Data + MongoDB: Repositories & Predicates]]
  — 2026-06-22 · article · repository + predicate patterns on Micronaut Data MongoDB.
- [[src-2026-06-22-study-hub-codebase|study-hub — codebase read]]
  — 2026-06-22 · codebase · Spring Boot 4 / Java 25 / MongoDB; CQRS-lite; QueryDSL; conventions & gotchas.

## Entities
- [[micronaut|Micronaut]] — JVM framework (AOT/DI) used for the EdTech backend. (1 source)
- [[mongodb|MongoDB]] — document database; primary datastore. (2 sources)
- [[spring-boot|Spring Boot]] — JVM framework powering the doltech spring-monorepo apps. (1 source)
- [[querydsl|QueryDSL]] — type-safe query library; static PredicateBuilders over MongoDB. (1 source)

## Projects (spring-monorepo apps) — bilingual EN/VI
- [[study-hub|study-hub]] — EdTech kid-exercise service (content CRUD + test-taking).
- [[action-history|action-history]] — central audit: AI history, field-change history, download tracking.
- [[billing|billing]] — subscriptions, payments (FlexPrice), feature access, employee premium.
- [[ev-dictionary|ev-dictionary]] — EN-VI dictionary content + AI enrichment + sheet import.
- [[g12|g12]] — grade-12 exams (11 subjects): authoring, do-test, AI explanations, course integration.
- [[grammar|grammar]] — grammar content + SEO publishing + ElasticSearch + user progress.
- [[hsa|hsa]] — university-entrance exams (VNU/HUST): full/section/practice + AI explanations.
- [[junior|junior]] — Junior-level English exams + AI marking for writing.
- [[k10|k10]] — English exam authoring + do-test + AI marking/explanations.
- [[k12|k12]] — English exams (HS & primary), REAL/CHILL modes, AI explanations.
- [[k12-all-subject|k12-all-subject]] — multi-subject K12 exams (11 subjects) + AI marking (Restate).
- [[material|material]] — BLOG/VIDEO/PDF learning content + student progress + cross-course analytics.
- [[me-invoice|me-invoice]] — e-invoice publishing via MISA MeInvoice (tax compliance).
- [[memories|memories]] — course photo/video archive with EC approval workflow.
- [[mental-model|mental-model]] — mental-model quizzes + leaderboards + course integration.
- [[pd-management|pd-management]] — teacher penalties, bonuses, workload tracking.
- [[practice-management|practice-management]] — practice analytics from 9 exam systems (Kafka), streaks, targets.
- [[referral|referral]] — referral programs, wallets, OTP, rate limiting.
- [[seo-redirect|seo-redirect]] — HTTP 301/302 redirect rules across apps (Excel via n8n).
- [[toeic|toeic]] — TOEIC L/R exam prep (oldest/critical); full tests, academy, AI explanations.
- [[toeic-assignment|toeic-assignment]] — TOEIC speaking/writing AI marking (Restate), payment-gated.
- [[user-academy-event|user-academy-event]] — event tracking + "Bang Vang" leaderboard (Kafka from 11 apps).
- [[virtual-exam|virtual-exam]] — IELTS practice + AI marking (n8n+Restate) + HeyGen speaking.
- [[young-learners-english|young-learners-english]] — Cambridge YLE (Starter/Mover/Flyer) + AI marking.
- _(✅ Tier 1 complete: all 24 spring-monorepo apps ingested.)_

### Tier 2 — standalone services (in progress)
- [[syllabus-service|syllabus-service]] — course syllabus structure (course→week→subweek→resources). **Micronaut**.
- [[exercise-v2|exercise-v2]] — English exercises + AI marking/suggestions (Spring Boot 3, older parent).
- [[assignment-service|assignment-service]] — assignments + multi-role/AI marking (Spring Boot 3, Firebase/DynamoDB).
- [[sat-service|sat-service]] — SAT exams; adaptive; AI explanations (Micronaut/Undertow).
- [[vocab-v2|vocab-v2]] — vocabulary SRS (spaced repetition) (Micronaut).
- [[verify-token|verify-token]] — JWT/OTP phone verification (Spring Boot).
- [[online-test-be|online-test-be]] — online test backend + AI gen (Spring Boot). *partial*
- [[course-app-sheet-api|course-app-sheet-api]] — course/sheet metadata API (Micronaut + BigQuery). *partial*
- [[course-app-sheet-sync-job|course-app-sheet-sync-job]] — cron sync (attendance/Zoom/HubSpot/Sheets) (Micronaut).
- [[offline-course-management|offline-course-management]] — offline/classroom course hub (✅ re-ingested, full; ~107 doc classes).
- _(✅ Tier 2 essentially complete: all ~34 backend services (24 spring + 10 standalone) catalogued.)_

### Tier 3 — micronaut-monorepo (new apps), python, frontend, shared libs
- [[quiz-test|quiz-test]] · [[marking-form-service|marking-form-service]] · [[final-test-merge-contact-api|final-test-merge-contact-api]] ·
  [[hubspot-user-resolver-api|hubspot-user-resolver-api]] · [[sat-service-entrance-final|sat-service-entrance-final]] — micronaut-monorepo apps.
- [[entrance-test|entrance-test]] · [[mid-final-test|mid-final-test]] — micronaut-monorepo apps (✅ re-ingested, full).
- [[python-monorepo|python-monorepo]] — 7 Python services (audio, pronunciation, speech, Restate AI, VCB payment, watchdog).
- [[react-web-monorepo|react-web-monorepo]] — Next.js frontend (~34 apps: LMS, landing, entrance/final-test, referral, admin).
- [[dol-shared-libraries|dol shared libraries]] — 35 `dol-common-*`/`dol-component-*` modules (parent dol-parent-v2_2).
- _(✅ Tier 3 covered — full doltech ingest complete.)_

## Concepts
- [[predicate-pattern|Predicate Pattern]] — composable, type-safe query building. (1 source)
- [[repository-pattern|Repository Pattern]] — abstraction over data access. (1 source)
- [[cqrs-command-query|CQRS-lite]] — command/query split per feature (doltech monorepo convention). (1 source)

## Decisions
_(none yet)_

## Syntheses
- [[micronaut-mongodb-query-strategy|Query strategy: Micronaut Data on MongoDB]] — finders vs predicates;
  when to use which. (filed from a query, 2026-06-22)
- [[spring-monorepo-feature-matrix|Spring-monorepo — Feature Matrix]] — capability comparison across all 24
  spring-monorepo apps (Author/DoTest/AI/Sheet/Course/Kafka/Hist/SEO/Rank). (2026-06-22)
- [[micronaut-monorepo-feature-matrix|Micronaut-monorepo — Feature Matrix]] — 12 micronaut apps × 10 capabilities;
  exam-engines vs CRM/data-ops (HubSpot+BigQuery) clusters. (2026-06-22)

## Templates
- [Project page template](wiki/entities/_template-project.md) — copy to `wiki/entities/<project>.md`
  to capture what's special about working with a doltech project (stack, conventions, gotchas, decisions).
- [ADR template](wiki/decisions/_template-adr.md) — copy to `wiki/decisions/adr-NNNN-<slug>.md` to record
  an architecture decision (context, decision, consequences with "who pays the cost", alternatives).
