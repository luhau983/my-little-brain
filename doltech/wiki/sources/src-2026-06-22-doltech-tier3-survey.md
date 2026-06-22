---
title: "doltech Tier 3 — micronaut-monorepo / python / react / shared libs survey"
type: source
source_type: codebase
author: doltech
url: ""
raw_path: /home/liuhao/Documents/doltech
date_published: 2026-06-22
ingested: 2026-06-22
created: 2026-06-22
updated: 2026-06-22
status: active
tags: [doltech, micronaut-monorepo, python, react, shared-libs, survey]
related: ["[[dol-shared-libraries]]", "[[python-monorepo]]", "[[react-web-monorepo]]"]
---

# doltech Tier 3 — survey

Read (2026-06-22) of the remaining doltech repos beyond the backend service catalog.

## micronaut-monorepo/applications (12 apps)
Houses 12 Micronaut/Java-17 apps. **5 already documented as standalone** ([[sat-service]], [[vocab-v2]],
[[course-app-sheet-api]], [[course-app-sheet-sync-job]], [[offline-course-management]]). **7 new:**
[[entrance-test]], [[mid-final-test]], [[quiz-test]], [[marking-form-service]],
[[final-test-merge-contact-api]], [[hubspot-user-resolver-api]], [[sat-service-entrance-final]].
All: Micronaut + Undertow, MongoDB + QueryDSL, CQRS, parent `dol-parent-v2`.

## python-monorepo (7 apps)
Python services (uv/pyproject + Dockerfile), several Restate-based: see [[python-monorepo]].

## react-web-monorepo (frontend)
Next.js monorepo (`doltech`) with ~34 apps + shared libs: see [[react-web-monorepo]].

## dol-parent-v2_2 (35 shared libs)
`dol-common-*` (models/CQRS/kafka/user) + `dol-component-*` (infra: aws, mongodb, editable-document,
excel, google-drive, etc.): catalogued in [[dol-shared-libraries]].
