# 18-Agent Dual-Perspective Research Synthesis Index

Every phase playbook (`playbooks/01..06`) and domain category overlay (`domains/01..03`) in this repository was produced by running two independent research agents in parallel and reconciling their findings:

1. **Craft & Domain Authority Agent:** Focused on primary literature, systems engineering textbooks, and category-defining product/engineering teams.
2. **AI-Native Practitioner Agent:** Focused on open-source agent skills (`mattpocock/skills`, Garry Tan's `gstack`), `AGENTS.md`/`CLAUDE.md` production guardrails, and automated verification harnesses.

---

## Phase Research Pairing Matrix

| Phase | Craft Authority Sources Synthesized | Practitioner Workflows Synthesized |
| :--- | :--- | :--- |
| **01. Brainstorm & Spec** | Ryan Singer (*Shape Up*), Marty Cagan (*Inspired* / 4 Risks), Teresa Torres (*Opportunity Solution Trees*), YC ("Hair-on-Fire" wedge), Linear Method | `mattpocock/skills` (`/grill-me` design-tree frontier), `gstack` (`/office-hours` 6 forcing questions & `/plan-ceo-review`), GitHub Spec Kit (EARS syntax & Phase 0 Capability Map) |
| **02. Frontend & UI/UX** | Emil Kowalski (`animations.dev` spring/latency budgets), Rauno Freiberg, Paco Coursey, Linear / Vercel Geist / Stripe / Causal token ladders, WCAG 2.2 AA (SC 2.4.11, 2.5.8) | `DESIGN.md` contract stack, `gstack` (`/design-shotgun` variant comparison board & `/design-review` atomic commits), Playwright a11y snapshots + Chrome DevTools MCP |
| **03. Middleware & API** | Stripe 3-State Idempotency Keys (`in_flight` lock + payload hash), OWASP API Security Top 10 (BOLA/BFLA/BOPLA), RFC 9457 (`application/problem+json`), Post-CVE-2025-29927 defense-in-depth | Wrapper-first route factories (`createProtectedRoute`), `.strict()` Zod / `additionalProperties: false` TypeBox contracts, session-derived tenant predicates, raw-byte `timingSafeEqual` webhooks |
| **04. Backend & Data** | John Ousterhout (*A Philosophy of Software Design* Deep Modules & Deletion Test), Eric Evans (*DDD* Bounded Contexts & Ubiquitous Language), 4-Stage Expand-and-Contract Migrations, Transactional Outbox | `mattpocock/skills` (`codebase-design` two-adapter seam rule, vertical-slice `tdd`, `diagnosing-bugs` `<5s` repro loop), PGlite/Testcontainers sub-second DB isolation, ORM CLI migration locks |
| **05. Position, Market & Sell** | April Dunford (*Obviously Awesome* 5-step positioning & *Sales Pitch* 8-step narrative), Madhavan Ramanujam (*Monetizing Innovation* WTP & value metrics), Elena Verna (PLG & PQA 4 W's) | Stack-specific hero formula, unauthenticated 3-click interactive hero demos, `no-ai-slop` copy gates, `<500ms` fast-ack idempotent billing webhooks + redirect-race polling + daily reconciliation cron |
| **06. Launch, Support & Ops** | Charity Majors / Honeycomb Wide-Event Observability (OpenTelemetry), Google SRE RED/USE metrics, SLO error budgets & multi-window burn-rate alerts, progressive delivery flags | `gstack-ship` + `gstack-land-and-deploy` (exact `MERGE_SHA` verification), `gstack-canary` (10m baseline-diffed monitoring), EvalOps golden datasets (`golden_dataset.jsonl`), Rule-of-3 Scar-Tissue promotion ladder |

---

## Domain Category Pairing Matrix

| Domain Category | Craft Authority Sources Synthesized | Practitioner Workflows Synthesized |
| :--- | :--- | :--- |
| **01. Education & EdTech** | Desmos (Eli Luberoff "math as a verb" & classroom pacing), Math Academy (Justin Skycak directed prerequisite graphs & implicit spaced repetition), Brilliant, Khanmigo, Duolingo, Causal | Split Buyer (parent) / User (student) / Operator (tutor) funnels, stream-buffered KaTeX rendering, presigned upload -> OpenCV -> Mathpix -> SymPy AST verification + Tutor Override, `ParentChild` RBAC bridge, Socratic answer-leak cutoff |
| **02. Algo & Crypto Trading** | Marcos López de Prado (Deflated Sharpe Ratio & Combinatorial Purged CV), Ernest Chan (point-in-time & survivorship-free datasets), NautilusTrader (unified event kernel), Hummingbot | `Decimal` / fixed-point enforcement (hard ban on IEEE-754 `float`), `.shift(1)` lookahead self-audits, deterministic `ClOrdID` status-before-retry, WebSocket `seq_id` gap book invalidation, dual opt-in live gates, Exchange Cancel-on-Disconnect (COD) + independent watchdog |
| **03. Home-Run Bakery & Drops** | Hotplate, Bakesy, BakeryFlow, DoughPlan, Cottage Food non-TCS compliance & sellable-yield batch economics (`20-30%` COGS, `30-40%` net after owner labor) | Per-`DropEvent` + `PickupSlot` pessimistic locks (`SELECT FOR UPDATE` / Redis `DECRBY` with 5–10m TTL), Baker's Percentage (`flour = 100%`) unrounded gram `PrepSheet` & mixer/oven batch splitting, `T-48h` backward fermentation schedule, formula-derived allergen labels, rate-paced SMS drop & porch pickup queues |
