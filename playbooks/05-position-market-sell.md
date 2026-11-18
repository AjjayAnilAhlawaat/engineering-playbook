# 05. Positioning, Marketing, Pricing & Sales (GTM) Playbook

## 1. Trigger & Scope
- **Load When:** Defining product positioning, writing landing page or launch copy, designing pricing tiers, wiring Stripe/Paddle/Lemon Squeezy checkout & entitlements, or optimizing user onboarding and conversion funnels.
- **Skip When:** Internal refactoring or backend infrastructure work with no customer-facing surface.

## 2. Researched Best Practices (Core Standards)
1. **April Dunford's 5-Step Positioning Sequence:** Never write marketing copy before locking down in `POSITIONING.md`:
   - *Competitive Alternatives:* What customers actually use today (often spreadsheets, WhatsApp, manual work—not just SaaS rivals).
   - *Unique Capabilities:* Specific mechanics your product has that the alternatives lack.
   - *Value Themes:* The measurable outcome those capabilities unlock (time saved, revenue gained, risk eliminated).
   - *Best-Fit Customer Segment:* The exact buyer profile that feels the pain most acutely and buys fastest.
   - *Market Category:* The category frame that makes your value immediately obvious.
2. **Evidence-Led Landing Pages (Zero AI Slop):** Above the fold must state what the product does, who it is for, why the old way breaks, and show an authentic interactive preview or real workflow artifact within 5 seconds.
3. **Value-Metric 3-Tier Packaging:** Price on the metric that scales with customer value (e.g., active pods/seats/usage). Structure three clear tiers (Starter/Self-Serve, Pro/Growth as the obvious default, and Team/Enterprise) with transparent pricing.
4. **Short Time-to-First-Value (TTFV < 3 Minutes):** Minimize signup friction (SSO / magic link, no multi-field questionnaires before value). Let users reach the "Aha!" moment before hitting a paywall or upgrade trigger.
5. **Webhook-Driven Entitlements:** Gate paid features via server-verified billing webhooks and an explicit `entitlements` table—never trust client-side checkout success redirects alone.

## 3. Hard Bans
- **NO** generic AI marketing copy (*"Unleash the power of…", "Revolutionize your workflow", "Supercharge", "Game-changer"*). Enforce `no-ai-slop` on every word of customer-facing copy.
- **NO** multi-step signup forms asking for phone numbers or company size before the user experiences the product.
- **NO** granting paid plan access purely from a client-side `?success=true` query parameter without verified billing webhook state.

## 4. Antigravity Execution Loop (Skills & Subagents)
1. **Lock Positioning:** Use `interview-me` and `no-ai-slop` to draft a concrete 1-page `POSITIONING.md` following April Dunford's 5 components.
2. **Design & Build Conversion Surface:** Use `gstack-design-shotgun` / `frontend-ui-engineering` to build the landing page, interactive product walkthrough (`gstack-design-motion` for showcase loops), and pricing table.
3. **Audit Onboarding Friction (TTFV):** Run `gstack-devex-review` (or `/browser`) to time the actual onboarding and checkout flow live in the browser and eliminate friction points.

## 5. Definition of Done (Verification Gate)
- `POSITIONING.md` is locked, all landing/onboarding copy passes `no-ai-slop`, checkout + webhook entitlement states (active, past_due, canceled) are tested, and live onboarding reaches first value in under 3 minutes.

## 6. Scar-Tissue Log
- *(Append real GTM, pricing, and conversion lessons here via `/learn`)*
