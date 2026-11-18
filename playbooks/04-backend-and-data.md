# 04. Backend Architecture, Deep Modules & Data Playbook

## 1. Trigger & Scope
- **Load When:** Writing core domain services, state machines, database schemas, SQL/ORM migrations, caching, or background workers/queues.
- **Skip When:** Pure UI/CSS changes or static documentation edits.

## 2. Researched Best Practices (Core Standards)
1. **Deep Modules (Simple Interface, Rich Implementation):** Follow John Ousterhout's *Philosophy of Software Design*: modules should expose a narrow, self-explanatory interface while hiding complex state, retries, and storage mechanics internally.
2. **Ubiquitous Domain Language (`GLOSSARY.md` & ADRs):** Name types, tables, and functions strictly after the domain vocabulary in `GLOSSARY.md`. Record non-obvious architectural trade-offs in `docs/adr/`.
3. **Red-Green-Refactor TDD at Service Seams:** Write failing behavioral tests against the module's public interface (not internal mocks) before implementing domain logic. Use `@total-typescript/shoehorn` instead of unsafe `as` casts in TypeScript tests.
4. **Expand-and-Contract Zero-Downtime Migrations:** Never rename or drop a live database column/table in a single deploy. Expand (add nullable column + dual-write), backfill, switch reads, and contract (drop old column in a later deploy).
5. **Query Discipline & Transactional Integrity:** Wrap multi-write invariants in database transactions, index foreign keys and frequent filter columns, and eliminate N+1 query loops.

## 3. Hard Bans
- **NO** shallow pass-through wrappers that add indirection without hiding complexity.
- **NO** destructive one-step database migrations (`DROP COLUMN`, `RENAME COLUMN`, locking full-table rewrites) on production tables without an expand/contract plan.
- **NO** changing domain behavior without a failing test first (`tdd`).

## 4. Antigravity Execution Loop (Skills & Subagents)
1. **Model & Seam Design:** Load `domain-modeling` and `codebase-design` to align terminology with `GLOSSARY.md` and design deep module interfaces.
2. **Test-First Implementation:** Load `tdd` (and `migrate-to-shoehorn` for TS) to run the red-green-refactor loop.
3. **Migration & Perf Check:** Load `deprecation-and-migration` for schema changes and `performance-optimization` for query paths.
4. **Pre-Merge Review:** Run `code-review` (or `gstack-review`) to check standards and spec compliance in parallel.

## 5. Definition of Done (Verification Gate)
- All unit/integration tests pass (`gstack-verify`), module interfaces are narrow and documented in `GLOSSARY.md`/`docs/adr/` if architectural, and migrations are backward-compatible.

## 6. Scar-Tissue Log
- *(Append real backend/database lessons here via `/learn`)*
