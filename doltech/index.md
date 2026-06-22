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
- _(✅ Tier 1 complete: all 24 spring-monorepo apps ingested. Tier 2/3 — standalone services + micronaut/python/react monorepos — pending.)_

## Concepts
- [[predicate-pattern|Predicate Pattern]] — composable, type-safe query building. (1 source)
- [[repository-pattern|Repository Pattern]] — abstraction over data access. (1 source)
- [[cqrs-command-query|CQRS-lite]] — command/query split per feature (doltech monorepo convention). (1 source)

## Decisions
_(none yet)_

## Syntheses
- [[micronaut-mongodb-query-strategy|Query strategy: Micronaut Data on MongoDB]] — finders vs predicates;
  when to use which. (filed from a query, 2026-06-22)

## Templates
- [Project page template](wiki/entities/_template-project.md) — copy to `wiki/entities/<project>.md`
  to capture what's special about working with a doltech project (stack, conventions, gotchas, decisions).
- [ADR template](wiki/decisions/_template-adr.md) — copy to `wiki/decisions/adr-NNNN-<slug>.md` to record
  an architecture decision (context, decision, consequences with "who pays the cost", alternatives).
