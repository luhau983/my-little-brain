# LittleBrain — Log

> Append-only. Each entry: `## [YYYY-MM-DD] <op> | <title>`. History: `grep "^## \[" log.md | tail -5`.

## [2026-06-22] schema | LittleBrain initialized
- Created CLAUDE.md schema, README.md, index.md, log.md.
- Created folder skeleton: raw/{articles,papers,transcripts,books,assets}, wiki/{sources,entities,concepts,decisions,syntheses}, outputs/{slides,charts}.
- Initialized git repo.

## [2026-06-22] ingest | Micronaut Data + MongoDB: Repositories & Predicates
- Source: raw/articles/micronaut-data-mongodb.md
- Created: wiki/sources/src-2026-06-22-micronaut-data-mongodb.md
- New entities: wiki/entities/micronaut.md, wiki/entities/mongodb.md
- New concepts: wiki/concepts/predicate-pattern.md, wiki/concepts/repository-pattern.md
- Seeded: wiki/overview.md
- Index updated; first ingest complete.
