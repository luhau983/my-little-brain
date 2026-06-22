---
title: "Micronaut-monorepo — Feature Matrix"
type: synthesis
tags: [doltech, micronaut-monorepo, feature-matrix, comparison]
created: 2026-06-22
updated: 2026-06-22
status: active
sources: ["[[src-2026-06-22-doltech-tier3-survey]]", "[[src-2026-06-22-doltech-standalone-survey]]"]
---

# Micronaut-monorepo — Feature Matrix

> Cross-app capability comparison of the **12 micronaut-monorepo applications** (all Micronaut 4 / Undertow /
> Java 17 / parent `dol-parent-v2`), synthesized from their per-app wiki pages. ✓ = documented feature; blank = no / n.a.

## English

### Capability matrix

| App | Author | DoTest | AI | Sheet | BigQuery | HubSpot | CourseHub | Kafka | Restate | CMS |
|-----|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| [[sat-service]] | ✓ | ✓ | ✓ | ✓ |  |  | ✓ | ✓ | ✓ | ✓ |
| [[sat-service-entrance-final]] |  | ✓ |  |  |  |  |  | ✓ |  |  |
| [[entrance-test]] | ✓ | ✓ | ✓ |  |  | ✓ | ✓ | ✓ |  | ✓ |
| [[mid-final-test]] | ✓ | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| [[quiz-test]] | ✓ | ✓ |  |  |  |  |  |  |  |  |
| [[vocab-v2]] | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ | ✓ | ✓ |
| [[marking-form-service]] | ✓ |  |  |  |  |  |  |  |  |  |
| [[offline-course-management]] |  |  |  |  |  | ✓ | ✓ | ✓ |  | ✓ |
| [[course-app-sheet-api]] |  |  |  | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| [[course-app-sheet-sync-job]] |  |  |  | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| [[final-test-merge-contact-api]] |  |  |  |  | ✓ | ✓ |  | ✓ |  |  |
| [[hubspot-user-resolver-api]] |  |  |  |  |  | ✓ |  | ✓ |  | ✓ |

**Legend.** Author = content/rubric authoring · DoTest = test execution · AI = AI marking/explanation ·
Sheet = Google-Sheets import · BigQuery = BQ analytics/warehouse · HubSpot = HubSpot CRM sync ·
CourseHub = course/resource metadata or sync hub · Kafka = event publish/consume · Restate = Restate durable
workflows · CMS = Directus/Strapi content integration.

### Observations
- **Two clusters.** (a) **Exam/test engines** that reuse the same backbone as spring-monorepo —
  [[sat-service]], [[sat-service-entrance-final]], [[entrance-test]], [[mid-final-test]], [[quiz-test]], [[vocab-v2]]
  (Author + DoTest + AI). (b) **CRM / data-ops services** that are *distinctive to this monorepo* —
  [[course-app-sheet-api]], [[course-app-sheet-sync-job]], [[final-test-merge-contact-api]], [[hubspot-user-resolver-api]].
- **HubSpot + BigQuery is the signature integration cluster** here (CRM + analytics warehouse) — largely absent
  from spring-monorepo exam apps. The course-app-sheet pair + contact/user resolvers are the CRM data plane.
- **Uniform stack:** unlike the mixed standalone Spring services, every app here is Micronaut 4 / Undertow / Java 17 /
  `dol-parent-v2`, CQRS, MongoDB + QueryDSL.
- **Hubs:** [[course-app-sheet-api]] = course/sheet metadata hub the whole fleet calls; [[offline-course-management]] =
  course/progress hub that backend apps push to.
- **Restate** powers durable AI workflows in [[sat-service]] and [[vocab-v2]] (paired with the Python `restate_ai` service).
- **Utility:** [[marking-form-service]] is a pure rubric-CRUD service (no test/AI/messaging).
- ⚠️ [[quiz-test]] has a known copy-paste bug: `markUsed()` dispatches the delete command.

## Tiếng Việt

Bảng ma trận ở trên dùng chung. Chú giải cột: **Author** = soạn nội dung/rubric · **DoTest** = làm bài ·
**AI** = AI chấm/giải thích · **Sheet** = import Google Sheets · **BigQuery** = analytics/warehouse BQ ·
**HubSpot** = sync CRM HubSpot · **CourseHub** = hub metadata/sync khoá-tài nguyên · **Kafka** = publish/consume ·
**Restate** = workflow bền vững Restate · **CMS** = tích hợp Directus/Strapi.

### Nhận xét
- **Hai cụm.** (a) **Engine thi** dùng lại xương sống như spring-monorepo: [[sat-service]], [[sat-service-entrance-final]],
  [[entrance-test]], [[mid-final-test]], [[quiz-test]], [[vocab-v2]] (Author + DoTest + AI). (b) **Service CRM / data-ops**
  *đặc trưng riêng monorepo này*: [[course-app-sheet-api]], [[course-app-sheet-sync-job]], [[final-test-merge-contact-api]], [[hubspot-user-resolver-api]].
- **HubSpot + BigQuery là cụm tích hợp đặc trưng** ở đây (CRM + warehouse) — gần như không có ở app thi spring-monorepo.
  Cặp course-app-sheet + các resolver contact/user là data plane CRM.
- **Stack đồng nhất:** khác mớ standalone Spring lẫn lộn, mọi app ở đây đều Micronaut 4 / Undertow / Java 17 / `dol-parent-v2`, CQRS, MongoDB + QueryDSL.
- **Hub:** [[course-app-sheet-api]] = hub metadata khoá/sheet cả fleet gọi; [[offline-course-management]] = hub khoá/tiến độ mà backend đẩy về.
- **Restate** chạy workflow AI bền vững trong [[sat-service]] và [[vocab-v2]] (đi cặp service Python `restate_ai`).
- **Tiện ích:** [[marking-form-service]] là service CRUD rubric thuần.
- ⚠️ [[quiz-test]] có bug copy-paste: `markUsed()` lại gọi command delete.

> Lưu ý: ma trận suy ra từ các page wiki từng app (không audit code lại). ✓ = chức năng đã ghi nhận; trống = không có / không áp dụng.

## Sources
- [[src-2026-06-22-doltech-tier3-survey]] · [[src-2026-06-22-doltech-standalone-survey]]
