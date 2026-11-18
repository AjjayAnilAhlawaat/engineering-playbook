# End-to-End Application Engineering, GTM & Domain Playbook

A centralized "Home Repo" (built on Matt Pocock's hub-and-spoke context pattern) that guides AI coding agents across the entire lifecycle of building, positioning, selling, and supporting software products—combining **6 Horizontal Lifecycle Playbooks** with **3 Industry Domain Overlays**.

Every module is synthesized from **Dual-Agent Consensus Research** pairing **Craft Experts** (authoritative domain pioneers and system architects) with **AI-Native Practitioners** (open-source agent skills, `AGENTS.md` guardrails, and verification harnesses).

---

## 1. Horizontal Lifecycle Playbooks (`playbooks/`)

| Phase | Playbook File | Dual-Agent Research Foundation (Craft Experts + Practitioners) |
| :--- | :--- | :--- |
| **01. Brainstorm & Spec** | [`playbooks/01-brainstorm-and-spec.md`](./playbooks/01-brainstorm-and-spec.md) | Shape Up (Ryan Singer), Marty Cagan, Teresa Torres, YC, Linear Method + `mattpocock/skills` `/grill-me`, `gstack` `/office-hours` & `/plan-ceo-review`, GitHub Spec Kit. |
| **02. Frontend & UI/UX** | [`playbooks/02-frontend-ui-ux.md`](./playbooks/02-frontend-ui-ux.md) | Emil Kowalski, Rauno Freiberg, Paco Coursey, Linear/Geist/Stripe/Causal, WCAG 2.2 AA + `DESIGN.md` stack, `gstack` `/design-shotgun` & `/design-review`, Chrome DevTools MCP. |
| **03. Middleware & API** | [`playbooks/03-middleware-and-api.md`](./playbooks/03-middleware-and-api.md) | Stripe API Design, OWASP API Top 10, RFC 9457, Post-CVE-2025-29927 Defense-in-Depth + Wrapper Route Factories, `.strict()` Zod/OpenAPI, Session-Derived BOLA Scoping. |
| **04. Backend & Data** | [`playbooks/04-backend-and-data.md`](./playbooks/04-backend-and-data.md) | John Ousterhout Deep Modules, Eric Evans DDD, Expand-and-Contract Migrations, Transactional Outbox + `codebase-design`, `tdd`, `diagnosing-bugs`, PGlite/Testcontainers. |
| **05. Position, Market & Sell** | [`playbooks/05-position-market-sell.md`](./playbooks/05-position-market-sell.md) | April Dunford (*Obviously Awesome* & *Sales Pitch*), Madhavan Ramanujam (*Monetizing Innovation*), Elena Verna (PLG/PLS) + Interactive Hero Demos, Fast-Ack Idempotent Billing. |
| **06. Launch, Support & Ops** | [`playbooks/06-launch-support-and-ops.md`](./playbooks/06-launch-support-and-ops.md) | Charity Majors / Honeycomb Wide Events (OTel), Google SRE RED/USE & Burn-Rate Alerts + `gstack-ship`, `gstack-canary`, EvalOps Golden Datasets, Rule-of-3 Scar-Tissue Ladder. |

---

## 2. Industry / Domain Category Overlays (`domains/`)

Each domain overlay specializes all 6 lifecycle phases (`01` through `06`) for a specific vertical without duplicating core rules:

| Category | Domain Overlay File | Craft & Practitioner Coverage Across Phases 01–06 |
| :--- | :--- | :--- |
| **01. Education & EdTech** | [`domains/01-education-edtech.md`](./domains/01-education-edtech.md) | Desmos, Math Academy, Khanmigo, Causal + KaTeX streaming, OpenCV/Mathpix/SymPy AST grading with Tutor Override, COPPA/FERPA `ParentChild` RBAC, Socratic guardrails, school-calendar anti-churn. |
| **02. Algo & Crypto Trading** | [`domains/02-algo-and-crypto-trading.md`](./domains/02-algo-and-crypto-trading.md) | López de Prado (DSR & Purged CV), Ernest Chan, NautilusTrader, Hummingbot + `Decimal` fixed-point enforcement, `.shift(1)` lookahead bans, `ClOrdID` idempotency, Exchange Cancel-on-Disconnect & Multi-Layer Circuit Breakers. |
| **03. Home Bakery & Drops** | [`domains/03-home-bakery-and-drops.md`](./domains/03-home-bakery-and-drops.md) | Hotplate, BakeryFlow, DoughPlan, Bakesy + Sellable-yield margin math, cottage non-TCS compliance, atomic slot/batch locks (`SELECT FOR UPDATE`), Baker's Percentage gram prep sheets, backward fermentation timelines, SMS porch pickup ops. |

---

## 3. How Any Project Links to This Repo

Copy [`templates/project-AGENTS.md`](./templates/project-AGENTS.md) into a project's root `AGENTS.md` and select its active domain overlay (`01-education-edtech.md`, `02-algo-and-crypto-trading.md`, or `03-home-bakery-and-drops.md`). See [`FRAMEWORK.md`](./FRAMEWORK.md) for the 6-part module specification and dual-agent consensus methodology.
