# study-hub — pagination perf note (2026-06-22)

While paginating the lesson list in study-hub, deep pages got slow. Root cause: MongoDB `skip/limit`
scans and discards `skip` documents — cost grows with page depth (≈ O(skip)).

Fix: keyset (range) pagination. Sort by an indexed field (e.g. `_id` or `createdAt`) and fetch the
next page with `{ _id: { $gt: lastSeenId } }` + `limit`. Constant cost regardless of depth; needs the
sort field indexed and a stable tiebreaker.

Trade-off: can't jump to an arbitrary page number (only next/prev). For an infinite-scroll lesson feed
that's fine; for a numbered admin table it isn't — keep offset paging there.
