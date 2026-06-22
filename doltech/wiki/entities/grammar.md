---
title: grammar
type: entity
entity_type: project
tags: [project, doltech, content, seo, search]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# grammar

## English

**One-liner.** Grammar content management + SEO publishing platform: theories (lessons), exercises,
topics, and authors, with user progress tracking and Elastic App Search integration.

**Stack.** Baseline + **Elastic App Search** (remote REST client for indexing/search).

**Features.**
- **Topics** — `/api/topics/*`: CRUD, paged by sortOrder, replace/sync. Entity `GrammarTopic` (sortOrder,
  Vietnamese name normalization for slugs).
- **Theories (lessons)** — `/api/theories/*`: create (auto-id `LT-{n}`), update, publish (ALL→syncs SEO+Elastic),
  total-views, paged/published. Entity `GrammarTheory` (extends `EditableDocument`): blog body, TOC, publishFor,
  totalViews, linked `grammarExerciseIds`. Delete blocked if viewed.
- **Exercises (practice)** — `/api/exercises/*`: same shape as theories (auto-id `BT-{n}`). Entity `GrammarExercise`.
- **Authors** — `/api/authors/*`: profiles with credentials/degrees/certificates. Entity `GrammarAuthor`.
- **SEO page management** — `/api/seo-page/*` (admin) + `/public/api/seo-page/*`: unified SEO layer (DOL/Google/Social
  tags, schema JSON-LD, URL/redirects, listingStatus), sitemap, by-url lookup. Entity `SEOPage`.
- **SEO sync** — `SyncSEOPageService` maps theory/exercise/author → SEOPage on publish, then indexes to Elastic.
- **ElasticSearch** — `/api/elastic-search/*` + public search: sync-all/single/remove; only PUBLISHED pages indexed.
- **User progress** — `/api/user/exercises/*`, `/api/user/theories/*`: status (NOT_STARTED/IN_PROGRESS/COMPLETED),
  time read, per-question progress. Entities `UserGrammarExercise`, `UserGrammarTheory`.
- **Landing blog** — homepage content blocks (`/api/landing-blog/*` + public).

**Data model.** `grammarTopic`, `grammarTheory`, `grammarExercise`, `grammarAuthor`, `seoPage`,
`userGrammarExercise`, `userGrammarTheory`, landing blog.

**Integrations.** user-service (cached author info), Elastic App Search (engine `dol-grammar-engine-int`),
Kafka topic `academic-resource-interaction` (wired), Redis cache.

**Gotchas.** Auto human-readable IDs (`LT-`/`BT-`). `noAccentName` for SEO slugs. Soft-delete only if `totalViews<1`.
View counter increments in-memory then saves (possible lost updates under concurrency).

## Tiếng Việt

**Một dòng.** Nền tảng quản lý nội dung ngữ pháp + publish SEO: theory (bài học), exercise, topic, author,
kèm theo dõi tiến độ người dùng và tích hợp Elastic App Search.

**Stack.** Baseline + **Elastic App Search** (REST client để index/search).

**Chức năng.**
- **Topics** — `/api/topics/*`: CRUD, phân trang theo sortOrder. Entity `GrammarTopic` (chuẩn hoá tên tiếng Việt cho slug).
- **Theories (bài học)** — `/api/theories/*`: tạo (auto-id `LT-{n}`), sửa, publish (ALL→sync SEO+Elastic), đếm view,
  phân trang. Entity `GrammarTheory` (body blog, TOC, publishFor, totalViews, liên kết exercise). Không xoá được nếu đã có view.
- **Exercises (luyện tập)** — `/api/exercises/*`: giống theory (auto-id `BT-{n}`). Entity `GrammarExercise`.
- **Authors** — `/api/authors/*`: hồ sơ kèm chứng chỉ/bằng cấp. Entity `GrammarAuthor`.
- **Quản lý trang SEO** — `/api/seo-page/*` + public: tầng SEO hợp nhất (tag DOL/Google/Social, schema JSON-LD,
  URL/redirect, listingStatus), sitemap, tra theo URL. Entity `SEOPage`.
- **Sync SEO** — map theory/exercise/author → SEOPage khi publish, rồi index lên Elastic.
- **ElasticSearch** — `/api/elastic-search/*` + search công khai; chỉ index trang PUBLISHED.
- **Tiến độ người dùng** — `/api/user/exercises|theories/*`: trạng thái, thời gian đọc, tiến độ từng câu.
- **Landing blog** — block nội dung trang chủ.

**Data model.** `grammarTopic`, `grammarTheory`, `grammarExercise`, `grammarAuthor`, `seoPage`,
`userGrammarExercise`, `userGrammarTheory`.

**Tích hợp.** user-service, Elastic App Search (`dol-grammar-engine-int`), Kafka `academic-resource-interaction`, Redis.

**Lưu ý.** Auto id dễ đọc (`LT-`/`BT-`). `noAccentName` cho slug SEO. Chỉ soft-delete khi `totalViews<1`.
Đếm view tăng in-memory rồi save (có thể mất update khi concurrent).

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
