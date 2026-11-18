# End-to-End Application Engineering & GTM Playbook

A centralized "Home Repo" (following Matt Pocock's hub-and-spoke context pattern) that guides AI coding agents across the entire lifecycle of building, shipping, selling, and supporting a software product—without bloating per-project context windows.

## Architecture: Thin Router + Modular Playbooks

Instead of pasting hundreds of lines of rules into every repository, each project keeps a ~20-line `AGENTS.md` file that routes the agent on demand to the 6 stage playbooks in this repository:

| Phase | Playbook File | Scope |
| :--- | :--- | :--- |
| **01. Brainstorm & Spec** | [`playbooks/01-brainstorm-and-spec.md`](./playbooks/01-brainstorm-and-spec.md) | Problem validation, premise interrogation, wedge selection, executable spec before code. |
| **02. Frontend & UI/UX** | [`playbooks/02-frontend-ui-ux.md`](./playbooks/02-frontend-ui-ux.md) | Design tokens (`DESIGN.md`), visual variant exploration, accessible build, live `/browser` QA. |
| **03. Middleware & API** | [`playbooks/03-middleware-and-api.md`](./playbooks/03-middleware-and-api.md) | Contract-first schemas, ingress validation, auth/RBAC, rate limiting, idempotency, error envelopes. |
| **04. Backend & Data** | [`playbooks/04-backend-and-data.md`](./playbooks/04-backend-and-data.md) | Deep modules, domain modeling (`GLOSSARY.md` + ADRs), TDD loop, expand/contract DB migrations. |
| **05. Position, Market & Sell** | [`playbooks/05-position-market-sell.md`](./playbooks/05-position-market-sell.md) | April Dunford positioning, high-converting landing pages, 3-tier value pricing, checkout & PLG funnel. |
| **06. Launch, Support & Ops** | [`playbooks/06-launch-support-and-ops.md`](./playbooks/06-launch-support-and-ops.md) | Pre-launch checklist, post-deploy canary monitoring, RED telemetry, support-ticket-to-regression-test loop. |

## How to Use This Repo Across Projects

1. Clone this repository once to a fixed path on your machine (e.g., `~/engineering-playbook`).
2. Copy [`templates/project-AGENTS.md`](./templates/project-AGENTS.md) into any project's root `AGENTS.md` (or add the routing block to `~/.gemini/config/GEMINI.md`).
3. See [`FRAMEWORK.md`](./FRAMEWORK.md) for the 6-part structure used to research, author, and evolve each playbook.
