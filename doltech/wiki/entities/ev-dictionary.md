---
title: ev-dictionary
type: entity
entity_type: project
tags: [project, doltech, dictionary, content, ai]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# ev-dictionary

## English

**One-liner.** English-Vietnamese dictionary content platform: word CRUD with rich metadata,
spreadsheet import, AI-powered enrichment (definitions, phonetics, thumbnails, word families), and
topic/collection organization.

**Stack.** Baseline. Integrates **english-utils** (metadata/thumbnails), **n8n** (AI workflows),
Directus, Google service account (Sheets).

**Features.**
- **Dictionary storage (CRUD + publish)** — `/api/storage/*`: create/update/clone/publish, publish-for
  targeting (`AvailableFor`), bulk fetch, paged search. Entity `Dictionary`: term, form, conjugations,
  cefrScale, phonetics, en/vi definitions, examples, enrichments (wordFamily/collocation/pattern/saurus).
- **Sheet import & sync** — `/api/sheet/*`: validate → import; sync meta-data/image/word-family (async batch
  to english-utils); webhook hooks `/api/sheet/hook/sync/*`. Entity `DictionarySheet` tracks `aiRequestGenerate` progress.
- **Collection management** — `/api/collection/*`: same shape as sheet, grouped by `DictionaryType`. Entity `DOLCollection`.
- **Topic hierarchy** — `/api/topic/*`: main/sub topics, bulk update; `Topic.totalWord` auto-incremented.
- **Sheet AI completion flow** — `/api/sheet-sync-ai-completion`: finds incomplete words, batches to n8n
  (text model `ev-dictionary-gpt-4o-json`, image `flux-schnell`); results returned via webhook.
- **Word family sync** — relates base→derived words from english-utils; tracks `existUnLinkedWordFamily`.
- **Reporting & backup** — `Report`/`ReportHistory` track import/sync ops + audit.

**Data model.** `dictionary`, `dictionarySheet`, `collection`, `topic`, `report`, `reportHistory`, AI-completion request/hook.

**Integrations.** english-utils (metadata/thumbnails), n8n (AI gen), user-service, page-management,
document-history, editor-utils, Directus, Google (Sheets), Kafka (wired, dormant).

**Gotchas.** Words aren't complete on import — `AiRequestGenerate` tracks pending/done/failed; sheets stay
"not valid" until AI fills gaps. Webhook hooks are NOT idempotent (dupes possible). Batched syncs (limit ~100).

## Tiếng Việt

**Một dòng.** Nền tảng nội dung từ điển Anh-Việt: CRUD từ vựng với metadata phong phú, import bảng tính,
làm giàu bằng AI (định nghĩa, phiên âm, thumbnail, word family), và tổ chức theo topic/collection.

**Stack.** Baseline. Tích hợp **english-utils** (metadata/thumbnail), **n8n** (workflow AI), Directus, Google (Sheets).

**Chức năng.**
- **Lưu trữ từ điển (CRUD + publish)** — `/api/storage/*`: tạo/sửa/clone/publish, publish-for theo đối tượng,
  fetch hàng loạt, search phân trang. Entity `Dictionary` (term, form, phiên âm, định nghĩa Anh/Việt, ví dụ, enrichment).
- **Import & sync sheet** — `/api/sheet/*`: validate → import; sync metadata/ảnh/word-family (batch async tới
  english-utils); webhook `/hook/sync/*`. Entity `DictionarySheet` theo dõi tiến độ `aiRequestGenerate`.
- **Quản lý collection** — `/api/collection/*`: cấu trúc giống sheet, gom theo `DictionaryType`. Entity `DOLCollection`.
- **Phân cấp topic** — `/api/topic/*`: topic chính/phụ, cập nhật hàng loạt; `Topic.totalWord` tự tăng.
- **Luồng AI completion** — `/api/sheet-sync-ai-completion`: tìm từ thiếu data, batch tới n8n (model text
  `ev-dictionary-gpt-4o-json`, ảnh `flux-schnell`); kết quả trả qua webhook.
- **Sync word family** — liên kết từ gốc→phái sinh từ english-utils; theo dõi `existUnLinkedWordFamily`.
- **Báo cáo & backup** — `Report`/`ReportHistory` ghi nhận thao tác import/sync + audit.

**Data model.** `dictionary`, `dictionarySheet`, `collection`, `topic`, `report`, `reportHistory`, request/hook AI-completion.

**Tích hợp.** english-utils, n8n, user-service, page-management, document-history, editor-utils, Directus, Google Sheets, Kafka (chưa dùng).

**Lưu ý.** Từ chưa hoàn chỉnh khi import — `AiRequestGenerate` theo dõi pending/done/failed; sheet ở trạng thái
"chưa valid" tới khi AI điền đủ. Webhook KHÔNG idempotent (có thể trùng). Sync theo batch (giới hạn ~100).

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
