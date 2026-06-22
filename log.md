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
