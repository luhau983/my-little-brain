---
title: hubspot-user-resolver-api
type: entity
entity_type: project
tags: [project, doltech, hubspot, user, micronaut, micronaut-monorepo]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-doltech-tier3-survey]]"]
---

# hubspot-user-resolver-api

## English

**One-liner.** User-resolution service enriching HubSpot contacts with Directus employee data and
course/role metadata from Strapi. Micronaut-monorepo app.

**Stack (detected).** Micronaut / Java 17 (Undertow); MongoDB, HubSpot API, Directus, Strapi, Kafka, QueryDSL, AWS S3.

**Features.**
- **Resolve user by email** — `POST /public/api/hs-user-resolver/by-email` (`{email, userId}` → `HSUserWithRolesDTO`):
  multi-source enrichment (HubSpot + Directus + Strapi). CQRS query handler `GetHubspotUserByEmailQueryHandler`.

**Data model.** `HSUserWithRolesDTO`, `EmployeeDTO` (Directus), `StrapiDolRoleDTO`, `DirectusSearchResponseDTO`.

**Integrations.** HubSpot API, Directus CMS, Strapi CMS, MongoDB, Kafka, AWS S3.

**Gotchas.** Cross-CMS lookups (Directus/Strapi) → latency risk. Custom DTOs map multi-schema. Public endpoint (`/public/...`).

## Tiếng Việt

**Một dòng.** Service phân giải user — làm giàu HubSpot contact bằng dữ liệu nhân viên Directus + metadata course/role từ Strapi. App micronaut-monorepo.

**Stack (detect).** Micronaut / Java 17; MongoDB, HubSpot API, Directus, Strapi, Kafka, QueryDSL, AWS S3.

**Chức năng.**
- **Resolve user theo email** — `POST /public/api/hs-user-resolver/by-email` (`{email, userId}` → `HSUserWithRolesDTO`):
  làm giàu đa nguồn (HubSpot + Directus + Strapi). CQRS query handler.

**Data model.** `HSUserWithRolesDTO`, `EmployeeDTO`, `StrapiDolRoleDTO`, `DirectusSearchResponseDTO`.

**Tích hợp.** HubSpot API, Directus, Strapi, MongoDB, Kafka, AWS S3.

**Lưu ý.** Lookup chéo CMS → rủi ro latency. DTO tuỳ biến map đa schema. Endpoint public.

## Sources
- [[src-2026-06-22-doltech-tier3-survey]]
