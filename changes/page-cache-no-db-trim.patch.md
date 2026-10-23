**Headline:** The page cache keeps answers put without a database inside `max_entries`.

### Fixed
- **The page cache grew past its entries limit (PERF.111).** An
  `ResponseCache.put` without a database (`db is None`, e.g. the list of
  databases) stored its answer without the trim every other put does, so
  those answers piled up past `max_entries` until a thread test's last such
  put broke the cache's own bound. They count against the limit now, and a
  unit test on the cache alone (no Redis) keeps them there.
