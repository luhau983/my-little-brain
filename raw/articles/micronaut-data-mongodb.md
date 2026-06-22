# Micronaut Data with MongoDB: Repositories and the Predicate Pattern

Micronaut Data is the data-access layer for the Micronaut framework. Unlike runtime-reflection ORMs,
it computes queries at **compile time** (AOT), so there is no runtime query translation overhead and
errors surface during the build.

For MongoDB, you define a repository interface annotated with `@MongoRepository`. Micronaut Data
generates the implementation. Finder methods like `findByNameAndActiveTrue(String name)` are derived
from the method name at compile time.

For dynamic queries — where the filter depends on optional user input — name-derived methods explode
combinatorially. The **Predicate pattern** solves this: build a composable `Predicate` (or
criteria/filter object) at runtime and pass it to the repository. Each optional filter is a small,
testable function that either adds a constraint or is skipped. Predicates compose with AND/OR.

MongoDB stores documents (BSON). It supports multi-document ACID transactions since v4.0 (replica
sets) and v4.2 (sharded clusters). For EdTech read-heavy workloads, model around access patterns and
use indexes aggressively; embed when data is read together, reference when it grows unbounded.
