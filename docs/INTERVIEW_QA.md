# Interview Q&A — SyncGuard

### "Tell me about this project."
SyncGuard is cache-consistency reconciliation between the database and the cache. SyncGuard reconciles cache against the database of record, detecting and repairing divergence so read-through/write-aside caching stays correct.

### "What was the hardest part?"
Keeping cache and source of truth consistent under concurrent writes without locking everything.

### "Why did you choose this stack?"
- **Postgres** — relational source of truth.
- **Redis** — in-memory store / cache / queue.

### "How does it fit the rest of your portfolio?"
It follows my "Antigravity" model — local logic/state/UI, cloud reasoning where it earns its cost — and shares the documentation and deployment conventions used across all my projects (#50).
