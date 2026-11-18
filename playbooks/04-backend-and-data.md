# 04. Backend Architecture, Deep Modules & Data Layer Playbook

*Synthesized from Dual-Agent Consensus: **Craft Experts** (John Ousterhout's Deep Modules, Eric Evans DDD Bounded Contexts, Expand-and-Contract Zero-Downtime Migrations, Transactional Outbox) + **AI-Native Practitioners** (`mattpocock/skills` `codebase-design`, `tdd`, `domain-modeling`, `diagnosing-bugs`, PGlite/Testcontainers sub-second loops).*

---

## 1. Trigger & Scope
- **Load When:** Designing core domain services, state machines, database schemas, SQL/ORM migrations, caching, or background workers/queues.
- **Skip When:** Pure UI/CSS changes or static documentation edits.

## 2. Dual-Agent Consensus Standards (Craft + Practitioner)
1. **Deep Modules & The Deletion Test (Ousterhout + `codebase-design`):** Pack rich business invariants, state transitions, and storage mechanics behind a narrow, self-explanatory public interface. Apply the **Deletion Test**: if removing a module deletes complexity rather than pushing it to callers, merge the shallow pass-through wrapper. Place a port/seam only where **at least two adapters exist** (e.g., production + test).
2. **Ubiquitous Domain Language (`GLOSSARY.md` + Sparse ADRs):** Name modules, tables, events, and methods strictly after the domain nouns in `GLOSSARY.md` (never generic `Manager`/`Helper`/`Record` CRUD terms). Record architectural decisions in `docs/adr/` only when a choice is hard to reverse and involves a real trade-off.
3. **Vertical-Slice TDD at Public Seams + In-Memory/PGlite Stand-Ins:** Write one failing behavioral test (`red`) against the module's public interface before writing minimal passing code (`green`). Never mock internal collaborators; use **PGlite** (in-process Postgres) or a shared **Testcontainer** with fast table truncation/transaction rollback for sub-second integration feedback, and mock only true external third parties (Stripe, Twilio).
4. **Expand-and-Contract Zero-Downtime Schema Evolution:** Never couple breaking schema changes to a single deploy. Follow 4 phases: **Expand** (add nullable columns / `CREATE INDEX CONCURRENTLY`), **Dual-Write & Batch Backfill**, **Switch Reads & Verify Parity**, and **Contract** (drop old columns in a subsequent deploy). Enforce `SET lock_timeout = '2s'` (with bounded retry) and `statement_timeout` on every `ALTER TABLE` step—even nullable `ADD COLUMN` expansions—so brief `ACCESS EXCLUSIVE` locks never queue behind slow queries and exhaust connection pools. Always generate migrations via ORM CLI tools (`drizzle-kit generate` / `prisma migrate dev`)—never hand-edit migration journals.
5. **Transactional Outbox & Idempotent Background Workers:** Never dual-write to a database and a job queue/message bus outside a single ACID transaction. Persist domain state + an `outbox` event atomically, and ensure every consumer/worker is idempotent (`ON CONFLICT DO NOTHING/UPDATE` or deduplication ledger) on retry.

## 3. Hard Bans
- **NO** shallow 1:1 pass-through service/repository wrappers or speculative single-implementation interfaces (`IFooService`).
- **NO** destructive CLI commands (`prisma migrate reset`, `drizzle-kit drop`, `DROP COLUMN` in the same deploy) or hand-editing ORM snapshot/journal files.
- **NO** table-locking DDL (`CREATE INDEX` without `CONCURRENTLY`, unbounded full-table `UPDATE` backfills in one transaction).
- **NO** `await db.save(); await queue.publish()` non-transactional dual-writes.
- **NO** theorizing on bug fixes without first writing a deterministic `<5s` reproduction command/test that exits red (`diagnosing-bugs`).

## 4. Antigravity Execution Loop (Skills & Subagents)
1. **Domain & Seam Design:** Load `domain-modeling` and `codebase-design` (plus active `domains/<category>.md`) to align `GLOSSARY.md` and lock the deep module interface.
2. **Red-Green-Refactor Loop:** Load `tdd` (and `migrate-to-shoehorn` for TypeScript partial test data) to implement one vertical slice at a time using targeted single-test commands.
3. **Migration Safety Check:** Load `deprecation-and-migration` to print the planned table/index diff and verify N-1 backward compatibility before generating migrations.
4. **Parallel Code Review:** Run `code-review` (`gstack-review`) to audit standards and spec compliance before merge.

## 5. Definition of Done (Verification Gate)
- Module passes the Deletion Test, public seam tests pass in `<5s`, migrations pass N-1 compatibility and lock-safety checks, outbox/worker idempotency is proven under replay tests, and `GLOSSARY.md`/`docs/adr/` are in sync.

## 6. Scar-Tissue Log
- *(Append real backend, domain, and database lessons here via `/learn`)*
