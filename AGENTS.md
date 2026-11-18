## End-to-End Engineering, GTM & Domain Router

Keep root context minimal. Load **1 Phase Playbook** + **1 Domain Category Overlay** matching the active task:

### 1. Horizontal Lifecycle Playbooks (`playbooks/`)
- **Brainstorming, validation, or spec writing:** `playbooks/01-brainstorm-and-spec.md`
- **Frontend UI, styling, components, or motion:** `playbooks/02-frontend-ui-ux.md` (plus project `DESIGN.md`)
- **API routes, BFF, auth, validation, or webhooks:** `playbooks/03-middleware-and-api.md`
- **Core domain logic, database schemas, migrations, or workers:** `playbooks/04-backend-and-data.md`
- **Positioning, landing page copy, pricing, checkout, or onboarding:** `playbooks/05-position-market-sell.md`
- **Deployment, CI/CD, telemetry, canary, or support bug triage:** `playbooks/06-launch-support-and-ops.md`

### 2. Industry / Domain Overlays (`domains/`)
- **Education, Tutoring & EdTech (e.g., `loveformaths`):** `domains/01-education-edtech.md`
- **Algorithmic & Crypto Trading Systems:** `domains/02-algo-and-crypto-trading.md`
- **Home-Run Bakery & Pre-Order Drops:** `domains/03-home-bakery-and-drops.md`
