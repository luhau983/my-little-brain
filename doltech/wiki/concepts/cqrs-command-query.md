---
title: CQRS-lite (Command/Query split)
type: concept
tags: [architecture, cqrs, spring, doltech]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-study-hub-codebase]]"]
---

# CQRS-lite (Command/Query split)

The doltech `spring-monorepo` convention: within each feature, **separate the write path from the
read path** — distinct command vs query controllers, services, and handlers — without full
event-sourced CQRS.

## Shape (per [[study-hub]])
- `controller/command/` + `controller/query/`.
- `service/command/` (interface) + `service/command/handler/` (impl); same for query.
- Command controllers extend `ValidatorController<XxxValidator>`; both inject the **interface**, not the handler.

## Why
Read and write concerns evolve independently; validation/locking live on the command side, caching on
the query side. Keeps handlers small (method soft-cap ~30 lines).

## Related
[[study-hub]] · [[spring-boot]] · [[repository-pattern]]

## Sources
- [[src-2026-06-22-study-hub-codebase]]
