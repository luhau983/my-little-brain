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
